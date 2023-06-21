# Fall Detection Using Deep Learning

본 연구는 [ICCV 2017] R-C3D Region Convolutional 3D Network for Temporal Activity Detection
논문을 참조하여 작성하였으며, 낙상감지를 주제로 분석하였다.

# Model figure
![image](https://github.com/MyoungChulcode/Fall-Detection-Using-Deep-Learning/assets/101051049/6f4d8e2c-3fbc-4a13-8c37-717120f05109)

# Project explanation
**1. 프로젝트 선정 배경 및 필요성**
  3학년 2학기 데이터분석 캡스톤디자인에서 “범죄 분석을 위한 이상치 탐색 및 클러스터링”을 주제로 연구를 진행하였다. 이상치 탐지 모델로 CNN 구조의 C3D, R3D를 사용하였지만 이상치 데이터의 특징을 고려한다면 이상치 프레임은 희소하게 발생할 확률이 높으며 그룹 내에서 정상 프레임에 의해 편향될 가능성이 존재한다. 이에 본 연구에서는 R-C3D base object detection을 활용한 이상치 탐지 모델을 개발할 것이다. 특히 낙상 감지는 bounding box 내에서 temporal information이 중요하기 때문에 기존에 있던 시스템에 비해 빠르게 정확하게 감지할 것으로 기대한다.


**2. 프로젝트 주요 내용**
 본 연구는 [ICCV 2017] R-C3D Region Convolutional 3D Network for Temporal Activity Detection 논문에서 제안하는 R-C3D 모델을 사용하여 낙상 감지 시스템에 적용한다.
1) AI-HUB에서 낙상 안전사고 data-set 다운로드
2) 낙상 발생구간에 대한 temporal annotation file(xml or json) 확인 후 조정
3) open cv로 bounding box를 annotation하고 낙상 발생영역에 대한 ROI 영역 검출
4) C3D middle convolution layer의 각 feature map 시각화
5) feature map을 정성적으로 평가하여 사용할 feature extraction 모델 결정
6) R-C3D base object detection과 training 진행
7) IOU로 performance measure 진행


**3. 목표 및 방법**
낙상 안전사고를 감지하는 모델을 설계하고 어플리케이션 레벨까지 시각화하는 프로그램을 개발
1) 활용 장비: 연구실, 개인 PC(3070 GPU 1대, 3060 GPU 1대) 및 연구실 서버를 활용
2) 사람, 이상치 데이터 셋: MPII, FPDS, COCO, AI-HUB(시니어 이상행동 영상)
3) 프로그래밍 언어: 모델 학습(python), 어플리케이션 개발(c++)


**4. 개발 내용**
1) MPII, FPDS, COCO data의 사람 영역에 학습한 Nanodet model을 활용하여 person detection 수행
2) person detection model을 활용하여 AI-HUB ‘시니어 이상행동’의 낙상 ROI 영역 검출
3) R-C3D를 활용하여 UCF-101 data의 특정 행동 분석 진행
4) Nanodet으로 학습한 person detection 모델은 이상 영상의 공간적 정보로 활용.
5) R-C3D로 학습한 action recognition 모델은 이상 영상의 시간적 정보로 활용.
6) 학습 진행시 AI-HUB ‘시니어 이상행동’의 낙상 ROI 영역을 활용하여 UHD 영상에서 발생할 수 있는 공간적 변화의 문제점을 방지함.


**5. 기대효과 및 활용방안**
1) 질병 관리청에 따르면 노인 낙상의 발생은 점점 늘어나고 있으며 심각한 손상을 동반하거나 낙상으로 인한 합병증으로 사망에까지 이르게 한다. 미국의 65세 이상 노인 중 3분의 1 이상에서 연간 한 번 이상 낙상을 경험한다고 하며, 우리나라의 경우 65세 이상 노인의 신체 손상 중 반 이상의 원인이 낙상이다.
2) 노인 낙상은 낙상으로 인한 사망 이외에도 중증의 손상으로 인해 삶의 질이 현저하게 감소하는 문제를 초래한다. 딥러닝 모델을 활용하여 자동으로 낙상을 감지하는 시스템을 개발하면 사고에 대한 적절한 손상 예방과 대처에 큰 기여를 할 것으로 기대한다.

**6. 결론 및 제언**
Nanodet을 통해 person detection을 수행하고 R-C3D를 통해 UCF-101의 action recognition task를 수행하였다. R-C3D model을 활용하여 anomaly detection을 수행하였을 때, 성능 개선이 있는지 아직 실험을 못 하였다. 해당 부분에 대한 실험과 연구가 더욱 필요하다.

# Demo example
**1. person detection**

![image](https://github.com/MyoungChulcode/Fall-Detection-Using-Deep-Learning/assets/101051049/b1583f52-79d8-4bb9-bdfd-defcd751a3e5)

**2. ROI extraction**

![image](https://github.com/MyoungChulcode/Fall-Detection-Using-Deep-Learning/assets/101051049/6725e371-484a-4605-9b81-56eb183fb3a8)

**3. R-C3D action recognition**

![image](https://github.com/MyoungChulcode/Fall-Detection-Using-Deep-Learning/assets/101051049/7ba302df-d8fe-45f0-a639-905febe2d0d4)
