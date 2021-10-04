---
title: Multi-Domain Learning for Accurate and Few-Shot Color Constancy
subtitle: 다양한 카메라에서 촬영된 이미지를 한꺼번에 사용하여 CC model 트레이닝하기

# Summary for listings and search engines
summary: 다양한 카메라에서 촬영된 이미지를 한꺼번에 사용하여 CC model 트레이닝하기

# Link this post with a project
projects: []

# Date published
date: "2021-10-04"

# Date updated
lastmod: "2021-10-04"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption:
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags: 
- PR
- Color Constancy

categories:
---

## PR1) Multi-Domain Learning for Accurate and Few-Shot Color Constancy

[PDF](https://openaccess.thecvf.com/content_CVPR_2020/papers/Xiao_Multi-Domain_Learning_for_Accurate_and_Few-Shot_Color_Constancy_CVPR_2020_paper.pdf)

### Model Architecture
![](architecture.png "Backbone 자체는 FC4의 SqueezeNet 버전을 사용했다. Fire block은 SqueezNet이라는 논문에서 소개되었는데, 연산량 대비 성능이 좋다고 한다.")


### Objective

카메라마다 다른 센서를 사용하기 때문에 생겼던 CameraRGB space domain 문제를 Multi-Domain learning으로 해결하고자 함.
Multi-Domain learning의 핵심은 서로 다른 도메인의 데이터에 대해 하나의 Universal feature extractor로 피쳐 추출을 한다는 것이 특징인데, 이 모델에서도 해당 아이디어를 사용함.

### Novelty

- Color Constancy 문제에 Multi-Domain learning 사용
- Device-specific channel re-weighting module 사용
- Re-weighted Feature에 Shared illuminant estimator 사용

### Misc

- 디바이스마다 다르게 학습되는 Re-weighting module은 전체 모델 파라미터의 6.7% 뿐이므로 Few-shot learning task에도 적절함
- 단일 조명 CC 이기 때문에 GT illuminant chromaticity와 Angular Error를 잼
- 사용된 데이터셋은 reprocessed Gehler-Shi, NUS-8, Cube+