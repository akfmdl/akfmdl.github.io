---
layout: post
title:  "[딥러닝 입문] 손실 함수와 경사 하강법의 관계"
date:   2020-08-18
excerpt: "Lost function"
feature: https://t1.daumcdn.net/cfile/tistory/99384F355A928B1C06
tag:
- AI
comments: true
---

<b>'Lost function'</b> 손실 함수.  
* 정의 : 예상한 값과 실제 타깃값의 차이를 함수로 정의한 것

위의 정의를 이해하기 위해 [이전 포스트](https://akfmdl.github.io//ai_gradient_descent)를 다시 한번 복습해볼까요?

## 복습
1. 딥러닝 알고리즘은 알아서 수식을 찾아준다.
2. 딥러닝은 문제를 대충 추론해서 정답이랑 비교했을 때 얼마나 다른지(오차)를 계산한다.
3. 그런데 여기서 오차를 이전 오차값 대비 현재 오차값의 변화량으로 계산한다.
4. 경사하강법은 이러한 변화량(기울기)을 사용하여 모델을 조금씩 조정(=학습)한다.

이 두가지 사실을 통해 우리가 얻을 수 있는 것은 경사하강법은 딥러닝이 알고리즘은 알아서 수식을 찾아주기 위한 하나의 방법이며, 오차값의 변화량을 통해 모델을 학습시킨다는 것입니다.

## 손실 함수
위에서 복습했던 것 중 계속 나오는 단어인 '오차값'
오차값은 단순히 변화량으로 계산하면 '정답 - 예측값'이 되겠죠? 그런데 좀 더 정확하게 계산하기 위한 여러 함수들이 개발되었습니다. 이러한 함수들을 '손실 함수'라고 합니다.
* 손실 함수의 종류  
  	> k : 샘플 번호  
	y<sub>k</sub> : 타겟값(정답), t<sub>k</sub> : 예측값
  * SE(squared error) : 제곱 오차  
	<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjNfxi%2FbtqAWxITre0%2FYtmkdmNp8E6Zy7f7T8pwRk%2Fimg.png" width=150> 
  * MSE(Mean Squared Error) : 평균 제곱 오차  
	<img src="https://t1.daumcdn.net/cfile/tistory/999E973A5A9273A405" width=150>  
	1/2 은 미분을 쉽게하기 위해 존재(값을 작게 하기 위함)  
  * CEE(Cross Entropy Error) : 교차 엔트로피 오차  
	<img src="https://t1.daumcdn.net/cfile/tistory/99C0D73B5A92769625" width=150>  
	위 식은 다음과 같이 변형 가능  
	<img src="https://t1.daumcdn.net/cfile/tistory/99C3EF395DA071DF13" width=150>  
	이것을 그래프로 그리면  
	<img src="https://t1.daumcdn.net/cfile/tistory/99384F355A928B1C06" width=500>  
	분류 문제에서 모델의 출력은 0에서 1 사이이므로 -log(y)의 함수는 위와 같습니다. 즉, 정답이 1이라고 했을 때, 정답에 근접하는 경우에는 오차가 0에 거의 수렴해갑니다. 그러나 0에 가까워지면, 정답에 멀어지면 멀어질수록 오차가 기하급수적으로 증가하는 것을 볼 수 있다. 정답에 멀어질수록 큰 패널티를 부여하는 것입니다.   
	따라서 출력값이 정답에서 멀어질수록 오차도 한없이 커지며 정답에 가까울수록 오차가 0에 가까워집니다. 그리고 출력값과 정답의 차이가 클 때 학습 속도가 빠를 것이라는 것도 유추해 볼 수 있습니다.  
	

## 경사하강법 재 정의
위에서 배운 내용으로 저희는 경사하강법을 아래와 같이 재 정의 할 수 있습니다.
정의 : 어떤 손실 함수(loss function)가 정의되었을 때 손실 함수의 값이 최소가 되는 지점을 찾아가는 방법

## 따라서
저희는 손실함수와 경사하강법의 관계를 알 수 있습니다. 정리하면,
> 신경망이 잘 학습할 수 있도록 하기 위해 손실 함수를 사용하여 오차를 구하고 그 값을 미분한 값이 최소화되도록 하는 방식인 경사 하강법을 사용한다.


> ref  
https://hyeonnii.tistory.com/228  
https://kolikim.tistory.com/36

## Previous
이전 강의에서는 경사 하강법에 대해 설명해드렸습니다.  
go to -> [Previous](https://akfmdl.github.io//ai_gradient_descent ){: .btn}