# \(2016\) SSD: Single Shot MultiBox Detector

## 1. Introduction

일반적인 2 stage object detection model\(Detection -&gt; Classification\)들은 정확도는 좋으나 이 당시 가장 빠르다고 나왔던 Faster-RCNN의 경우도 FPS가 겨우 7밖에 되지 않았음. 처리속도가 너무 느려 빠르게 하고자 하는 시도가 많았는데, 속도와 정확도의 trade-off가 꽤 심했음.

이 논문에서는 YOLO와 같은 1 stage detection model을 선보이면서, 속도 대비 정확도를 최상급으로\(mAP 73.2%, 59 FPS for VOC2007\) 만드는 방법을 소개한다.

### Contributions

* Single shot detector 중 가장 좋은 성능을 보임.
* 다양한 scale의 feature map으로부터 multi scale prediction을 가능하게 한다.\(Bounding box 후보 크기가 다양함\)
* Bounding box proposal을 제거해서 속도를 올림.

## 2. Model Architecture

![](../../.gitbook/assets/screenshot-from-2020-02-14-14-59-03%20%281%29.png)

SSD의 기본 모델 구성은 위와 같다. VGG-16 model을 backbone으로 사용하여 특정 Conv output들로부터 bounding box를 추출하여 low-level에서 high-level feature로 가면서 다양한 크기의 bounding box 위치를 고려한다. \(이 말은 multi-scale object detection을 고려한다는 의미와 같다.\) SSD에서는 총 6군데의 feature map에서 추출하게 되며 아래의 그림과 같이 고정된 영역을 bounding box로써 살펴본다.

![](../../.gitbook/assets/screenshot-from-2020-02-14-14-58-55.png)

위 그림처럼 SSD의 bounding box는 이전의 다른 모델들과 다르게 conv layer의 feature map\(HxW\)의 크기대로 볼 수 있다. 예를 들면, \(b\)의 8x8 feature map을 보면 input image의 크기가 224x224라고 할 때 feature map의 1 pixel은 입력 이미지에서 28 픽셀만큼의 영역을 의미한다. 그래서 SSD에서는 각 feature map의 1개의 pixel을 cell이라 부르고 1개의 cell에 대해 aspect ratio를 다양하게 주어 cell 당 다양한 모양의 bound box를 생성한다. 이 방식으로 object의 후보를 생성하면 논문 기준으로 300x300 크기의 입력 이미지로 8,732개의 박스를 생성한다.

## 3. Learning Strategy

## 4. Experimental Results



