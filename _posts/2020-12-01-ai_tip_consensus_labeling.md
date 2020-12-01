---
layout: post
title:  "[라벨링 노하우] 컨센서스 라벨링"
date:   2020-12-01
excerpt: "Consensus labeling"
feature: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTUUz_rgRMn0FyuHGei6nRFfeOEPJQvfmZ_gg&usqp=CAU
tag:
- AI
comments: true
---

## DEVIEW 2020의 '데이터 라벨링 너무 귀찮아요: 컨센서스 라벨링 도입기'
를 읽고 정리한 포스트입니다.

저는 Vision inspection 장비 개발자였습니다. 때문에 라벨링이 얼마나 귀찮은 일인지, 컨센서스를 맞추는 건 또 얼마나 어려운 일인지 잘 알고 있습니다.

본 강의에서 소개한 방식은 다음과 같습니다.

## 컨센서스 라벨링 자동화: SQIP
SQIP(Statistical Quality Inference Protocol)는 Crowd Truth라는 Framework을 참고했는데, 작업자들의 선택지에 대한 모호함을 수치화 시킨 방법입니다.

우선, 모든 작업자들의 선택지를 sum한 후 그 지표를 바탕으로 각 작업자의 결과차이를 기반으로 모호한 정도를 측정하는 것입니다.

결국 다수의 의견을 기반으로 평가한다는 거죠.

이러한 방법을 SQIP에서는 이미지 라벨링에 적용했는데요.

## 같은 이미지를 N명에게 주어 컨센서스 맞추기
### 라벨링 데이터를 2D Matrix로 변환
![image](https://user-images.githubusercontent.com/31917080/100744769-a616a880-3421-11eb-8862-1983dd59166f.png)
### 작업결과를 합치기
![image](https://user-images.githubusercontent.com/31917080/100744669-81bacc00-3421-11eb-9e3a-b1f48d2172ce.png)
### 작업자들이 가장 많이 라벨링 한곳을 기준으로 컨센서스 확정
![image](https://user-images.githubusercontent.com/31917080/100745071-158c9800-3422-11eb-8183-34a65162f5f1.png)

그리고 TWS 평가지표를 기반으로 다양한 알고리즘들을 적용했습니다.
![image](https://user-images.githubusercontent.com/31917080/100746324-e6772600-3423-11eb-976f-37e2a0637177.png)


Image Classification 문제의 경우에도 과반일치 방식을 사용했습니다.
![image](https://user-images.githubusercontent.com/31917080/100746935-ba0fd980-3424-11eb-8aae-31bd47e8c902.png)


DEVIEW의 해당 강의에는 해당 포스트에서 설명드린 것보다 훨씬 더 많은 불량 작업을 최소화시키기 위한 알고리즘이 소개됩니다. 정말 엔지니어들이 얼마나 많은 노력을 했는지 상상이 갑니다.


> ref  
https://tv.naver.com/v/16969174