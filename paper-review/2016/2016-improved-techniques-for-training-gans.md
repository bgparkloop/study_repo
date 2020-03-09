# 작성중 \(2016\) Improved Techniques for Training GANs

## 1. Introduction

GAN은 Nash equilibrium\(내쉬 평형\)에 근거 게임이론에 의해 생성자와 분류자가 서로 최대의 이득을 얻기 위해 경쟁한다. 해당 논문에서는 이 과정에서 학습의 수렴이 매우 어렵게 되는데, 이를 해결하기 위한 여러 시도 중 유의미하였던 것들에 대해 소개한다.

* 내쉬 평형 : 상대방이 전략을 유지한다는 전제하에 자신도 현재 전략을 바꿀 이유가 없는 상태. 즉, 경쟁자의 대응에 따라 최선의 선택을 하면 서로가 자신의 선택을 바꾸지 않는 균형을 유지하는 상태를 말함.

## 2. Methods

### 2.1. Feature matching

기본적인 GAN의 Loss는 discriminator가 얼마나 잘 분류하냐로 정의되는데, 관점을 바꾸어 generator가 얼마나 real data에 유사한 분포를 학습할 수 있게 하는지를 loss로 바라보게 한다. 아래와 같이 수식이 변형된다.

$$
|| {f(x) - f(G(z))} ||
$$

여기서 f\(x\)는 real data x에 대한 판별함수이며, G는 input z에 대한 generator 모델링이다. 위와 같이 generator에 대한 새로운 loss 함수를 생성하는 데이터를 판별하는 것과 real data에 대한 판별하는 것의 차이로 정의하면, generator의 학습 방향이 real data의 분포의 모양으로 진행된다. 이렇게 loss 함수에 변형을 주는 것은 기존 GAN의 불안정한 학습에 대해 경험적으로 좀 더 나은 결과를 보여준다.

### 2.2. Minibatch discrimination

ㅁㅁㄴㅇㅁㄴㅇ

### 2.3. Historical averaging

asdasdasda

### 2.4. One-sided label smoothing

asfasdfasf

### 2.5. Virtual batch normalization

asdfasfdasdf



## 3. Experiment & Analysis

## References

* [https://arxiv.org/pdf/1606.03498.pdf](https://arxiv.org/pdf/1606.03498.pdf)

