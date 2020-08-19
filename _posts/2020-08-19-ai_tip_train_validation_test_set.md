---
layout: post
title:  "[훈련 노하우] Train, Validation, Test set 개념 뿌수기"
date:   2020-08-19
excerpt: "Train, Validation, Test set"
feature: https://www.sisa-news.com/data/photos/20200521/art_159005622283_490cdb.jpg
tag:
- AI
comments: true
---

> 모델과 학습에 대한 개념이 안 잡히신 분들은 [딥러닝과 경사 하강법](https://akfmdl.github.io//ai_gradient_descent)를 참고하시기 바랍니다.

## Train, Validation, Test set 개념

모델을 아무것도 모르는 고3이라고 가정해보죠. 고3의 목표는 무엇일까요? 수능을 잘 치는 것이겠죠? 그 동안 이 고3 수험생은 교과서, 각종 학습지 등으로 공부를 빡쎄게 합니다. 그런데 수능은 1년에 한번 뿐이니.. 수능과 비슷한 중간, 기말, 모의고사도 칩니다. 자신의 실력을 가끔 <b>'검증'</b>해보는거죠. 검증해보고 자신이 어떤 과목에서 부족한지를 깨닫고 그 과목을 집중 공부하면 되는거죠.

각각의 정의와 역할은 다음과 같습니다.

<b>'Train set'</b> 훈련 세트.  
* 정의 : model을 fit하기 위해 사용되는 데이터 샘플. 
  * 역할 : 고3 수험생이 공부하는 교과서, 학습지 등.
  
딥러닝에서 model을 fit한다는 것은 학습시킨다는 말과 같습니다. 그래서 함수명도 '.train()'보다는 '.fit()'을 많이 사용하죠. 학습이란게 데이터에 맞게 수식을 잘 fitting 해주는 것이기 때문이겠죠?

<b>'Validation set'</b> 검증 세트.  
* 정의 : 모델의 하이퍼파라미터를 튜닝할 때 모델 학습의 평가 척도로 사용되는 데이터 샘플.
* 모델의 성능을 update하는 역할을 하므로 dev set, development set이라고도 함.
  * 역할 : 모의고사

하이퍼파라미터란 머신러닝에서 어떠한 임의의 모델을 학습시킬때, 튜닝해주어야하는 변수를 말합니다.

<b>'Test set'</b> 테스트 세트.  
* 정의 : 학습이 끝난 모델을 최종적으로 평가하기 위한 데이터 샘플.
  * 역할 : 수능

고3 수험생은 평소 Train set으로 학습을 하고 가끔 Validation set으로 검증을 해보고 어떤 방식으로 학습을 해야 할지 방향을 잡습니다(하이퍼파라미터 튜닝). 그리고 드디어 Test set으로 최종 테스트를 하는 것이죠.

## Validation set VS Test set
두 샘플 데이터의 다른 점은 '성능 관여'라는 점입니다. 고3 수험생이 모의고사를 친 뒤, 부족한 부분을 열심히 학습하거나 아예 방향을 틀 수 있는 것처럼 validation set은 수험생의 성능(?)에 간접적으로 영향을 미칩니다.  
하지만 Test set은 학습을 마친 수험생이 한번만 수행하고 이 점수로 최종 대학이 결정된다는 점에서 Validation set과 다르죠. 수험생의 성능을 높이고 싶으면 재수(=Transfer learning)를 해야합니다...ㅠㅠ  
* Transfer learning : 처음부터 학습시키는 게 아닌 이미 학습된 모델을 새로운 Dataset을 추가하여 학습시키거나 하이퍼파라미터 튜닝을 하여 재학습 시키는 것입니다.


## Data set 분배
수험생(모델)의 실력(성능)을 높이기 위해서 학습(train set)과 모의고사(validation) 수능(test)의 분배를 어떻게 해야할까요? 학습만 하고 모의고사는 안치고 바로 수능을 본다면.. 너무 위험하겠죠? 반대로 학습은 안하고 모의고사만 주구장창 본다면? 둘 다 좋지 않은 케이스인건 확실합니다.  
딥러닝에서도 모델의 성능을 높이기 위해 Data set 분배를 잘 해줘야 하는데요. 일반적으로 아래와 같이 분배해주었습니다.  
```
1. Train과 Test만 나눌경우
Train : Test
  7   :   3
2. Train과 Validation, Test로 나눌 경우
Train : Validation : Test
  6   :      2     :   2
```
하지만 이것은 정해진 규칙은 아니며 데이터가 적을 경우, 학습시키기도 부족한 데이터를 검증, 테스트 데이터로 나누는 것은 의미가 없죠.  
Validation set은 최적의 하이퍼파라미터를 찾아내는 목적으로 사용되는 데이터이기 때문에 그렇게까지 많이 필요 없습니다. 특히 Dataset이 굉장히 많을 경우. 약 백만 개가 있을 경우에는 아래와 같이 나누어도 괜찮습니다.
```
Train : Validation : Test
  98   :     1     :   1
```
비율로 보면 Validation과 Test set이 엄청 적어보이지만 절대량으로 치면 무려 10,000개나 됩니다. 이 정도면 여러 특성들이 골고루 분포되어 있을 거라 충분히 검증용으로 사용할만 합니다.  
만약 데이터가 부족한데 꼭 검증을 해야겠다면 어떻게 해야할까요?

## K-폴드 교차 검증 구현
* 정의 : K개의 fold를 만들어서 진행하는 교차검증

Train data set에서 Validation set으로 나누니 train할 data가 부족해져 성능이 낮아지는 현상이 있었습니다.
이러한 현상을 보완하기 위해 아래와 같이 진행하는 것을 <b>'K-폴드 교차 검증 구현'</b>이라고 합니다.
* dataset을 k개의 폴드로 나누어 Validation VS Train data로 사용
* 폴드를 번갈아가며 바꾸어 Validation, Train set도 바꾸며 반복
* k개의 검증 세트로 k번 성능을 평가한 후 계산된 성능의 평균을 내어 최종 성능을 계산

원리에 대해 설명드리자면  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F993CCE445AC0B5A233734C" width=500>
1. 먼저 기존처럼 Training Set과 Test Set을 나눈다
2. Training을 K개의 fold로 나눈다
3. 위는 5개의 Fold로 나눴을때 모습이다
4. 한 개의 Fold에 있는 데이터를 다시 K개로 쪼갠다음, K-1개는 Training Data, 마지막 한개는 Validation Data set으로 지정한다
5. 모델을 생성하고 예측을 진행하여, 이에 대한 에러값을 추출한다
6. 다음 Fold에서는 Validation셋을 바꿔서 지정하고, 이전 Fold에서 Validatoin 역할을 했던 Set은 다시 Training set으로 활용한다
7. 이를 K번 반복한다

여기까지 Dataset을 Train과 validation set으로 K개의 fold를 만드는 방법입니다. 그 다음은 이렇게 나눈 데이터를 검증하는 방법입니다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile27.uf.tistory.com%2Fimage%2F9916854E5AC0B61D220CD3" width=500>

1. 각각의 Fold의 시도에서 기록된 Error를 바탕(에러들의 평균)으로 최적의 모델(조건)을 찾는다
2. 해당 모델(조건)을 바탕으로 전체 Training set의 학습을 진행한다
3. 해당 모델을 처음에 분할하였던 Test set을 활용하여 평가한다

이렇게 K 겹으로 나누어 K번 검증을 하면 1번 검증하는 것을 K번이나 검증할 수 있으므로 데이터가 부족해도 Validation을 할 수 있고 믿을 만한 검증을 할 수 있다는 것입니다.  
하지만 그냥 Training set / Test set 을 통해 진행하는 일반적인 학습법에 비해 시간 소요가 크다는 단점이 있습니다.

> ref  
https://towardsdatascience.com/train-validation-and-test-sets-72cb40cba9e7  
https://brunch.co.kr/@coolmindory/31  
https://nonmeyet.tistory.com/entry/KFold-Cross-Validation%EA%B5%90%EC%B0%A8%EA%B2%80%EC%A6%9D-%EC%A0%95%EC%9D%98-%EB%B0%8F-%EC%84%A4%EB%AA%85  

