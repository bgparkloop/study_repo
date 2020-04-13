# \(2019\) Video Object Segmentation using Space-Time Memory Networks

## 1. Introduction

* Video object segmentation은 다음과 같은 방법들이 있음
  * 이전 frame만 참고 : 변화에 더 잘 적응하고, occlusion에도 강건함
  * first frame만 참고 : 위에 것과 반대
  * 이전 + first frame 참고 : 위 둘의 장점을 합침. 정확도 + 변화에 잘 적응
* 제안한 방법의 이점
  * 별도의 Memory에 각 frame에서의 foreground 정보를 저장하고 업데이트하여 사용
  * 참조 frame 수의 제한이 없어짐
  * non-local spatial pixel matching을 적용하여 더 정확한 segmentation 가능
  * 많은 frame을 참조 가능하여 occlusion, 형태 변화 등에 강

## 2. Methods

## 3. Results & Conclusion

## References

* aasd

