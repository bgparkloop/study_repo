# Medical Data

## Introduction

의료 분야에서의 데이터들에 대해 간단한 소개 및 특징, AI 학습 시 어떤점을 고려해야 하는지에 대해 요약하는 문서입니다.

의료데이터의 경우 다른 데이터들보다 해당 분야에 대한 전문적인 지식이 많이 필요하다. 예를 들면 Chest X-ray와 같은 데이터가 있다면 그냥 봐서는 어디가 병인지도 모르는게 일반적이다. 알아도 비슷한 다른 이미지를 주면 알기가 어렵다. 그만큼 이를 제공해주는 전문가\(의사\)와의 의사소통이 많이 필요하며 개인적으로도 많은 공부가 필요한 분야이다. 전문가분들에게 학습에 필요한 정확한 Annotation 정보를 얻기 위해서는 그만큼 공부가 필요하기 때문이다.

## Chest X-ray

### 데이터 소개

Pathology, Fundus와 같이 가장 쉽게 접근 가능한 의료 데이터라고 볼 수 있다. 목부터 치골정도까지의 범위를 X-ray 촬영한 이미지를 가리키며 해당 이미지에서도 다양한 질병을 관측 가능하다.

![](../.gitbook/assets/cxr.jpg)

Chest X-ray\(이하 CXR\)은 grayscale의 밝기 분포만으로 이루어진 영상이므로, 질병에 따른 위치, Texture와 Shape이 주된 특징이라고 볼 수 있다. 전통적인 방식으로는 GLCM\(Gray Level Co-occurance Matrix\)를 이용한 다양한 Texture, Shape feature를 추출하여 SVM과 같은 ML 기법을 사용한다.

### Augmentation 방법

Deep Learning을 이용한 학습법으로는 다양한 방식이 있겠지만, 일반적으로 아래와 같은 Augmentation을 주로 사용하여 학습을 진행한다. 하지만 가장 중요한 것은 Task에 따른 Annotation의 Quality가 가장 중요하다고 볼 수 있겠다.

* Rotation \(사람마다 촬영할 때 항상 똑바로 서있지 않다.\)
* Horizontal / Vertical Flip \(좌우 반대나 이미지 자체 상하 반대가 있다\)
* Brightness/Contrast Adjustment \(희미한 Feature를 강조하기 위해\)
* CLAHE \(Histogram Equalization 방법 중 하나로 CXR에서 굉장히 효과적임\)
* Elastic Deformation \(CXR 이미지를 다양한 방식으로 Morphological 부분을 변형시켜 효율적인 학습이 가능하게 함\)

### 어려운 점

CXR은 쉽게 구하기 쉬운 이미지지만, public dataset은 정말 Quality가 좋지 않다. AI 학습을 위해 다양한 시도를 경험하면서 다음과 같은 문제들이 있었다.

* Label과 이미지가 맞지 않음
* 나이가 너무 많거나 어려서 CXR 촬영이 제대로 이루어지지 않음
* 병이 너무 심해서 병원에서 촬영하는 일반적인 CXR이 아닌 Portable 기기를 이용한 촬영인 경우
* Annotation의 부재 \(정확한 Annotation을 받기가 어렵다\)
* 정면 사진이라면서 옆모습이 있음 \(이것도 Label 문제라고 볼 수 있을듯하다\)
* 이미지 자체가 분간이 어려움 \(최소 3분의 1에서 절반 가량이 그냥 회색이거나 회색이 진하게 겹쳐있음\)

이러한 데이터 구성 문제도 그렇고 일반적으로 알려진 14 disease라고 불리는 것들 중 증상과 병명이 섞여 있어 이를 이미지에서 분간하기 쉽지 않다. \(증상들이 여러개 존재해야 병명을 붙이는 것이기 때문\)

이러한 저 Quality 데이터에도 불구하고 다양한 테크닉으로 성능을 끌어올릴 수는 있지만 만족할만한 성과를 얻기는 어렵다. 결국 Data Cleaning과 정확한 Annotation이 필수불가결하다.

## CT

### 데이터 소개

### Augmentation 방법

### 어려운 점

## MRI

### 데이터 소개

### Augmentation 방법

### 어려운 점

## Fundus

### 데이터 소개

카메라를 통해 눈을 촬영한 이미지를 갖고 진단하는 것으로 일반적으로 녹내장, 당뇨병성 망막증 등을 진단하기 위해 사용한다. CXR과 더불어 Public dataset이 굉장히 많으며 접근성이 좋다. 하지만, CXR과 마찬가지로 Public dataset의 상태는 그리 좋지 않다. \(그래도 CXR보다는 좋다\)

![](../.gitbook/assets/typical-fundus-images-at-the-different-stages-of-dr-a-normal-b-mild-npdr-c.png)

위 그림과 같이 눈을 굉장히 근접해서 촬영하며 홍채, 동공, 혈관 등이 자세하게 보인다. 여기서 혈관의 변이성이나 특정 부위의 변형 등을 찾아내어 진단하게 된다.

### Augmentation 방법

Color가 거의 붉은색 계열로 비슷하며 촬영된 모양도 거의 유사하기 때문에 Rotation이나 Hue 등을 조절할 필요가 적어진다.

* Brightness/Contrast Adjustment \(안저 이미지 특성 상 환자가 눈을 어디까지 가까이하냐에 따라 밝기가 많이 차이난다\)
* Horizontal / Vertical Flip
* 
### 어려운 점



## Pathology

### 데이터 소개

### Augmentation 방법

### 어려운 점

## IVUS

### 데이터 소개

IntraVascular UltraSound의 약자로 혈관 내를 초음파를 이용하여 촬영하는 방법이다. 소형화된 초음파 프로브와 함께 특별 제작된 Catheta를 이용하여 혈관 내의 병변을 찾아낸다.

![](../.gitbook/assets/intravascular.png)

위 그림처럼 이미지가 구성되며, 일반적으로 EEM\(External Elastic Membrane\)이라 불리우는 Vessel 영역과 실제 혈류가 지나가는 Lumen, 그리고 병변 부위인 Thrombus\(혈전\)을 검출하는 것이 주 목적이다.

초음파 데이터 특성상 Grayscale 이미지로 특징을 분별하는데 Color가 개입이 없기 때문에 Texture와 Shape의 영향이 가장 크다. 특히, IVUS의 경우 중심을 기준으로 일정 영역 크기안에서만 data가 발생되기 때문에 이것을 기준삼아 다양한 처리를 가해주는 것이 좋다.

### Augmentation 방법

실제 IVUS Segmentation을 Deep Learning으로 진행하면서 유의미한 효과를 보았던 Augmenation 방법들은 다음과 같다.

* Rotation 90도 단위
* Horizontal / Vertical Flip
* Brightness, Contrast Adjustment

### 어려운 점

이 외에도 효과적인 방법이 있겠지만, 사실 Annotation만 제대로 되어있다면 위에 언급된 3가지를 분류하기에는 큰 지장이 없다고 볼 수 있다. Shadow와 같이 영역 자체를 가리는 것이 아니라면 데이터 양과 Annotation의 Quality에 따라 성능이 정해진다고 볼 수 있겠다.

실제로 IVUS data를 통해 학습을 진행하기 위해 data를 얻는 것이 쉽지 않다. 필요한만큼 Annotation이 자유로운 마땅한 도구가 없기 때문에 병원에서 일반적으로 사용하고 있는 오래된 Tool을 이용해서 Vessel, Lumen이나 내부 혈전 등이나 가능하고 나머지는 수작업으로 다른 프로그램에서 진행해야 한다. 특히, Video 데이터이기 때문에 이를 Frame마다 annotation해야해서 매우 고역이다. \(이 말은 그만큼 데이터 획득에 시간이 오래 걸린다는 것을 의미\)

## Cytology

### 데이터 소개

Pathology에서는 전반적인 형태를 보고 진단을 하지만, Cytology는 세포 단위로 그에 맞는 진단을 내린다. 세포학에 해당하는 분야는 굉장히 많겠지만 예를 들어 Pap Test라 불리우는 자궁경부암에서의 세포진 검사를 예로 들면 다음과 같다.

![](../.gitbook/assets/screenshot-from-2020-02-28-15-55-31.png)

왼쪽은 Conventional 방식의 슬라이드에서 촬영된 이미지이고, 오른쪽은 Liquid 방식의 슬라이드에서 촬영된 이미지이다. Conventional의 경우 세포를 채취하여 슬라이드에 평평하게 바르는 작업을 거치기 때문에 세포 사이의 위상차가 생겨 Focus를 어떻게 맞추냐에 따라 슬라이드 이미지가 굉장히 달라지게 된다. 반면, Liquid 방식은 특수한 용액을 통해 자연스럽게 모여 보기 편한 상태로 퍼지기 때문에 Conventional과 비교하여 굉장히 깔끔한 이미지를 얻을 수 있다.

Cytology 이미지들은 Pathology와 마찬가지로 염색시약이 사용되기 때문에 컬러가 다양하다. 일반적으로 병리\(의\)사들은 세포질과 세포핵을 동시에 보고 판별하지만, AI가 경계가 모호한 세포질까지 판단하기는 어렵다고 본다. 세포학 분야에서의 Task로는 Detection과 Segmentation이 주가 되므로 이에 대한 Annotation이 필요하다.

### Augmentation 방법

염색시약에 종속적인 데이터가 나오므로 이를 고려하는 전처리/Augmentation들이 필요하다고 생각한다.

* Rotation
* Horizontal / Vertical Flip
* Gaussian Blur \(Focus가 맞춰진 정도나 Noise 제거용\)
* Elastic Deformation \(의료 분야에서 다양하게 사용되는 변환방법, 위치별로 affine 변환이 이루어지기 때문에 자연스러운 변화를 줄 수 있음\)
* Hue/Saturation Adjustment
* Brightness/Contrast Adjustment
* Scale \(세포 크기가 다양하기 때문에 Multi scale에 robust하도록\)

위와 같은 다양한 처리 방식이 들어갈 수 있지만, 모든 데이터가 그렇듯이 항상 잘되는 것은 아니다. 데이터에 맞춘 사용법이 필요하다. Pap test의 AI detection 학습 시, Hue/Saturation보다는 Brightness/Contrast가 더 효과적이었으며 Scale도 나름 효과적이었다.

### 어려운 점

세포학 이미지 학습에서 어려운 점은 Pap test를 예로 들면 Conventional 방식과 같은 슬라이드에서 데이터의 Quality보장이 잘 안된다는 것이다. 우리나라의 경우 굉장히 우수한 분들이 슬라이드 제작을 하기 때문에 슬라이드 간 편차가 거의 없고 좋은 Quality를 보장하지만, 동남아같은 의료시설이 낙후된 곳은 정도관리가 잘 되지 않아 매우 Poor한 슬라이드들이 만들어진다. 그래서 실제로 이미지를 획득하더라도 슬라이드 자체가 굉장히 Poor하기 때문에 진단 및 학습에 어려움이 크다.

## Karyotyping

### 데이터 소개

혈액 또는 골수 등을 채취하여 그 안에 들어있는 1~22번 염색체와 성 염색체\(X, Y\)를 분석하는 방법이다. 염색체를 추출하여 G, R, C, Q 밴딩에 대한 염색법을 이용하여 이미지 상에서 염색체의 밴드 정보가 잘 보이게 해준다.

![](../.gitbook/assets/karyotyping-2x.jpg)

위 그림과 같이 Karyotype 이미지가 얻어지며, 왼쪽은 무작위로 퍼져있는 슬라이드 내 염색체 분포 이미지이다. 오른쪽은 왼쪽의 염색체들을 분류하여 각 번호에 맞게 재정렬한 이미지이다. Karyotyping 검사는 이와 같은 프로세스로 진행이 되며 전처리 과정\(염색\)외에 가장 시간이 많이 걸리는 분류 작업은 전문가들 조차 숙련되지 않으면 어려운 점이 많다.

염색체를 분류하고나면 염색체들의 총합이 정상적인지, 특정 염색체가 변형되지 않았는지를 보아 검사 대상자가 병이 있는지를 판단한다. 진단 가능한 유명한 병으로는 다운 증후군과 터너 증후군 등이 있다. 

Karyotyping 이미지는 염색체의 Resolution이 가장 중요하다고 볼 수 있는데, 여기서 말하는 해상도는 일반적인 의미와는 조금 다르게 염색체가 얼마나 성장했는지\(길이가 얼마나 긴지\)로 결정된다. 그러므로, 해상도가 좋은 염색체들일수록 분류가 쉽다.

### Augmentation 방법

Karyotype은 grayscale이미지에 각 염색체마다 고유의 밴드 패턴이 있기 때문에 이를 학습할 수 있는 방향의 augmentation들이 필요하다.

* Rotation \(염색체들은 무작위로 퍼져있고, 머리와 꼬리 부분 위치가 무작위이므로 모든 경우에 대해 회전을 적용하는 것이 좋다\)
* Horizontal/Vertical Flip \(염색체들이 퍼져있는 모양은 항상 같지 않으므로, rotation과 같이 적용하면 다양한 경우를 예상하여 학습 가능하다\)
* Brightness/Contrast Adjustment \(Karyotyping 이미지 내 염색체들은 각 이미지마다 밝기 및 대조의 차이가 어느정도 있으므로 이를 고려하는 것이 좋다\)
* Random Crop \(Detection이 필요하다면 고려하는 것이 좋다\)

### 어려운 점

Public dataset의 경우 해상도가 좋지 않아 밴드 패턴 모양이 뚜렷하지 않아 육안으로 분간이 어렵다. 하지만, AI 사용시 밴드 패턴에 대해서는 어느정도 잘 학습이 된다고 볼 수 있다. Karyotyping의 가장 큰 문제점은 Overlap 되어있는 염색체들을 어떻게 분류하고 떼어낼 것인지와 염색체가 구부러지고 이물질이 가려져 있을 때의 분류가 어렵다는 점이다. 특히, 염색체가 상당히 많이 구부러진 경우 AI를 도입해도 생각보다 많은 양을 틀리게 된다. \(특히, 짧아질수록\)

