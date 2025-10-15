# ZJUHDR-dataset

Eight HDR 10-bit video sequences were encoded with six different codecs, and over 4,800 quality judgments were collected on 178 compressed videos. Based on subjective scores, we evaluated five full-reference objective quality models (PSNR, VMAF, SSIM, ColorVideoVDP, and HDRMAX+VMAF). We observed inadequate generalization capability across codecs, with performance on learning-based codecs generally lower than that on traditional ones. Moreover, HDR metrics have not demonstrated significant advantages over the SDR metrics, highlighting the need for further research to advance HDR metric development.

We will make source videos, encoded sequences, subjective and objective scores available soon.

## Encoding Configuration

1) **AVS3 (HPM v15.7)**
   - **QP**: After testing rate points ranging from 20 to 56, four QP points (28, 32, 36, 44) were chosen.
   - Available to members of AVS working group.

2) **VVC (VTM v23.9)**
   - **Configuration**:
     - `cfg/per-class/classH1.cfg` and `cfg/encoder_randomaccess_vtm.cfg`
     - GOP size: 64
   - **QP**: Six initial rate points (QP = 22, 27, 32, 37, 42, 47), refined to four.
   - **url**: [https://vcgit.hhi.fraunhofer.de/jvet/VVCSoftware_VTM](https://vcgit.hhi.fraunhofer.de/jvet/VVCSoftware_VTM)

3) **LCEVC (LTM v7.0)**
   - **Base layer**:
     - **Configuration**:
       - VVC (VTM v23.9)
       - Down-sampling from 3840×2160 to 1920×1080.
     - **QP**: 11, 17, 23, 29, 32, 35, 38.
   - **Enhancement layer**:
     - **Configuration**:
       - Sublayer 1 step width (SW1): 32767.
       - Sublayer 2 step width (SW2): Computed based on the formula in [MPEG/m56330](https://dms.mpeg.expert/doc_end_user/current_document.php?id=78233&id_meeting=0) (Annex 2).
   - **url**: [https://git.mpeg.expert/MPEG/Video/LCEVC/LTM](https://git.mpeg.expert/MPEG/Video/LCEVC/LTM)

4) **AVS EEM (v6.1)**
   - **Configuration**: intra-period = -1 (only the first frame as I-frame, remaining as P-frames).
   - **QP**: As AVS EEM is a single-rate model, four separate models (QP = 0, 1, 2, 3) were used to generate four rate points per sequence.
   - **url**: [https://gitlab.com/xhsheng/avs-eem/-/tags/v5.2](https://gitlab.com/xhsheng/avs-eem/-/tags/v5.2)

5) **AlphaVC-P**
   - **Configuration**: intra-period = 60 (I-frame every 60 frames).
   - **QP**: Two multi-rate models, each targeting three rate points:
     - **High-rate model**: lambda = 0.025 (QP 0), 0.01 (QP 1), 0.005 (QP 2).
     - **Low-rate model**: lambda = 0.025 (QP 3), 0.005 (QP 4), 0.001 (QP 5).
   - **Private.**

6) **NNVC (VTM-based Neural Network Encoder)**
   - **Configuration**:
     - Random Access mode with configuration file `encoder_randomaccess_nnvc.cfg`.
     - HOP5 model: `--NnlfOption=4`, `--NnlfModelName=nnlf_hop5_model_int16.sadl`.
   - **QP**: Seven QP points (17, 22, 27, 32, 37, 42, 47) were encoded, with four retained for final evaluation.
   - **url**: [https://vcgit.hhi.fraunhofer.de/jvet-ahg-nnvc/VVCSoftware_VTM](https://vcgit.hhi.fraunhofer.de/jvet-ahg-nnvc/VVCSoftware_VTM)


The detailed Bitrate values of encoded sequences are shown in the below table.

![bitrate_values.png](https://github.com/blindwang/ZJUHDR-dataset/blob/main/bitrate_values.png)

## RD-Plot

We demonstrate the RD-Plots comparison on different codecs.

| ![Chimera2](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Chimera2_MOS_RD-plot.png) | ![Chimera3](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Chimera3_MOS_RD-plot.png) | ![Chimera4](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Chimera4_MOS_RD-plot.png) | ![Smithy1](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Smithy1_MOS_RD-plot.png) |
| --- | --- | --- | --- |
| ![Sparks2](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Sparks2_MOS_RD-plot.png) | ![Sparks3](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Sparks3_MOS_RD-plot.png) | ![Nocturne1](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Nocturne1_MOS_RD-plot.png) | ![Football1](https://github.com/blindwang/ZJUHDR-dataset/blob/main/RD-plot/Football1_MOS_RD-plot.png) |

