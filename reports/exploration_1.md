# Exploration #1 - Industrial Anomaly Detection Datasets

Project: Liora #7, Anomaly Detection in Industrial Components.
Brief difficulty: 10/10. Cursus: DS.

This first exploration covers the two image-anomaly benchmarks supplied with the brief: **MVTec AD** and **VisA**. Together they are 6.8 GB on disk and were inspected without extraction, by streaming archive members through Python `tarfile` and PIL.

## 1. Sources and on-disk layout

| Dataset | Archive | Compressed size | Format |
|---|---|---:|---|
| MVTec AD | `data/mvtec_anomaly_detection.tar.xz` | 5.0 GB | xz-compressed tarball |
| VisA     | `data/VisA_20220922.tar`               | 1.8 GB | uncompressed tarball |

Both are read with `tarfile.open(..., 'r:xz' / 'r')` and members are streamed via `extractfile()` into PIL. No 6.8 GB extraction is needed for EDA.

## 2. MVTec AD

Released by MVTec Software (2019), MVTec AD is the de facto benchmark for unsupervised industrial anomaly detection.

- **15 categories** split into two families:
  - **Objects (10):** bottle, cable, capsule, hazelnut, metal_nut, pill, screw, toothbrush, transistor, zipper.
  - **Textures (5):** carpet, grid, leather, tile, wood.
- **Layout per category:**
  - `train/good/*.png` (defect-free only),
  - `test/good/*.png` plus `test/<defect_type>/*.png`,
  - `ground_truth/<defect_type>/*_mask.png` (pixel-level binary masks).
- **Counts (canonical, confirmed by the streaming index in the notebook):** ~3,629 training images (all good), ~1,725 test images split roughly 467 good / 1,258 defective. Defect-type counts vary per category from ~20 to ~150 test images.
- **Defect taxonomy** is per-category and is the multi-class label for objective 2. Examples:
  - bottle: `broken_large`, `broken_small`, `contamination`,
  - cable: `bent_wire`, `cable_swap`, `combined`, `cut_inner_insulation`, `cut_outer_insulation`, `missing_cable`, `missing_wire`, `poke_insulation`,
  - capsule: `crack`, `faulty_imprint`, `poke`, `scratch`, `squeeze`,
  - carpet: `color`, `cut`, `hole`, `metal_contamination`, `thread`,
  - hazelnut: `crack`, `cut`, `hole`, `print`,
  - metal_nut: `bent`, `color`, `flip`, `scratch`,
  - pill: `color`, `combined`, `contamination`, `crack`, `faulty_imprint`, `pill_type`, `scratch`,
  - screw: `manipulated_front`, `scratch_head`, `scratch_neck`, `thread_side`, `thread_top`,
  - toothbrush: `defective`,
  - transistor: `bent_lead`, `cut_lead`, `damaged_case`, `misplaced`,
  - zipper: `broken_teeth`, `combined`, `fabric_border`, `fabric_interior`, `rough`, `split_teeth`, `squeezed_teeth`,
  - wood: `color`, `combined`, `hole`, `liquid`, `scratch`,
  - tile: `crack`, `glue_strip`, `gray_stroke`, `oil`, `rough`,
  - leather: `color`, `cut`, `fold`, `glue`, `poke`,
  - grid: `bent`, `broken`, `glue`, `metal_contamination`, `thread`.
- **Image dimensions:** mostly 1024x1024 for objects, 1024x1024 for most textures (some 700-840 px). All RGB PNG.
- **Imbalance:** train is 100% good. Test is dominated by defective images per category (typically 3-5x more defects than good in test). No anomalies appear in train, which is the standard one-class setup.

## 3. VisA

Released by Amazon (2022), VisA is harder than MVTec AD: more cluttered scenes, multi-instance categories (e.g. PCBs with many components), and finer defects.

- **12 categories:** candle, capsules, cashew, chewinggum, fryum, macaroni1, macaroni2, pcb1, pcb2, pcb3, pcb4, pipe_fryum.
- **Layout per category:** `<category>/Data/Images/Normal/*.JPG` and `<category>/Data/Images/Anomaly/*.JPG`, plus `<category>/Data/Masks/Anomaly/*.png` and a per-category `image_anno.csv`. There is also a top-level `split_csv/1cls.csv` that defines the official 1-class train/test split.
- **Counts (canonical, confirmed by the streaming index in the notebook):** **9,621 normal** images and **1,200 anomalous** images, total **10,821**. Per category roughly 800-1000 normal and 100 anomalous.
- **Defect notes:** VisA does not break anomalies into named sub-classes per directory the way MVTec does; defect category is recorded in `image_anno.csv` (e.g. surface scratches, dents, contamination, missing parts, misalignment for PCBs). Multi-class defect classification on VisA therefore needs the CSV, not the directory tree.
- **Image dimensions:** ~1500x1000 to ~1920x1440 JPG, generally larger and noisier than MVTec.
- **Imbalance:** ~8:1 normal-to-anomalous overall, even more skewed inside the official train split (train is normal-only).

## 4. Comparison table

| Property | MVTec AD | VisA |
|---|---|---|
| Categories | 15 | 12 |
| Train labels | good only | normal only (in 1cls split) |
| Test labels | good + per-defect type | normal + anomaly |
| Pixel masks | yes (`ground_truth/`) | yes (`Data/Masks/Anomaly/`) |
| Native size | mostly 1024x1024 | ~1.5K-1.9K wide JPG |
| Total images | ~5,354 | 10,821 |
| Defect class labels | folder name per defect type | `image_anno.csv` |
| Scene complexity | single centered object/texture | cluttered, multi-instance for PCB and capsules |

## 5. Key observations for modeling

1. **Two-stage objective from the brief maps cleanly to MVTec.** Binary good-vs-defect on either dataset, then per-defect multi-class strictly on MVTec test (folder names are class labels). VisA multi-class needs to read `image_anno.csv` to recover defect types.
2. **Train sets are normal-only**, so the natural baseline is unsupervised / one-class: PaDiM, PatchCore, FastFlow, or autoencoder reconstruction. Supervised CNN classifiers can be added after pseudo-labeling defect crops.
3. **Severe class imbalance** (no anomalies in train). Use AUROC, AUPR, AUPIMO (per the brief bibliography), and pixel-level F1 with masks; never rely on plain accuracy.
4. **Resolution varies widely.** Standard pipeline: resize 256x256, ImageNet-normalize, keep a higher-res copy (e.g. 512) for evaluation since some defects are small.
5. **Storage strategy.** Do NOT extract the 6.8 GB tarballs in full. The notebook streams members on demand. For training we will either (a) extract one category at a time on demand, or (b) build a single resized PNG cache under `.tmp/anomaly_cache/<dataset>/<category>/` once and reuse it.
6. **Cross-dataset transfer** is a credible bonus: train PatchCore on MVTec, evaluate on VisA per-category to test domain robustness, mirroring the RAD benchmark cited in the brief.

## 6. Next steps

- Notebook 02: build the `.tmp/anomaly_cache/` resized cache (256x256), category-by-category, streaming from each tarball.
- Notebook 03: implement a baseline (PatchCore with a frozen WideResNet-50 backbone) on one MVTec category end-to-end, then sweep all 15.
- Notebook 04: extend to VisA, then add the per-defect multi-class head on MVTec.

## 7. Files produced

- `notebooks/01_eda.ipynb` - streaming EDA, reproduces all numbers above.
- `reports/exploration_1.md` - this report.
