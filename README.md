# CNN-Based Single-Image Super-Resolution of Satellite Images
This repository contains the results for "A Comparative Study on CNN-Based Single-Image Super-Resolution Techniques for Satellite Images", my first bachelor's project. You can find the trained models in the **Releases** section of the repository. *I'll soon add the scripts for all the experiments. The experiments have been developed in separate private repositories, so it's gonna take some time to rearrange them and upload them here.* Check out this [english article]() or the [گزارش فارسی](https://drive.google.com/file/d/1n20s3Pb_dP0E-lA1Z8n9bMoC0Kt9ZTys/view?usp=sharing) for more details on the project, including a theory my instructor had for making a Mixture of Experts from the techniques, which unfortunately failed to produce any results.

## Compared Techniques
Based on their novelty and reported performances, we have chosen the following techniques for this study, sorted by their earliest draft publication date:

+ Zhang et al., Residual Dense Network (RDN) ([repo](https://github.com/yjn870/RDN-pytorch))
+ Zhang et al., Residual Channel Attention Network (RCAN) ([repo](https://github.com/yulunzhang/RCAN))
+ Li et al., Feedback Network for Image Super-Resolution (SRFBN) ([repo](https://github.com/Paper99/SRFBN_CVPR19))
+ Anwar & Barnes, Densly Residual Laplacian Network (DRLN) ([repo](https://github.com/saeed-anwar/DRLN))
+ Li et al., Gated Multiple Feedback Network (GMFN) ([repo](https://github.com/liqilei/GMFN))
+ Mei et al., Cross-Scale Non-Local Network (CSNLN) ([repo](https://github.com/SHI-Labs/Cross-Scale-Non-Local-Attention))

## Performance Evaluation
Training and evaluation of the techniques has been done on a Tesla P100 GPU, using the PyTorch library, while the bicubic interpolation algorithm has been run on a Core i7-9500H CPU, with the tools provided by the Scikit-Image library. The results for the models marked with an * have been directly lifted from our [baseline article](https://ieeexplore.ieee.org/abstract/document/8677274).

| Scale | Model                   | PSNR      | SSIM      | Weights<br>(Millions) | Training Time<br>(Hours) | Inference Time<br>(Seconds) |
|-------|-------------------------|-----------|-----------|-----------------------|--------------------------|-----------------------------|
| 2     | Bi-cubic Interpolation* | 34.01     |     0.938 | 0                     | 0                        | 0.5                         |
|       | SRCNN*                  | 36.79     |     0.960 | -                     | -                        | -                           |
|       | VDSR*                   | 37.94     |     0.967 | -                     | -                        | -                           |
|       | SRGAN*                  | 37.69     |     0.963 | -                     | -                        | -                           |
|       | EEGAN*                  | 38.82     |     0.973 | -                     | -                        | -                           |
|       | CSNLN                   | **39.87** | **0.976** | 3.06                  | 112                      | 104                         |
|       | DRLN                    | **39.87** | **0.976** | 34.43                 | 5                        | 7.5                         |
|       | GMFN                    | 39.49     | 0.974     | 9.75                  | 13                       | **3**                       |
|       | RCAN                    | 39.83     | **0.976** | 15.44                 | 11                       | 19.5                        |
|       | RDN                     | 39.75     | **0.976** | 22.12                 | **1.5**                  | **3**                       |
|       | SRFBN                   | 39.49     | 0.974     | **2.14**              | 10.5                     | 5                           |
| 3     | Bi-cubic Interpolation* | 30.52     | 0.870     | 0                     | 0                        | 0.5                         |
|       | SRCNN*                  | 32.44     | 0.906     | -                     | -                        | -                           |
|       | VDSR*                   | 33.69     | 0.924     | -                     | -                        | -                           |
|       | SRGAN*                  | 33.70     | 0.919     | -                     | -                        | -                           |
|       | EEGAN*                  | 34.84     | **0.936** | -                     | -                        | -                           |
|       | CSNLN                   | **35.39** | **0.936** | 6.01                  | 57                       | 53                          |
|       | DRLN                    | 35.22     | 0.932     | 34.61                 | 3                        | 7                           |
|       | GMFN                    | 35.26     | 0.932     | 9.80                  | 11                       | **1**                       |
|       | RCAN                    | 35.24     | 0.932     | 15.63                 | 6.5                      | 14                          |
|       | RDN                     | 35.19     | 0.933     | 22.31                 | **1.5**                  | 2.5                         |
|       | SRFBN                   | 35.18     | 0.931     | **2.83**              | 9                        | 2.5                         |
| 4     | Bi-cubic Interpolation* | 28.54     | 0.808     | 0                     | 0                        | 0.5                         |
|       | SRCNN*                  | 30.06     | 0.848     | -                     | -                        | -                           |
|       | VDSR*                   | 31.06     | 0.874     | -                     | -                        | -                           |
|       | SRGAN*                  | 31.17     | 0.882     | -                     | -                        | -                           |
|       | EEGAN*                  | 32.36     | **0.898** | -                     | -                        | -                           |
|       | CSNLN                   | 32.84     | 0.885     | 6.57                  | 107                      | 182                         |
|       | DRLN                    | 32.87     | 0.885     | 34.58                 | 2.68                     | 6.5                         |
|       | GMFN                    | **32.96** | 0.887     | 9.86                  | 10                       | **0.5**                     |
|       | RCAN                    | 32.90     | 0.886     | 15.59                 | 3.5                      | 12                          |
|       | RDN                     | 32.89     | 0.887     | 22.27                 | **1.5**                  | 2                           |
|       | SRFBN                   | 32.82     | 0.884     | **3.63**              | 10                       | 2                           |

# Visual Comparison
The following shows a single image, being down-scaled and then reconstructed, first using the Bicubic interpolation, and
then using the trained SISR models.

![Image Reconstruction](figures/samples.png)
 