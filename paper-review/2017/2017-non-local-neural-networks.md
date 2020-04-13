# \(2017\) Non-local Neural Networks

## 1. Introduction

* CNN, RNN에서 long-range dependency에서 local operation 사용
* image에서는 long-range dependency를 위해 receptive field를 넓게 잡도록 pooling등의 연산 필요
* local operation의 단점
  * long-range dependency 전파가 힘듦
  * 연산량이 많아지고, 최적화가 힘듦
* 제안한 방법의 이점
  * 어떤 두 지점 사이의 위치적 거리를 고려하지 않고 상호작용을 직접적으로 계산
  * 제안한 방법의 layer를 추가하면 적은 parameter 추가로도 큰 성능 상승을 보임

## 2. Methods

## 3. Results & Conclusion

## References

* [https://arxiv.org/abs/1711.07971](https://arxiv.org/abs/1711.07971)
* [https://blog.lunit.io/2018/01/19/non-local-neural-networks/](https://blog.lunit.io/2018/01/19/non-local-neural-networks/)
* [https://github.com/facebookresearch/video-nonlocal-net](https://github.com/facebookresearch/video-nonlocal-net)

