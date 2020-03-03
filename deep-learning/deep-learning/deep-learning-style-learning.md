# \(작성중\) Deep Learning: Style Learning

## 1. Introduction

Style transfer learning은 두 가지의 입력 이미지\(Content & Style\)가 주어지면, Content의 내용물\(형태\)은 최대한 유지하며 목표로 하는 Style을 적용시키는 방법이다. 쉽게 말해 아래 그림 같은 예를 들 수 있다.

![](../../.gitbook/assets/style-learning-01.png)

이렇게 학습하는 방법으로는 크게 2가지로 나뉠 수 있다.

1. Pre-trained 네트워크 모델을 이용하는 방법
   * Content 네트워크와 Style 네트워크의 feature map을 추출하여 새롭게 합성될 이미지의 feature map을 이들과 유사하게 학습하는 방법
   * 장점 : 이미지 2장\(Content & Style\)만으로 학습 가능
   * 단점 : 합성할 이미지마다 최적화가 필요하여 시간이 오래걸림
2. Style transfer 네트워크 모델을 이용하는 방법
   * 서로 다른 도메인\(A style, B style\)끼리 변환되는 네트워크를 학습
   * 장점 : 네트워크를 학습한 후 사용만 하면 됨
   * 단점 : 도메인 별로 학습을 해야 , 데이터가 많이 필요함

## 2. Methods

### 2.1. Image Style Transfer Using Convolutional Neural Networks

2016년 CVPR에서 발표된 논문으로 CNN을 이용하여 Style Transfer Learning을 성공적으로 수행하였다. 주요 포인트는 Pretrained VGG 19모델을 이용하여 Content와 Style 이미지 간의 차이를 줄여주는 방법을 End-to-End로 만들었다. 공식 코드 및 사람들이 작성한 코드를 기반으로 좀 더 분석하자면,

* Model : Pretrained VGG 19 \(Gradient update 없음\)
* Input Image
  * Content : Style을 적용하고자 하는 이미지 \(Gradient update 없음\)
  * Style : Content 이미지에 적용하고자 하는 Style을 갖는 이미지 \(Gradient update 없음\)
  * Target : 적용하고자 하는 Style을 적용한 Content 이미지
    * Random Noise, Content Image, Style Image 중 1개를 선택
    * Gradient update 있음 \(Content + Style Image로 변환이 진행되어야 하기 때문\)
  * Initialization : Content나 Style 이미지로 초기화하면, 항상 같은 Output만 나옴. 하지만, White noise로 초기화하면 매 번 새로운 이미지 생성. \(Output의 퀄리티는 거의 차이가 없음\)
* Gram Matrix : Style Representation Feature 추출을 위해 각 Layer마다 추출된 Feature끼리 gram matrix를 이용하여 correlation을 계산한다. 이렇게 얻어진 multi-layer 간 correlation은 stationary하고 multi-scale을 아우르는 feature가 된다.
* L-BFGS \(Limited-memory BFGS\) : Quasi-Newton 방법 중 하나로 복잡한 Hessian Matrix 연산이 들어가는 optimization에서 유용함.

### 2.2. GAN based Style Transfer Learning





## References

* [https://blog.lunit.io/2017/04/27/style-transfer/](https://blog.lunit.io/2017/04/27/style-transfer/)
* [https://www.popit.kr/neural-style-transfer-%EB%94%B0%EB%9D%BC%ED%95%98%EA%B8%B0/](https://www.popit.kr/neural-style-transfer-%EB%94%B0%EB%9D%BC%ED%95%98%EA%B8%B0/)
* [https://towardsdatascience.com/style-transfer-styling-images-with-convolutional-neural-networks-7d215b58f461](https://towardsdatascience.com/style-transfer-styling-images-with-convolutional-neural-networks-7d215b58f461)
* [https://datascience-enthusiast.com/DL/Art\_Generation\_with\_Neural\_Style\_Transfer\_v2.html](https://datascience-enthusiast.com/DL/Art_Generation_with_Neural_Style_Transfer_v2.html)
* [https://seongkyun.github.io/papers/2019/11/13/style\_transfer/](https://seongkyun.github.io/papers/2019/11/13/style_transfer/)
* [https://www.cv-foundation.org/openaccess/content\_cvpr\_2016/papers/Gatys\_Image\_Style\_Transfer\_CVPR\_2016\_paper.pdf](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf)
* [https://github.com/cysmith/neural-style-tf/blob/a2c374f9ee2938f0022e1e0b720f4eb28cf7d0a8/neural\_style.py\#L406](https://github.com/cysmith/neural-style-tf/blob/a2c374f9ee2938f0022e1e0b720f4eb28cf7d0a8/neural_style.py#L406)
* [https://github.com/leongatys/PytorchNeuralStyleTransfer/blob/master/NeuralStyleTransfer.ipynb](https://github.com/leongatys/PytorchNeuralStyleTransfer/blob/master/NeuralStyleTransfer.ipynb)
* [https://wikidocs.net/22155](https://wikidocs.net/22155)

