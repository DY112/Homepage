---
title: GAN부터 WGAN까지
subtitle: GAN의 기본과 다양한 해석, 그리고 WGAN까지 이어지는 간략한 설명

# Summary for listings and search engines
summary: GAN의 기본과 다양한 해석, 그리고 WGAN까지 이어지는 간략한 설명

# Link this post with a project
projects: []

# Date published
date: "2021-10-03"

# Date updated
lastmod: "2021-10-03"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags: 
- Article
- GAN

categories:
---

## GAN 부터 WGAN 까지

[원문 출처](https://lilianweng.github.io/lil-log/2017/08/20/from-GAN-to-WGAN.html) | [한국어 번역본 출처](https://github.com/yjucho1/articles/blob/master/fromGANtoWGAN/readme.md#generative-adversarial-network-gan)

본 포스트는 간단한 정리입니다.
자세한 내용은 출처를 참고하세요.

### GAN loss의 수학적 해석
GAN 의 loss함수는 real data distribution과  generated data distribution을 JS Divergence로 측정하는 것과 결과적으로 같음

### Problems in GANs
1. Hard to achieve Nash equilibrium

    두 플레이어 (G&D)의 업데이트가 동시에 이루어지므로, 이는 불안정성을 더 키울 수 있다.
2. Low dimensional supports
    
    고차원 공간(생성된 이미지 또는 진짜 이미지) 에서 저차원 매니폴드는 서로 겹칠 확률이 매우 적음.
    진짜 이미지는 고유한 데이터 특성을 갖고 있으므로 저차원 매니폴드이며, 가짜 이미지는 랜덤 벡터로부터 생성되었으므로 또한 저차원 매니폴드이다.
    두 이미지는 따라서 고차원(이미지공간) 내에 존재하는 저차원 매니폴드 두개이며, 이 둘은 겹치는 경우가 거의 없다.
    따라서 이 둘을 완벽히 구분하는 D가 존재할 수 있다.따라서 D를 헷갈리게 할 정도로 완벽하게 real 같은 fake data를 생성하기 어렵다.
3. Vanishing gradient
    
    2번에서 말한 것 처럼 D가 완벽해지기 쉽다면, 손실함수는 점점 0에 가까워지며, 학습 과정에서 loss를 업데이트 할 수 있는 Generator gradient를 얻지 못해서 결국 학습이 종료됨.
4. Mode collapse
    
    Generator의 목표가 오로지 Discriminator를 속이는 데에는 성공했지만 실제 데이터의 매니폴드를 폭넓게 학습하지는 못한 상황. 극단적으로 낮은 다양성을 갖는 공간 내에 같혀버린 상황.
5. Lack of a proper evalutaion metric
    
    Validation Metric이 없으므로 언제 학습을 중단해야하는지, 어떤 모델이 제일 나은지 판단하기 어렵다. (Unsupervised GAN의 경우)