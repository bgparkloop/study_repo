---
description: Adversarial Gated Networks for Multi-Collection Style Transfer
---

# 작성중 \(2019\) Gated-GAN

## 1. Introduction

Gatys가 제안한 Neural style transfer learning처럼 content와 style 이미지를 사용하여 학습하는 GAN이다. 특이하게 다양한 style을 학습하기 위해 단일 GAN 내부 encoder와 decoder 사이 Transformer module이라는 것을 추가하여 gate를 열고 닫듯이 style을 정하여 학습 및 생성하도록 하였다. 논문의 주요 contribution은 다음과 같다.

* Gate module을 추가하여 단일 모델에서도 multi style learning이 가능하게 함
* Gate module을 이용하여 input과 output 사이에의 consistency를 없애 auto-encoder형태에서 탈피하여 mode collapse를 회피함
* Real/Fake의 기존 GAN부분과 Auxiliary classifier를 두어 overlaid-gradient problem 회피

주석\) mode collapse : random input이 다양한 변화를 주는 output을 생성하지 못해 GAN을 통해 생성한 output 이미지가 동일한 형태가 나오는 것을 의

## 2. Methods



## 3. Experimental Results & Conclusion
