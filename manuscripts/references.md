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


---

## 2024-2026 additions (post-QA literature scout)

# Additional References - Industrial Anomaly Detection (MVTec AD)

Independent literature scan run on 2026-05-08 against CrossRef live API
(`https://api.crossref.org/works/{doi}`). Every entry below resolved with HTTP 200
and a title match at the time of the scan. Entries are grouped by sub-topic and
prioritise 2024-2026 work that is NOT already covered in
`manuscripts/references.md`. Format per QA rules: Authors. Title. Journal. Year.
DOI. No volume/issue/page numbers.

## State-of-the-art callout - gaps the current `references.md` does NOT cover

After completing the independent search above, a peek at the existing
`manuscripts/references.md` (final SOTA-gap check only, per QA rules) confirms
five concrete gaps that this project SHOULD cite given its scope:

1. **MVTec AD 2 dataset (Heckler-Kram et al. 2026, IJCV).** The direct successor
   to MVTec AD with harder defect types and the new evaluation protocol; any
   PaDiM-lite paper benchmarked on MVTec AD in 2026 needs to acknowledge the
   refreshed benchmark. DOI: 10.1007/s11263-026-02743-0.
2. **IM-IAD benchmark (Xie et al. 2024, IEEE TCyber).** Standardised manufacturing
   anomaly-detection benchmark and protocol. Closes the "is the leaderboard
   number reproducible" gap that the manuscript flags in Section 5. DOI:
   10.1109/TCYB.2024.3357213.
3. **MVTec LOCO logical-anomaly literature (SALAD, LogicAL, PyramidCore).** The
   manuscript only addresses structural defects on MVTec AD; logical anomalies
   (missing component, wrong count) are the harder regime and have their own
   sub-literature that the cable-category failure mode in Section 5 directly
   touches.
4. **2025-2026 zero-shot CLIP successors (AA-CLIP, AF-CLIP, FE-CLIP, GA-CLIP).**
   The current refs cite WinCLIP and AnomalyCLIP (both 2023-2024) but miss the
   2025-2026 wave, which now sits at the top of the zero-shot leaderboard and is
   directly relevant to "deploy without target-factory data" Mittelstand pitch.
5. **3D point-cloud / multimodal track (DAUP, MAESTRO).** The brief explicitly
   names MVTec ITODD (3D), but the current refs include no 3D AD paper. The
   project document leaves this thread dangling.

A sixth gap, the AUPIMO metric named in the brief, is currently arXiv-only and
does not yet resolve via CrossRef, so it is omitted per the "verify or omit"
rule.

## Architectures (2024-2026)

Zhao Y. LogicAL: Towards logical anomaly synthesis for unsupervised anomaly
localization. 2024 IEEE/CVF Conference on Computer Vision and Pattern
Recognition Workshops (CVPRW). 2024. DOI: 10.1109/CVPRW63382.2024.00406

Fucka M, Zavrtanik V, Skocaj D. SALAD - Semantics-Aware Logical Anomaly
Detection. 2025 IEEE/CVF International Conference on Computer Vision (ICCV).
2025. DOI: 10.1109/ICCV51701.2025.02028

Fucka M, Zavrtanik V, Skocaj D. PyramidCore - Feature Pyramids for Few-Shot
Logical Anomaly Detection. 2026 IEEE 23rd Mediterranean Electrotechnical
Conference (MELECON). 2026. DOI: 10.1109/MELECON64486.2026.11418871

Kamiya S, Yamashita K, Hotta K. ASO PatchCore: Memory-Efficient and Fast
Anomaly Detection via Automatic Sampling Optimization. Proceedings of the 21st
International Conference on Computer Vision Theory and Applications. 2026.
DOI: 10.5220/0014445100004084

Lardon L, Guis VH, Busvelle E. Anomaly Detection Using a Lite PatchCore for
Mobile Robotic Industrial Application. Proceedings of the 21st International
Conference on Computer Vision Theory and Applications. 2026. DOI:
10.5220/0014253200004084

Yang B, Zhang Z, Ma J. Co-Progression Knowledge Distillation with Knowledge
Prototype for Industrial Anomaly Detection. Proceedings of the AAAI Conference
on Artificial Intelligence. 2025. DOI: 10.1609/aaai.v39i12.33419

Xu J, Jiang S. Hierarchical Knowledge Transfer: Cross-Layer Distillation for
Industrial Anomaly Detection. Journal of Imaging. 2025. DOI:
10.3390/jimaging11040102

Sun X, Pan W, Qin J, Lang Y, Qian Y. Unsupervised industry anomaly detection
via asymmetric reverse distillation. Computers and Electrical Engineering.
2024. DOI: 10.1016/j.compeleceng.2024.109759

Fu M, Fu Z. A unified multi-class anomaly detection model based on reverse
distillation. IET Image Processing. 2025. DOI: 10.1049/ipr2.13309

Tan P, Wong WK. Unsupervised anomaly detection and localization with one model
for all category. Knowledge-Based Systems. 2024. DOI:
10.1016/j.knosys.2024.111533

Kruse M, Rosenhahn B. Multi-Flow: Multi-View-Enriched Normalizing Flows for
Industrial Anomaly Detection. 2025 IEEE/CVF Conference on Computer Vision and
Pattern Recognition Workshops (CVPRW). 2025. DOI:
10.1109/CVPRW67362.2025.00378

Shi J, Wen X, Guo S, Deng H, Xie J, Cao R. Multi-Level Normalizing Flow for
Comprehensive Anomaly Detection and Localization. 2025 IEEE International
Conference on Multimedia and Expo (ICME). 2025. DOI:
10.1109/ICME59968.2025.11209960

Kumar K, Chakraborty S, Mahapatra D, Bozorgtabar B, Roy S. Self-Supervised
Anomaly Segmentation via Diffusion Models with Dynamic Transformer UNet. 2025
IEEE/CVF Winter Conference on Applications of Computer Vision (WACV). 2025.
DOI: 10.1109/WACV61041.2025.00770

## Datasets and benchmarks

Wang C, Zhu W, Gao B, Gan Z, Zhang J, Gu Z. Real-IAD: A Real-World Multi-View
Dataset for Benchmarking Versatile Industrial Anomaly Detection. 2024 IEEE/CVF
Conference on Computer Vision and Pattern Recognition (CVPR). 2024. DOI:
10.1109/CVPR52733.2024.02159

Heckler-Kram L, Neudeck J, Scheler U, Koenig R, Steger C. The MVTec AD 2
Dataset: Advanced Scenarios for Unsupervised Anomaly Detection. International
Journal of Computer Vision. 2026. DOI: 10.1007/s11263-026-02743-0

Xie G, Wang J, Liu J, Lyu J, Liu Y, Wang C. IM-IAD: Industrial Image Anomaly
Detection Benchmark in Manufacturing. IEEE Transactions on Cybernetics. 2024.
DOI: 10.1109/TCYB.2024.3357213

## Foundation models / zero-shot / few-shot

Ma W, Zhang X, Yao Q, Tang F, Wu C, Li Y. AA-CLIP: Enhancing Zero-Shot Anomaly
Detection via Anomaly-Aware CLIP. 2025 IEEE/CVF Conference on Computer Vision
and Pattern Recognition (CVPR). 2025. DOI: 10.1109/CVPR52734.2025.00447

Fang Q, Lv W, Su Q. AF-CLIP: Zero-Shot Anomaly Detection via Anomaly-Focused
CLIP Adaptation. Proceedings of the 33rd ACM International Conference on
Multimedia. 2025. DOI: 10.1145/3746027.3755635

Gong T, Chu Q, Liu B, Zhou W, Yu N. FE-CLIP: Frequency Enhanced CLIP Model for
Zero-Shot Anomaly Detection and Segmentation. 2025 IEEE/CVF International
Conference on Computer Vision (ICCV). 2025. DOI: 10.1109/ICCV51701.2025.01971

Guo W, Wan Y, Yuan S, Chang L, Wu Y, Dou Z. GA-CLIP: Dual-branch CLIP for
generalizable and anomaly-aware zero-shot anomaly detection. Knowledge-Based
Systems. 2026. DOI: 10.1016/j.knosys.2026.116078

Wan Y, Lang Y, Yao L. DCS: A Zero-Shot Anomaly Detection Framework with
DINO-CLIP-SAM Integration. Applied Sciences. 2026. DOI: 10.3390/app16041836

Fan Y, Liu J, Chen X, Gao B, Li J, Liu Y. Towards fine-grained vision-language
alignment for few-shot anomaly detection. Pattern Recognition. 2026. DOI:
10.1016/j.patcog.2026.113316

Liu S, Koch D, Kaiser J, Stamer F. Automating Industrial Quality Assurance: A
Zero-Shot MLLM Framework for Defect Detection and 3R. Procedia CIRP. 2026.
DOI: 10.1016/j.procir.2025.09.037

## Domain applications and 3D anomaly detection

Li H, Niu Y, Yin H, Mo Y, Liu Y, Huang B. DAUP: Enhancing point cloud
homogeneity for 3D industrial anomaly detection via density-aware point cloud
upsampling. Advanced Engineering Informatics. 2024. DOI:
10.1016/j.aei.2024.102823

Lhoste R, Vacavant A, Delhay D. MAESTRO: A Full Point Cloud Approach for 3D
Anomaly Detection Based on Reconstruction. Proceedings of the 20th
International Joint Conference on Computer Vision, Imaging and Computer
Graphics Theory and Applications. 2025. DOI: 10.5220/0013250500003912

Kozamernik N, Bracun D. A novel FuseDecode Autoencoder for industrial visual
inspection: Incremental anomaly detection improvement with gradual transition
from unsupervised to mixed-supervision learning with reduced human effort.
Computers in Industry. 2025. DOI: 10.1016/j.compind.2024.104198

Facoco I, Carvalho R, Rosado L. Towards efficient wafer visual inspection:
Exploring novel lightweight approaches for anomaly detection and defect
segmentation. Intelligent Systems with Applications. 2025. DOI:
10.1016/j.iswa.2025.200576

Zhang X, Jing J, Wang Y. PFADet: A few-shot prompt-guided fabric anomaly
detection network using Large Vision-Language Models. Applied Soft Computing.
2026. DOI: 10.1016/j.asoc.2025.114005

Yapp EK, Doan NC. Anomaly detection on MVTec AD using VQ-VAE-2. Procedia
CIRP. 2024. DOI: 10.1016/j.procir.2024.10.320

Kumari S, Prabha C. Anomaly Detection Utilizing PatchCore for Reimagining
Industrial Visual Inspection. Artificial Intelligence and Applications. 2025.
DOI: 10.47852/bonviewaia52026321

