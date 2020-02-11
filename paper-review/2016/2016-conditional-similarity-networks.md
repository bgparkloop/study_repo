# \(2016\) Conditional Similarity Networks

## 1. Introduction

* Optimal 임베딩 벡터는 개념적으로 유사한 Object끼리의 거리 차이가 작은 것을 의미.
* 하지만, 기본 Triplet은 Semantic과 Categorical Similarity를 동시에 만족시킬 수 없음.
* Semantic한 부분을 나누기 위해 masking을 이용하여 sub category를 만듦.

### Contributions:

* 단일 임베딩 하나로 Semantic과 Categorical Similarity 동시 만족 가능.
* 어려운 Visual Task에서도 성공적임.
* 의미있는 분류 가능.\(예 - 빨간 구두, 파란 구두\)

![](../../.gitbook/assets/screenshot-from-2020-02-11-14-05-47.png)

## 2. Conditional Similarity Networks

![](../../.gitbook/assets/screenshot-from-2020-02-11-14-06-22.png)

이 논문에서 소개하는 전체 Architecture는 위와 같다. 기본적인 Embedding Extractor\(CNN\)이 있고, 이를 통해 추출된 Embedding vector를 세부 분류\(semantic\)에 따라 mask를 달리하여 원하는 형태의 clustering을 수행한다.

이 때, Mask는 고정되 있지 않으며 embedding vector와 함께 학습과정에서 점차 명확하게 정해진다. CSN\(Conditional Similarity Network\)의 Loss는 Triplet Loss\(T\)와 latent space에 대한 embedding Loss\(W\), 마지막으로 mask에 대한 Loss\(M\)의 합으로 결정된다.

$$
\mathcal{L}_{CSN} = \mathcal{L}_{T} + \lambda_{1}\mathcal{L}_{W} + \lambda_{2}\mathcal{L}_{M}
$$

ㅁㅁㅁㅁㅁㅁ

![](../../.gitbook/assets/screenshot-from-2020-02-11-14-06-44.png)

## 3. Experiments & Conclusion

asfasdf



