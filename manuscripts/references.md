# References: Industrial Anomaly Detection on MVTec AD + VisA

All entries verified via arXiv API and complementary searches (Semantic Scholar, CVF Open Access, Springer) on 2026-05-01. Each ref provides a verifiable arXiv ID or DOI.

## Datasets

1. **Bergmann, P., Fauser, M., Sattlegger, D., Steger, C. (2019).** MVTec AD - A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection. *CVPR 2019*, pp. 9592-9600. DOI: 10.1109/CVPR.2019.00982.
   - First multi-object, multi-defect industrial AD dataset (15 categories, 5354 images, pixel-accurate ground truth).

2. **Bergmann, P., Batzner, K., Fauser, M., Sattlegger, D., Steger, C. (2021).** The MVTec Anomaly Detection Dataset: A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection. *International Journal of Computer Vision*, 129(4), 1038-1059. DOI: 10.1007/s11263-020-01400-4.
   - IJCV journal extension of MVTec AD with thorough evaluation, threshold-selection techniques, and runtime/memory analysis.

3. **Zou, Y., Jeong, J., Pemula, L., Zhang, D., Dabeer, O. (2022).** SPot-the-Difference Self-Supervised Pre-training for Anomaly Detection and Segmentation. *ECCV 2022*. arXiv: 2207.14315.
   - Introduces VisA dataset (12 categories, 10,821 images) and a self-supervised pre-training scheme via spot-the-difference contrastive task.

4. **Wang, C., Zhu, W., Gao, B.-B., et al. (2024).** Real-IAD: A Real-World Multi-View Dataset for Benchmarking Versatile Industrial Anomaly Detection. *CVPR 2024*. arXiv: 2403.12580.
   - Large-scale multi-view dataset (150K images, 30 objects) with sample-level metrics and a fully-unsupervised IAD setting.

## Reconstruction-based methods

5. **Bergmann, P., Loewe, S., Fauser, M., Sattlegger, D., Steger, C. (2019).** Improving Unsupervised Defect Segmentation by Applying Structural Similarity to Autoencoders. *VISAPP 2019*. arXiv: 1807.02011.
   - Replaces per-pixel L2 with SSIM loss in autoencoders for crisper defect localization on textures.

6. **Akcay, S., Atapour-Abarghouei, A., Breckon, T.P. (2018).** GANomaly: Semi-Supervised Anomaly Detection via Adversarial Training. *ACCV 2018*. arXiv: 1805.06725.
   - Encoder-decoder-encoder GAN; anomalies scored by latent reconstruction error after training only on normals.

7. **Schlegl, T., Seeboeck, P., Waldstein, S.M., Langs, G., Schmidt-Erfurth, U. (2019).** f-AnoGAN: Fast Unsupervised Anomaly Detection with Generative Adversarial Networks. *Medical Image Analysis*, 54, 30-44. DOI: 10.1016/j.media.2019.01.010.
   - Encoder-augmented WGAN enabling fast anomaly mapping; widely cited industrial/medical AD baseline.

8. **Gong, D., Liu, L., Le, V., Saha, B., Mansour, M.R., Venkatesh, S., van den Hengel, A. (2019).** Memorizing Normality to Detect Anomaly: Memory-augmented Deep Autoencoder for Unsupervised Anomaly Detection. *ICCV 2019*. arXiv: 1904.02639.
   - MemAE adds a memory module to autoencoders to prevent generalization to anomalies.

## Feature-embedding / memory-bank methods

9. **Cohen, N., Hoshen, Y. (2020).** Sub-Image Anomaly Detection with Deep Pyramid Correspondences (SPADE). arXiv: 2005.02357.
   - Multi-resolution kNN matching of deep features against a normal-image gallery for joint detection and localization.

10. **Defard, T., Setkov, A., Loesch, A., Audigier, R. (2021).** PaDiM: a Patch Distribution Modeling Framework for Anomaly Detection and Localization. *ICPR Workshops 2021*. arXiv: 2011.08785.
    - Per-patch multivariate Gaussian over pretrained-CNN features; Mahalanobis distance gives anomaly maps.

11. **Roth, K., Pemula, L., Zepeda, J., Schoelkopf, B., Brox, T., Gehler, P. (2022).** Towards Total Recall in Industrial Anomaly Detection (PatchCore). *CVPR 2022*. arXiv: 2106.08265.
    - Coreset-subsampled memory bank of mid-level patch features; SOTA for years on MVTec AD (~99.6% AUROC).

## Knowledge-distillation methods

12. **Bergmann, P., Fauser, M., Sattlegger, D., Steger, C. (2020).** Uninformed Students: Student-Teacher Anomaly Detection with Discriminative Latent Embeddings. *CVPR 2020*. arXiv: 1911.02357.
    - Ensemble of students mimic a frozen teacher; predictive variance and regression error flag anomalies.

13. **Wang, G., Han, S., Ding, E., Huang, D. (2021).** Student-Teacher Feature Pyramid Matching for Anomaly Detection (STFPM). *BMVC 2021*. arXiv: 2103.04257.
    - Multi-scale feature-pyramid distillation; anomaly score is the feature-difference at each level.

14. **Deng, H., Li, X. (2022).** Anomaly Detection via Reverse Distillation from One-Class Embedding (RD4AD). *CVPR 2022*. arXiv: 2201.10703.
    - Inverts the distillation direction: a decoder student reconstructs teacher features from a one-class bottleneck.

## Normalizing-flow methods

15. **Gudovskiy, D., Ishizaka, S., Kozuka, K. (2022).** CFLOW-AD: Real-Time Unsupervised Anomaly Detection with Localization via Conditional Normalizing Flows. *WACV 2022*. arXiv: 2107.12571.
    - Conditional normalizing flow over CNN features; real-time inference and pixel-level localization.

16. **Yu, J., Zheng, Y., Wang, X., Li, W., Wu, Y., Zhao, R., Wu, L. (2021).** FastFlow: Unsupervised Anomaly Detection and Localization via 2D Normalizing Flows. arXiv: 2111.07677.
    - 2D normalizing flow that works directly on feature maps; fast and effective on MVTec AD.

## Self-supervised / synthetic-anomaly methods

17. **Li, C.-L., Sohn, K., Yoon, J., Pfister, T. (2021).** CutPaste: Self-Supervised Learning for Anomaly Detection and Localization. *CVPR 2021*. arXiv: 2104.04015.
    - Self-supervised pretext: cut and paste random patches; learn features then fit one-class classifier.

18. **Zavrtanik, V., Kristan, M., Skocaj, D. (2021).** DRAEM - A Discriminatively Trained Reconstruction Embedding for Surface Anomaly Detection. *ICCV 2021*. arXiv: 2108.07610.
    - Joint reconstruction + discriminative segmentation network trained on simulated anomalies.

19. **Schlueter, H.M., Tan, J., Hou, B., Kainz, B. (2022).** Natural Synthetic Anomalies for Self-Supervised Anomaly Detection and Localization (NSA). *ECCV 2022*. arXiv: 2109.15222.
    - Poisson-image-editing-based synthetic anomalies that look more natural than CutPaste; strong MVTec results.

20. **Liu, Z., Zhou, Y., Xu, Y., Wang, Z. (2023).** SimpleNet: A Simple Network for Image Anomaly Detection and Localization. *CVPR 2023*, pp. 20402-20411. arXiv: 2303.15140.
    - Pretrained extractor + feature adapter + Gaussian-noise pseudo-anomalies + binary discriminator; 99.6% AUROC.

## One-class deep baselines

21. **Ruff, L., Vandermeulen, R.A., Goernitz, N., Deecke, L., Siddiqui, S.A., Binder, A., Mueller, E., Kloft, M. (2018).** Deep One-Class Classification (Deep SVDD). *ICML 2018*, PMLR 80:4393-4402.
    - First end-to-end deep SVDD: learn an embedding minimizing the volume of a hypersphere enclosing normals.

## Diffusion-based methods

22. **Mousakhan, A., Brox, T., Tayyub, J. (2023).** Anomaly Detection with Conditioned Denoising Diffusion Models (DDAD). arXiv: 2305.15956.
    - Conditioned denoising diffusion reconstructs normal counterparts; SOTA on MVTec (99.8%) and VisA (98.9%) AUROC.

23. **Zhang, H., Wang, Z., Wu, Z., Jiang, Y.-G. (2023).** DiffusionAD: Norm-guided One-step Denoising Diffusion for Anomaly Detection. arXiv: 2303.08730.
    - Reformulates reconstruction as noise-to-norm and uses one-step denoising for fast inference.

## Foundation-model / vision-language methods

24. **Jeong, J., Zou, Y., Kim, T., Zhang, D., Ravichandran, A., Dabeer, O. (2023).** WinCLIP: Zero-/Few-Shot Anomaly Classification and Segmentation. *CVPR 2023*. arXiv: 2303.14814.
    - Window-based CLIP scoring with compositional prompts; 91.8% zero-shot AUROC on MVTec-AD.

25. **Zhou, Q., Pang, G., Tian, Y., He, S., Chen, J. (2024).** AnomalyCLIP: Object-agnostic Prompt Learning for Zero-shot Anomaly Detection. *ICLR 2024*. arXiv: 2310.18961.
    - Learns object-agnostic prompts for normality/abnormality, validated across 17 AD datasets.

26. **Chen, X., Han, Y., Zhang, J. (2023).** APRIL-GAN: A Zero-/Few-Shot Anomaly Classification and Segmentation Method for CVPR 2023 VAND Workshop Challenge. *CVPRW 2023*. arXiv: 2305.17382.
    - 1st place zero-shot / 4th place few-shot at VAND 2023; CLIP with linear projection layers and feature memory bank.

## Efficient / real-time methods

27. **Batzner, K., Heckler, L., Koenig, R. (2024).** EfficientAD: Accurate Visual Anomaly Detection at Millisecond-Level Latencies. *WACV 2024*. arXiv: 2303.14535.
    - Lightweight student-teacher + autoencoder for global logical anomalies; 2 ms latency, 600 FPS, SOTA accuracy.

## Toolkits and surveys

28. **Akcay, S., Ameln, D., Vaidya, A., Lakshmanan, B., Ahuja, N., Genc, U. (2022).** Anomalib: A Deep Learning Library for Anomaly Detection. *ICIP 2022*. arXiv: 2202.08341.
    - OpenVINO-backed library implementing PaDiM, PatchCore, FastFlow, RD, STFPM, etc., with experiment trackers.

29. **Liu, J., Xie, G., Wang, J., Li, S., Wang, C., Zheng, F., Jin, Y. (2024).** Deep Industrial Image Anomaly Detection: A Survey. *Machine Intelligence Research*, 21(1), 104-135. arXiv: 2301.11514. DOI: 10.1007/s11633-023-1459-z.
    - Comprehensive taxonomy of architectures, supervision regimes, losses, metrics, datasets, and open challenges.

30. **Tao, X., Gong, X., Zhang, X., Yan, S., Adak, C. (2022).** Deep Learning for Unsupervised Anomaly Localization in Industrial Images: A Survey. *IEEE Transactions on Instrumentation and Measurement*, 71. arXiv: 2207.10298.
    - Reviews 120+ unsupervised AD localization works covering benchmarks and quantitative comparisons.
