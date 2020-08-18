---
layout: post
title:  "[딥러닝 입문] 05. 로지스틱 회귀"
date:   2020-08-18
excerpt: "Logistic regression"
feature: https://mblogthumb-phinf.pstatic.net/MjAxODA1MjdfMjI3/MDAxNTI3MzU2OTE4NTQw.Vo_z9kQAYu_U5NUAX8Jeb4K_RvEF9tANme2Afq4Ft6Mg.eZShGvApNJMNWgfQ3i3SHr2duGOkFGpMCuaGaSLyRD0g.PNG.lyshyn/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-05-27_%EC%98%A4%EC%A0%84_2.47.18.png?type=w2
tag:
- AI
comments: true
---

<b>'Logistic regression'</b> 로지스틱 회귀.  
* 정의 : 독립 변수의 선형 결합을 이용하여 사건의 발생 가능성을 예측하는데 사용되는 통계 기법이다.(from 위키백과)

지난 포스트에서 공부한 선형 회귀의 정의와 많이 다른가요?
* 선형 회귀 : 통계학에서 종속 변수 y와 한 개 이상의 독립 변수 (또는 설명 변수) X와의 선형 상관 관계를 모델링하는 회귀분석 기법이다. (from 위키백과)

별로 다르지 않죠? 그 이유는 로지스틱 회귀는 선형 회귀의 단점을 보완한 모델이기 때문입니다. 그럼 선형 회귀의 단점이 무엇이며 어떻게 보완했는지 살펴보도록 하죠.

## 선형 회귀의 단점
실생활에서 모든 원인과 결과는 아래 왼쪽 그림과 같이 직선 형태로 표현할 수 없습니다. 그래서 S자 비선형 형태로 정확도를 높인 것이 바로 로지스틱 회귀죠. 또한 선형 회귀 식의 x값(독립변수)은 -∞ ~ +∞의 범위를 갖고있습니다. 그러나 0과 1사이의 확률값만을 얻기를 원할 때에도 이 로지스틱 회귀가 사용됩니다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb6RYtA%2FbtqACP40kYg%2FyWYC5rbnWuDwCvbh09zyBK%2Fimg.png" height=200>

## 로지스틱 회귀가 S자인 이유
활성화 함수로 시그모이드(sigmoid)함수를 사용했기 때문입니다.

선형 회귀와 활성화 함수를 100% 이해하시고 이 포스트를 보셨다면 로지스틱 회귀가 별 것 아니라는 것을 알게 되셨을겁니다. 아직 선형 회귀와 활성화 함수에 대해 이해가 부족하신 분들은 [선형 회귀와 경사 하강법의 관계](https://akfmdl.github.io//ai_linear_regression), [활성화 함수](https://akfmdl.github.io//ai_activation_function) 이 포스트들을 참고하시기 바랍니다.



> ref  
https://ebbnflow.tistory.com/129  
https://m.blog.naver.com/lyshyn/221285013102  


## Previous
선형 회귀와 경사 하강법의 관계  
go to -> [Previous](https://akfmdl.github.io//ai_linear_regression){: .btn}

활성화 함수  
go to -> [Previous](https://akfmdl.github.io//ai_activation_function){: .btn}