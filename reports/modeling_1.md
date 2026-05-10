# Modeling 1 - Mean-Feature Baseline (MVTec AD)

## Task

Image-level anomaly detection on three MVTec AD categories (`bottle`, `cable`, `capsule`). Train on normal-only, score test images (good + defective) by their distance from a per-category training-set centroid in deep feature space.

## Data and pipeline

The 4.9 GB tar.xz archive was streamed (not unpacked) with `tarfile.open('r:xz')`. Only the chosen 3 categories' `train/good/` and `test/{good, defect_*}/` PNG members were extracted to a working directory; all `ground_truth/` mask members were skipped (image-level metric only).

Per-category counts:

| Category | Train (good) | Test (good) | Test (defect) |
|---|---|---|---|
| bottle | 209 | 20 | 63 |
| cable | 224 | 58 | 92 |
| capsule | 219 | 23 | 109 |

## Method

1. PIL load -> RGB -> Resize 256 -> CenterCrop 224 -> ImageNet normalisation.
2. Forward through frozen ResNet18 (`IMAGENET1K_V1` weights, `requires_grad_(False)`, `eval()` mode).
3. Capture `layer3` activation (256 channels x 14 x 14), apply global average pooling -> 256-d image feature.
4. Compute per-category mean `mu_c` over all train (good) features.
5. Score each test image by L2 distance `||x - mu_c||`.
6. Compute image-level AUROC on the test labels (0 = good, 1 = defect).

## Results

| Category | Baseline AUROC |
|---|---|
| bottle | **0.988** |
| cable | 0.746 |
| capsule | 0.691 |
| **Mean across 3 categories** | **0.808** |

The bottle category, where normal images cluster tightly around a single visual mode (a glass bottle, fixed pose, clean background), is essentially solved by this 256-d centroid. Cable (multiple cable types per category, high intra-class diversity) and capsule (subtle defects against a smooth background) sit much lower; both motivate the spatially-aware PaDiM extension in `modeling_2.md`.

## Configuration details

- Backbone: `torchvision.models.resnet18(weights=ResNet18_Weights.IMAGENET1K_V1)`.
- Forward hook on `layer3` to capture activations.
- Feature pooling: global average over the spatial axes.
- Distance: standard L2.
- No standardisation / whitening.
- Random seeds: `torch.manual_seed(0)`, `np.random.seed(0)`.

## Limitations

- A single global mean is wrong for multi-modal normal distributions (cable, where each image shows a different cable type).
- GAP discards spatial layout, so localised defects affecting a small patch are diluted by the rest of the image.
- L2 treats all 256 channels as equally important; channels with high variance dominate the score even if they carry no defect signal.

These limitations motivate the per-pixel multivariate-Gaussian variant in `modeling_2.md`.

## Persisted artifacts

- `deliverables/metrics.json` - per-category AUROC for both methods plus the mean.
- `deliverables/anomaly_features.npz` - example per-image GAP features (bottle category).
- Streaming-extracted MVTec category data lives at `[local temp dir] (regenerable from the tar.xz archive).
