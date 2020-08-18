---
layout: post
title:  "[딥러닝 입문] 선형 회귀와 경사 하강법의 관계"
date:   2020-08-14
excerpt: "Linear regression"
feature: https://miro.medium.com/max/640/1*nbgt8RgzHPengnq6igs3aQ.png
tag:
- AI
comments: true
---

<b>'Linear regression'</b> 선형 회귀.  
* 정의 : 통계학에서 종속 변수 y와 한 개 이상의 독립 변수 (또는 설명 변수) X와의 선형 상관 관계를 모델링하는 회귀분석 기법이다. (from 위키백과)

...이걸 딥러닝을 처음 공부하는 사람들이 알아볼 수 있을까요? 분명 아래와 같은 질문을 하실껄요?

1. 종속 변수 y는 뭐고 독립 변수 X는 뭐야?
2. 선형 상관 관계를 모델링?
3. 그래서 선형 회귀와 경사 하강법의 관계가 어떻게 된다고?

언제나 그랬듯이 하나하나 뜯어보도록 하죠.

## 1. 종속 변수 y는 뭐고 독립 변수 X는 뭐야?
통계학에서 회귀란, 여러 개의 독립변수와 한 개의 종속변수 간의 상관관계를 모델링하는 기법을 통칭합니다. 모델링한다는 것은 [이전 포스트](https://akfmdl.github.io//ai_gradient_descent)에서 다뤘으니 감이 오지 않으신다면 다시 한번 읽어보시기 바랍니다.  
어쨌든, 아파트 가격을 예측하는 알고리즘을 만든다고 가정했을 때 종속 변수와 독립변수의 관계는 다음과 같습니다.
> 아파트 가격 -> 종속변수  
아파트 방 개수, 크기, 주변 학군 등 아파트 가격에 영향을 미치는 것들 -> 독립변수

즉 독립변수는 결과값에 영향을 미치는 feature들, 아파트 가격은 그 feature들을 통해 유추할 수 있는 target값이 되는 거죠.

## 2. 선형 상관 관계를 모델링?
위에서 배운 종속변수와 독립변수의 상관 관계를 모델링한다는 거죠. 그런데 그 관계를 x, y 2차원 축으로 그려보면 아래와 같이 선형으로 나타나기 때문에 '선형 상관 관계' 라고 하는 겁니다. 여기서 모델링 한다는 건 예측값과 실제값을 잘 표현하도록 잘 학습시킨다는 거죠.
<figure>
	<img src="https://t1.daumcdn.net/cfile/tistory/997E924F5CDBC1A628" width=200 height=200>
</figure>
참고로, 상관 관계와 인과 관계의 차이를 알고싶으신 분은 <a href="http://www.datamarket.kr/xe/index.php?mid=board_mXVL91&listStyle=viewer&document_srl=6771">이 사이트</a>를 참고하시기 바랍니다.

## 3. 그래서 선형 회귀와 경사 하강법의 관계가 어떻게 된다고?
이전 포스트에서 경사하강법은 Optimizer이며 처음에 말씀드렸듯이, 모델이 데이터를 잘 표현할 수 있도록 기울기(변화율)를 사용하여 모델을 조금씩 조정하는 최적화 알고리즘이라고 했죠? 선형 회귀 모델에서도 이러한 경사하강법을 활용하여 오차를 최소화시킵니다.
> 참고로 오차를 최소화 시킨다는 것은 곧 데이터를 잘 표현한다는 말이며 간단하게 학습을 잘 시킨다는 말입니다.

하지만 [이전 포스트](https://akfmdl.github.io//ai_gradient_descent)에서 설명드렸듯이, 오차를 최소화시키는 Optimizer의 종류는 다양하고 꼭 경사하강법을 사용하지 않아도 됩니다. 그런데 이 두개가 항상 붙어다니는 이유는 둘 다 기본적인 딥러닝 알고리즘이기 때문입니다.

## 따라서
'Linear regression' 즉 선형 회귀는 종속 변수와 한 개 이상의 독립 변수와의 선형 상관 관계를 모델링하는 회귀분석 기법이며, 잘 모델링 하기 위해 경사 하강법과 같은 Optimizer를 사용할 수도 있습니다.


> ref  
https://medium.com/@john_analyst/%ED%9A%8C%EA%B7%80-regression-%EB%9E%80-398c548e1560

## Previous
경사 하강법  
go to -> [Previous](https://akfmdl.github.io//ai_gradient_descent ){: .btn}