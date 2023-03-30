# FCN: Fully Convolutional Networks for Semantic Segmentation
###### [Submitted on 14 Nov 2014 (v1), last revised 8 Mar 2015 (this version, v2)]  https://arxiv.org/pdf/1411.4038.pdf
<br>

## FCN
**Fully Convolution Networks는 이미지 분류 AlexNet, VGG net, GoogLeNet과 같은 최신의 분류 네트워크를 fully convolutional 네트워크로 적용하고, 분할 작업에 대한 fine-tuning을 통해 학습된 표현을 전이시킨다.** <br> 
**이후 shallow layer와 dense layer를 결합하여 보다 더 정확한 분할을 생성하는 새로운 아키텍처를 정의한다.** <br>
<br>

💡 point
- **CNN end-to-end 학습** : <br>
픽셀별 예측 작업을 위해 CNN을 end-to-end로 학습하여, 입력 이미지와 출력 레이블 간의 모든 변환을 하나의 네트워크에서 학습한다. <br>
※end to end learning : 입력에서 출력까지 파이프라인 네트워크 없이 신경망으로 한 번에 처리
- **입력 이미지와 출력 레이블 모두 임의의 크기** : <br>
기존 CNN은 고정 크기의 이미지에 대해서만 동작했지만 FCN은 입력 이미지와 출력 레이블 모두 임의의 크기가 될 수 있다. 
이를 위해 FCN의 모든 layer는 convolution 연산만을 사용하며, 마지막 layer에서는 픽셀 단위의 출력을 얻기 위해 upsamplig layer를 사용한다.
- **전체 이미지 한번에 처리** : <br>
FCN은 기존 CNN과 마찬가지로 subsampled pooling을 사용하여 고해상도 이미지를 저해상도로 축소한다. 그러나 FCN은 upsamling layer를 사용하여 다시 고해상도로 복원한다. 이를 통해 전체 이미지에 대해 한번에 feedforward 계산 및 backpropagation을 수행할 수 있으며, 높은 밀도의 출력을 생성할 수 있다.


💡 To [image segmentation] From [image classification]
- **Convolutionalization**
- **Deconvolution**
- **Skip architecture**
<br>

## Convolutionalization
기존의 이미지 분류 AlexNet, VGG net, GoogLeNet 모델들은 입력 데이터의 고차원 특징을 저차원으로 압축하여 class를 분류하기 위해 fully connected layer를 출력층으로 사용한다. 
하지만 segmentationd에서는 출력층으로 fc layer의 사용이 문제를 일으킨다. <br>

먼저, segmentation은 이미지의 각 픽셀에 대해 클래스를 분류하고 객체 및 배경을 분할해야 하므로 위치 정보가 매우 중요하다. 하지만 fc layer를 사용하면 가중치 수가 줄어들어 **위치 정보가 사라진다.** 
또 다른 문제는 **입력 이미지의 크기가 고정된다**는 것이다. Dense layer의 가중치 개수가 고정되면 바로 앞 layer의 Feature Map의 크기도 고정되며, 연쇄적으로 각 layer의 Feature Map 크기와 Input Image 크기가 고정되게 된다. <br>

이를 해결하기 위해 FCN은 fc layer 대신 conv layer를 사용하는 Convolutionalization을 한다. 이는 출력 Feature map이 원본 이미지의 위치 정보를 내포할 수 있게 하며, 입력 이미지의 크기 제한을 없앤다. <br>
<br>

## Deconvolution


## Skip architecture


