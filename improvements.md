# Improvements - Project #07 Industrial Anomaly Detection (MVTec/VisA)

Role: IMPROVER. Output of an independent review of the executed project (frozen ResNet18 mean-feature baseline + PaDiM-lite on three MVTec AD categories: bottle, cable, capsule). All artefacts read; no files modified.

## Top recommendation

**Replace the diagonal-Gaussian PaDiM-lite scorer with a PatchCore coreset memory bank on the same frozen backbone, and run it across all 15 MVTec AD categories plus the 12 VisA categories.** PatchCore (Roth et al. 2022, arXiv:2106.08265) is a near drop-in change that uses k-NN against a coreset-subsampled bank of mid-level patch features instead of fitting one Gaussian per spatial location. It directly fixes the `cable` regression (the documented failure mode is multi-modal normal data, which a memory bank handles natively because each sub-mode survives as its own gallery patches) and is the de facto SOTA on MVTec AD at fixed inference budget. Concrete next steps:

1. Implement `src/model_advanced.py` as a PatchCore variant: same `layer2`+`layer3` patch aggregation already used in the notebook, replace the `mean_pix`/`inv_cov` fit with `sklearn.neighbors.NearestNeighbors` over the train-good patches; downsample the bank to 1 percent or 10 percent with greedy coreset (Sener and Savarese 2017).
2. Run on all 15 MVTec categories + 12 VisA categories. Report image-level AUROC and pixel-level AUROC + AUPIMO.
3. Expected lift on cable: 0.681 (current PaDiM-lite) to ~0.99 at the published recipe; mean across 15 categories is expected near 0.99 with WideResNet50, near 0.97 with ResNet18.

This single change dominates every other suggestion below in expected delta and addresses the project's largest analytical gap (the unexplained cable regression and the three-category-only macro mean).

## Weaknesses and proposed improvements

### 1. Three-category macro mean is not a benchmark number (HIGH)

The current `metrics.json` reports a 0.808/0.850 mean across only `bottle`, `cable`, `capsule`. The MVTec AD convention is to report all 15 categories. A three-category mean that includes the project's worst-case regression (cable) is not directly comparable to any published number, including the Defard 2021 reference cited in the manuscript. Action: extend the existing `03_modeling.ipynb` loop to all 15 MVTec categories and all 12 VisA categories. The pipeline is already streaming-extraction friendly; runtime on CPU is approximately 15-20 minutes per category for ResNet18, so the full 27 categories fit overnight. Add a 15-row + 12-row results table and a macro mean comparable to the literature.

### 2. No pixel-level metrics, no AUPIMO (HIGH)

The brief explicitly cites AUPIMO (Bertoldo et al. 2024) as the recommended bibliography. The current run reports image-level AUROC only and skips ground-truth masks during streaming extraction. AUPIMO is the modern per-image, per-region metric that fixes the well-known instability of pixel-level AUROC at low FPR and is the reviewer-default metric on MVTec since 2024. Action: stop skipping `ground_truth/` members in `category_done()`, compute pixel-level AUROC and AUPIMO using `anomalib.metrics.AUPIMO` or the reference implementation at github.com/jpcbertoldo/aupimo. Add a third column to Table 2 in the manuscript. This single addition aligns the project with the brief's explicit reading list.

### 3. Cable regression is reported but not ablated (HIGH)

The manuscript correctly diagnoses the multi-modal normal-distribution failure mode on cable but does not test the diagnosis. Action: add a one-cell ablation that clusters the train-good cable embeddings into k=2 or k=3 sub-modes (k-means on the layer3 GAP vector), fits a per-sub-mode PaDiM-lite, and scores test images against the nearest sub-mode. If the diagnosis is correct, AUROC should recover from 0.681 toward the centroid baseline's 0.746 or above. This is a 20-line change to `03_modeling.ipynb` and converts a textual hypothesis into a measured result.

### 4. Backbone choice is fixed, never ablated (MEDIUM)

ResNet18 is justified by CPU runtime but never compared against alternatives. Two cheap swaps would substantially strengthen the methods section: (a) WideResNet50-2 with the same channel subsample (the canonical PaDiM/PatchCore backbone, expected to recover most of the cable and capsule gap to Defard 2021); (b) DINOv2 ViT-S/14 features (Oquab et al. 2024, arXiv:2304.07193) which now lead the MVTec leaderboard for any-shot AD methods such as MuSc and AnomalyDINO. Action: parametrise the backbone in `extract_features` and run a 2-3 row backbone-ablation table (ResNet18 vs WideResNet50 vs DINOv2-S) on at least one representative category per regime (bottle, cable, capsule). Document inference latency per image alongside AUROC so the Mittelstand cost-vs-accuracy curve is explicit.

### 5. No requirements.txt, no checkpoint.json, missing reproducibility scaffolding (MEDIUM)

`requirements.txt`, `checkpoint.json`, `data/README.md`, and `src/model_baseline.py`/`src/model_advanced.py` are all absent (the QA-rules common-artefact list expects them). The notebook uses torch, torchvision, sklearn, PIL, numpy, matplotlib but pins no versions. `src/` is empty, which makes the pipeline notebook-only and unreusable from a script. Action: (a) create `requirements.txt` pinning the four core libraries by major-minor version (`torch==2.x`, `torchvision==0.x`, `scikit-learn==1.5.x`, `Pillow==10.x`); (b) refactor the modeling notebook into `src/model_baseline.py` (centroid scorer) and `src/model_advanced.py` (PaDiM-lite or PatchCore) with a CLI; (c) add `checkpoint.json` with `project_number`, `title`, `methodology`, `status` fields per the QA schema; (d) add `data/README.md` documenting the two `.tar`/`.tar.xz` archives, their SHA256 sums and the streaming-extraction protocol.

### 6. Single-seed evaluation, no confidence intervals (MEDIUM)

Both scorers are run with one fixed random seed for the channel subsample (PaDiM 100 channels via `np.random.RandomState(0)`). The published PaDiM ablation shows the AUROC variance across seeds at 100 channels is on the order of 0.01-0.02 AUROC; the manuscript reports differences such as the bottle delta of 0.002 that are well inside this seed noise. Action: re-run the PaDiM-lite scorer with five seeds (0, 1, 2, 3, 4) and report the median AUROC plus the 5-95 percentile band per category. State explicitly when a category-level delta is inside seed noise. This is a 5-line loop and converts numeric claims that currently have no uncertainty into defensible point estimates.

### 7. Image preprocessing collapses native resolution (MEDIUM)

Images are resized to 224x224 before feature extraction, discarding most of the native 1024x1024 resolution. Capsule defects can occupy under one percent of the image area (the manuscript says so explicitly in section 2). At 224x224 such defects are subpixel. Action: add a higher-resolution path that resizes to 448 or 512, runs ResNet18 in fully-convolutional mode (the backbone is FCN-friendly), and reports AUROC at the higher resolution. Published EfficientAD and PatchCore numbers use 224 because they tune the network with that input; an off-the-shelf frozen ResNet18 still benefits from 448 inputs on MVTec capsule and screw. Expected lift: 0.02-0.05 AUROC on capsule.

### 8. No supervised multi-class objective addressed (MEDIUM)

The brief explicitly states a second objective: per-defect multi-class classification. The current run delivers binary anomaly detection only. Action: add a third notebook (`04_multiclass.ipynb`) that trains a linear probe on top of the frozen ResNet18 layer3 GAP features, using only the test-defect images grouped by their folder-name defect type. Report per-class precision/recall/F1 and a confusion matrix per category with at least three defect types (bottle, cable, capsule, hazelnut, pill all qualify). This closes the brief's second objective which is currently unaddressed.

### 9. VisA archive present but never modeled (LOW)

VisA was indexed in the EDA notebook but the modeling pipeline only touches MVTec. Cross-dataset evaluation (train PaDiM/PatchCore on MVTec, score on VisA) is the standard robustness test cited by the RAD benchmark in the brief. Action: add a single cross-dataset cell that loads MVTec-trained statistics and scores VisA test images of the matching category (capsules, candle, cashew). Report degradation vs in-domain AUROC. This is a credible bonus result with a 30-line addition.

### 10. Presentation HTML is technical, not business-facing (LOW)

The deliverable is a research-style presentation with method names (PaDiM, ResNet18, Mahalanobis) front-and-centre. A Mittelstand quality-assurance buyer needs cost (euro per inspected unit), throughput (units per hour), and defect-recall at fixed false-alarm-rate (operating-point ROC, not AUROC). Action: add one slide with a single ROC operating point per category at FPR=0.01 and report the corresponding TPR, alongside a back-of-envelope euro estimate (CPU-cycle cost per image times throughput). Move method internals to an appendix slide. The current presentation reads as a method paper, which is appropriate for graders but reduces sales utility.

## Summary scoring

| # | Improvement | Priority |
|---|---|---|
| 1 | All 15 MVTec + 12 VisA categories | HIGH |
| 2 | Pixel AUROC + AUPIMO | HIGH |
| 3 | Cable sub-mode ablation | HIGH |
| 4 | WideResNet50 / DINOv2 backbone ablation | MEDIUM |
| 5 | requirements.txt + src/ scripts + checkpoint.json | MEDIUM |
| 6 | Multi-seed evaluation with CIs | MEDIUM |
| 7 | 448-px input ablation for small-defect categories | MEDIUM |
| 8 | Per-defect multi-class linear probe (brief objective 2) | MEDIUM |
| 9 | Cross-dataset MVTec to VisA transfer | LOW |
| 10 | Operating-point + cost slide for business audience | LOW |
| Top | PatchCore memory bank as primary advanced model | HIGH |
