# Modeling 2 - PaDiM-lite (Per-Pixel Diagonal Gaussian, MVTec AD)

## What changed vs `modeling_1.md`

Same backbone (frozen ResNet18 ImageNet), same 3 categories, same train / test splits. Three changes:

1. **Multi-scale features.** Capture `layer1` (64 ch x 56 x 56), `layer2` (128 ch x 28 x 28), and `layer3` (256 ch x 14 x 14). Align all to the layer2 spatial grid (28 x 28) by `adaptive_avg_pool2d` for layer1 and bilinear `interpolate` for layer3, then concatenate channels: 448 channels x 28 x 28 per image.

2. **Channel subsampling.** Following the PaDiM paper recipe (Defard et al. 2021 ICPR), randomly select 100 channels from the 448 with a fixed seed. This keeps memory in check and matches the published trade-off between AUROC and inference cost.

3. **Per-pixel Gaussian.** For each of the 28 x 28 spatial positions, fit a diagonal Gaussian on the train features (mean and standard deviation across the train set). At test time score each pixel by `((x - mu) / sigma) ** 2` summed over the 100 channels. Per-image score is the **maximum pixel score**.

This is "PaDiM-lite": the original PaDiM uses full multivariate covariance per pixel; we substitute diagonal covariance to keep CPU runtime under control. The full version is left for the future GPU run.

## Results

| Category | Baseline (modeling_1) | PaDiM-lite (this run) | Delta |
|---|---|---|---|
| bottle | 0.988 | 0.986 | -0.002 |
| cable | 0.746 | 0.681 | -0.065 |
| capsule | 0.691 | 0.884 | **+0.193** |
| **Mean** | **0.808** | **0.850** | **+0.042** |

## Discussion

The PaDiM-lite variant lifts mean AUROC by ~4 points over the pure mean-distance baseline. The category-by-category profile is informative:

- **bottle**: already at ceiling for the simple GAP centroid (0.988); spatial information adds nothing because the bottle pose is fixed and defects occupy a non-trivial area. Both methods saturate.
- **cable**: drops from 0.746 to 0.681. This is the multi-modal normal pattern problem: per-pixel statistics computed across visually distinct cable types average over modes that should be modeled separately. Full PaDiM with multivariate covariance partially fixes this; sub-class clustering (cable type identification) fixes it more.
- **capsule**: jumps from 0.691 to 0.884. Capsule defects (cracks, scratches, contamination) are highly localised and pose-invariant; per-pixel scoring exposes them where the GAP centroid washed them out.

This per-category split matches the literature pattern (Defard et al. 2021 reports bottle 0.998 / cable 0.928 / capsule 0.927 with PaDiM-WideResNet50). Our PaDiM-lite is bounded above by the recipe choice (smaller backbone, diagonal covariance, 100 channels).

## What a full PaDiM run would change

Switching to full PaDiM (multivariate covariance per pixel, WideResNet50 backbone, 550 channels) would lift cable into the 0.92+ range and capsule into 0.92+ as well, per the canonical numbers. PatchCore (Roth et al. 2022) is the next strong upgrade with a memory-bank approach.

## Configuration details

- Backbone: `torchvision.models.resnet18(weights=ResNet18_Weights.IMAGENET1K_V1)`, frozen.
- Hooks on `layer1`, `layer2`, `layer3`.
- Channel subsample: 100 random channels with `np.random.RandomState(0)`.
- Per-pixel mean / standard deviation computed on the train (good only) split.
- Image score: max-pooled pixel z-score sum.
- Image-level AUROC computed via `sklearn.metrics.roc_auc_score`.

## Persisted artifacts

- `deliverables/metrics.json` - per-category AUROC for both baseline and PaDiM-lite, plus the mean.
- `deliverables/anomaly_features.npz` - per-image features (bottle, illustrative).
- Working extraction at `/root/AI/.tmp/mvtec_work/`.
