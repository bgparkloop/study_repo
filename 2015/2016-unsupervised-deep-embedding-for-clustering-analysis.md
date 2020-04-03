# \(작성중\) \(2015\) Unsupervised Deep Embedding for Clustering Analysis

## 1. Introduction

* Data analysis와 Visualization에서 Clustering은 핵심적인 기술임
* Clustering algorithm에서 distance와 dissimilarity는 중요
  * Distance는 Data -&gt; Feature space로 표현하는데 중요함
  * Distance를 정의하기 위한 dissimilarity를 측정하는 것도 중요함

### Contributions

* Soft cluster assignment로부터 auxiliary target distribution으로 iteratively하게 clustering을 optimization
* Hyperparameter 선택에 sensitive하지 않음
* Clustering + Feature representation 동시 학습 진

## 2. Methods

* Raw data X에서 feature space Z로 embedding. \(이 때, 차원의 저주를 피하기 위해 훨씬 작은 dimension을 갖음\)
* 전체적인 Algorithm Flow
  * Autoencoder 모델로 feature space Z를 추출하고
  * K개의 cluster에 대해 auxiliary target distribution 사이의 Kullback-Leibler divergence를 최소화시키는 방향으로 parameter update

### 2.1. Soft Assignment

* Raw data X에 대해 embedding Z\_i를 추출하고 Centroid U\_i와 비교하여 i번째 clustering에 속할 확률을 계산함
* 자유도 알파 값은 별도의 cross-validation을 진행하지 않으므로 1로 설

$$
q_{ij} = \frac{ {( 1 + {|| z_i - \mu_j ||}^2 / \alpha )}^{-\frac{\alpha + 1}{2}} }{ \sum_{j'}{( 1 + {|| z_i - \mu_{j'} ||}^2 / \alpha )}^{-\frac{\alpha + 1}{2}} }
$$

### 2.2. KL Divergence minimization

* Soft assignment q와 auxiliary distribution p와의 KL을 계산함
* P의 선택이 제안한 논문의 알고리즘 성능에 중요한 역할을 담당함
  * 단순하게는 confidence threshold로 그 이상의 값들만 취하여 만드는 법이 있음
  * 하지만 soft assignment를 이용하고 있으므로 확률값인 p도 인위적인 값이 더 자연스러운 방법이기 때문에 이를 채택함
* 타겟 분포 P는 이러한 특징을 갖기를 원함
  * 예측 강화
  * high confidence를 갖는 data 강조
  * cluster size로 loss 값의 정규화. cluster 크기에 따른 feature space에 기여하는 정도를 최소

$$
L=KL(P||Q) = \sum_i \sum_j p_{ij} log{\frac{ p_{ij} }{ q_{ij} }}
$$

$$
p_{ij} = \frac{  q_{ij}^2 / f_{j}  }{  \sum_{j'} q_{ij'}^2 / f_{j'}  }, f_{j}=\sum_i q_{ij}
$$

### 2.3. Optimization

* asdf

### 2.4. Parameter Initialization

* asdadsa

## 3. Results & Conclusion

## References

* [https://leedakyeong.tistory.com/entry/%EB%85%BC%EB%AC%B8Unsupervised-Deep-Embedding-for-Clustering-AnalysisDEC](https://leedakyeong.tistory.com/entry/%EB%85%BC%EB%AC%B8Unsupervised-Deep-Embedding-for-Clustering-AnalysisDEC)
* [https://arxiv.org/pdf/1511.06335.pdf](https://arxiv.org/pdf/1511.06335.pdf)



