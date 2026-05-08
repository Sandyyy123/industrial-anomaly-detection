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
