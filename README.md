# Context_Prediction
##self-supervised learning의 한 종류입니다.<br/>

###self-supervised learning이란 라벨이 없는 untagged data를 기반으로 한 학습, 자기 스스로 학습데이터에 대한 분류를 수행합니다.<br/>
기존 학습법은 unsupervised learning, supervised learning으로 나뉩니다. <br/>
두 학습법의 차이는 태그 데이터의 유무입니다.<br/>
unsupervised learning은 태그데이터가 없기에 실제 데이터가 어떠한 범주에 해당하는지 모른 채 데이터 특징에 따라 클러스터링수행합니다.<br/>
supervised learning은 대상의 분류나 예측의 목적으로 사용합니다.<br/>

Context Prediction은 자기지도학습(self-supervised learning)이며 이미지로부터 패치를 추출하여 패치간의 상대적위치를 예측하도록 학습합니다.<br/>
이미지 하나를 9개의 패치로 나누어 이 패치의 순서를 맞추도록 모델을 학습합니다.<br/>
사람도 예측하기 어려운 task를 신경망이 예측합니다. <br/>

기존 자기지도학습이 개발되기 전 모델들의 공통적인 한계존재합니다.<br/>
Label 데이터가 없으면 아무것도 할 수 없습니다.<br/>
이러한 문제점을 해결하기 위해 Label 데이터 없이 스스로지도하는 self-supervised learning 개발하였습니다.<br/>
Conetxt Prediction이 발표 됬던 시기만 해도 self-supervised learning이 널리 알려지지않았습니다.<br/>
대부분 Supervised learning 사용했으나, 큰 단점 " 많은 비용 " 입니다. <br/>
이미지 마다 Label 데이터를 만드는 작업이 큰 비용이 들게 했습니다. <br/>
Context Prediction은 이러한 상황에서 Label 데이터 없이 이미지의 특성을 학습할 수 있습니다. <br/>

Context Prediction은 input image 패치의 상대 위치를 맞추도록 학습하는 방법을 제안하는 방법입니다.<br/>
그림과 같이 모델에게 파란색 네모의 이미지 패치와 8개의 빨간색 이미지 패치 중 한개를주고서 몇번째 패치인지 맞추도록 학습합니다.<br/>
![CP1](https://github.com/chaehyun01/Context_Prediction/assets/146818726/39e97660-633c-4806-bad8-f64f2ed23177<br/>
모델은 크게 2가지의 CNN으로 구성됩니다.input으로 받는 이미지가 2개이기 때문입니다.<br/>
9개의 Image Patch중 중앙의 패치와 랜덤으로 선택한 이미지 패치가 각각의 CNN을 통과하도록 되어있습니다. <br/>이렇게 각각 연산 되어 나온 Feature는 fc7에서 합쳐져서 최종적으로는 파란패치를 제외한 8가지의 종류(fc9)를 맞추는 구조로 되어있습니다.
![CP2](https://github.com/chaehyun01/Context_Prediction/assets/146818726/1ff42ea0-2ead-4270-b680-5874a55d91ce)
