# \(2019\) Unsupervised Deep Learning by Neighbourhood Discovery

## 1. Introduction

* clustering과 sample specificity learning의 장점을 합치고 단점은 완화시킨 방식을 제안함
* divide-conquer방식의 알고리즘 제안
  * 개별적인 학습 샘플들에 anchored한 인접 샘플들\(divide\)
  * divide 과정에서 구성된 neighbourhood 내에서 sample 간 관계를 전파함\(conquer\)
  * 각 neighbourhood는 하나의 sample단위로 취급될 수 있음\(class 일치도, 밀집도\)

### contributions

* local neighbourhood를 이용한 unsupervised clustering end-to-end deep learning 학습법 제안
* Anchor Neighbourhood Discovery\(AND\) approach 제안
* curriculum learning algorithm 제

## 2. Methods

### 2.1. Neighbourhood Discovery

$$
\mathcal{N}_k(x) = \{x_i | s(x_i,x)\,is\,top-k\,in\,X\} \cup \{x\}
$$

* similarity metric s \(ex- cosine similarity\)
* k-nearest neighbours로 Anchor Neighbourhood를 생성함

## 3. Results & Conclusion

## References

* [https://arxiv.org/abs/1904.11567](https://arxiv.org/abs/1904.11567)

