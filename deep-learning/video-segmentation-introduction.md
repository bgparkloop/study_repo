# \(작성중\) Video Segmentation Introduction

https://www.youtube.com/watch?v=0VH1Lim8gL8

### Video Segmentation <a id="video-segmentation"></a>

Model 종류

* FCN
* U-Net
* 3D Segmentation Model
* RNN + Segmentation Model \(Sequence Video Segmentation\)

#### 3D Semantic Segmentation <a id="3d-semantic-segmentation"></a>

1. An Efficient 3D CNN for Action/Object Segmentation on Video
   * Unsupervised Learning
   * Use 3D Seperable convolution\(channel-wise\(known as depth-wise\) + point-wise\)
   * R\(2+1\)D Conv\(Spatial + Temporal\) : A Closer Look at Spatiotemporal Convolutions for Action Recognition [ref site](https://blog.airlab.re.kr/2019/09/R%282+1%29D)

Primary Metrics :

* IoU\(Intersection over Union\) or Jaccard Index
* F-measure\(Contour Accuracy\)

