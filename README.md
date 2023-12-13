# Context_Prediction
self-supervised learning의 한 종류
self-supervised learning이란 라벨이 없는 untagged data를 기반으로 한 학습, 자기 스스로 학습데이터에 대한 분류를 수행
기존 학습법은 unsupervised learning, supervised learning으로 나뉨. 
두 학습법의 차이는 태그 데이터의 유무.
unsupervised learning은 태그데이터가 없기에 실제 데이터가 어떠한 범주에 해당하는지 모른 채 데이터 특징에 따라 클러스터링수행
supervised learning은 대상의 분류나 예측의 목적으로 사용.

Context Prediction은 자기지도학습(supervised learning)이며 이미지로부터 패치를 추출하여 패치간의 상대적위치를 예측하도록 학습.
이미지 하나를 9개의 패치로 나누어 이 패치의 순서를 맞추도록 모델을 학습
사람도 예측하기 어려운 task를 신경망이 예측

