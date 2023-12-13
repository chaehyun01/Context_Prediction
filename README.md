# Context_Prediction
## 서론
self-supervised learning의 한 종류입니다.<br/>

self-supervised learning이란 라벨이 없는 untagged data를 기반으로 한 학습, 자기 스스로 학습데이터에 대한 분류를 수행합니다.<br/>
기존 학습법은 unsupervised learning, supervised learning으로 나뉩니다. <br/>
두 학습법의 차이는 태그 데이터의 유무입니다.<br/>
unsupervised learning은 태그데이터가 없기에 실제 데이터가 어떠한 범주에 해당하는지 모른 채 데이터 특징에 따라 클러스터링수행합니다.<br/>
supervised learning은 대상의 분류나 예측의 목적으로 사용합니다.<br/>

### Context Prediction은 자기지도학습(self-supervised learning)이며 이미지로부터 패치를 추출하여 패치간의 상대적위치를 예측하도록 학습합니다.<br/>
이미지 하나를 9개의 패치로 나누어 이 패치의 순서를 맞추도록 모델을 학습합니다.<br/>
사람도 예측하기 어려운 task를 신경망이 예측합니다. <br/>

기존 자기지도학습이 개발되기 전 모델들의 공통적인 한계존재합니다.<br/>
Label 데이터가 없으면 아무것도 할 수 없습니다.<br/>
이러한 문제점을 해결하기 위해 Label 데이터 없이 스스로지도하는 self-supervised learning 개발하였습니다.<br/>
Conetxt Prediction이 발표 됬던 시기만 해도 self-supervised learning이 널리 알려지지않았습니다.<br/>
대부분 Supervised learning 사용했으나, 큰 단점 " 많은 비용 " 입니다. <br/>
이미지 마다 Label 데이터를 만드는 작업이 큰 비용이 들게 했습니다. <br/>
Context Prediction은 이러한 상황에서 Label 데이터 없이 이미지의 특성을 학습할 수 있습니다. <br/>
## 학습방법
### Context Prediction은 input image 패치의 상대 위치를 맞추도록 학습하는 방법을 제안하는 방법입니다.<br/>
그림과 같이 모델에게 파란색 네모의 이미지 패치와 8개의 빨간색 이미지 패치 중 한개를주고서 몇번째 패치인지 맞추도록 학습합니다.<br/>
![CP1](https://github.com/chaehyun01/Context_Prediction/assets/146818726/39e97660-633c-4806-bad8-f64f2ed23177)<br/>
모델은 크게 2가지의 CNN으로 구성됩니다. input으로 받는 이미지가 2개이기 때문입니다.<br/>
9개의 Image Patch중 중앙의 패치와 랜덤으로 선택한 이미지 패치가 각각의 CNN을 통과하도록 되어있습니다. <br/>이렇게 각각 연산 되어 나온 Feature는 fc7에서 합쳐져서 최종적으로는 파란패치를 제외한 8가지의 종류(fc9)를 맞추는 구조로 되어있습니다.<br/>
이때 최종 Output인 8가지의 종류란 ‘상대 위치 종류’ 를 의미합니다. <br/>
예를 들어 결과가 0이라면 중앙 Patch를 기준으로 왼쪽 상단에 위치한 Patch임을 의미합니다. <br/>
반면 결과가 1이라면 상단에 위치한 Patch를 의미합니다. <br/>
![CP2](https://github.com/chaehyun01/Context_Prediction/assets/146818726/1ff42ea0-2ead-4270-b680-5874a55d91ce)
<br/>
## Test Runnig
1. python 내부에서 train.py 을 실행합니다. 이렇게 하면 2000번 반복할 때마다 스냅샷을 생성하는 무한 훈련 루프가 시작됩니다. 

코드는 GPU 0에서 실행됩니다. 환경 변수 CUDA_VISIVE_DEVICE를 사용하여 GPU를 변경할 수 있습니다.

모든 테스트는 python 2.7로 수행되었습니다.('train.py ')를 사용하여 ipython 내부에서 실행하는 것이 좋습니다.

2. train.py 스크립트를 중지하려면 코드를 실행한 디렉터리에 train_quit 파일을 생성해야 합니다.
   
코드가 백그라운드 프로세스를 시작하여 데이터를 로드하고 Ctrl+C를 통해 코드가 중단되면 이러한 백그라운드 스레드가 종료된다는 보장이 어렵기 때문에 이러한 우회 접근 방식이 필요합니다.

train.py 이 종료된 후 다시 started하는 경우 출력 디렉토리를 검사하고 반복 횟수가 가장 많은 스냅샷부터 계속 시도합니다.

3. 코드를 실행한 디렉터리에 train_ pause 파일을 생성하면 언제든지 훈련을 일시 중지할 수 있습니다.

그러면 pycaffe을 사용하여 네트워크 상태를 검사할 수 있습니다.

4. 실험을 위해 1.7M 반복 실험을 실행했습니다. 이 시점 이후에 출력에서 debatchnorm.py 을 실행할 수 있습니다.
   
실행한 후에는 미세 tuned가 가능한 모델이 있습니다. 미세 조정 전에 데이터 의존적 초기화 및 보정 절차 [Krähenbühl et al.]를 사용하는 것이 좋습니다.

debatchnorm.py 을 사용하면 scaled 가중치가 심하게 발생하기 때문입니다.

이 절차를 사용하여 훈련되고 VOC2007에서 fast-rcnn으로 미세 조정된 네트워크는 51.4%의 MAP를 달성합니다.
