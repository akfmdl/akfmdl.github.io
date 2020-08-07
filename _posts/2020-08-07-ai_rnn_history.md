---
layout: post
title:  "수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN) 1장"
date:   2020-08-07
excerpt: "LSTM의 탄생"
feature: http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-chain.png
tag:
- AI
comments: true
---
<iframe width="560" height="315" src="https://www.youtube.com/embed/ylIOZ8FQRMY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

본 포스트는 위 동영상을 글로 요약한 버전입니다. 그리고 이 영상은 제 <a href="https://www.youtube.com/channel/UCNdk6BMd8bTtCpngkBxA4ow"><b>Youtube</b></a>에 있는 강의입니다.

## 순차 데이터 혹은 시계열 데이터
우리가 다루는 데이터는 이미지들처럼 따로 봐도 되는 data들이 있고 시간순서대로 연관지어 봐야하는 data들이 있습니다.
날씨를 예로 들어 볼까요? 지금 창 밖에 비가 엄청 내리고 있다고 가정해보죠. 그럼 10분뒤에도 비가 올까요? 아마 여러분들은 창 밖에 비가 쏟아지는 걸 보면서 10분뒤에 나가실 때 비가 올 것을 예측하고 우산을 챙기시겠죠.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615725-2721c100-d8c2-11ea-9294-75d7cfc2c44b.PNG">
</figure>
이처럼 딥러닝에서 다루는 데이터들 중엔 시간을 연관지어 생각해야 하는 경우가 있습니다. 이런 데이터를 순차 데이터(sequential data) 혹은 시계열 데이터라고 부릅니다. 순차 데이터에는 날씨정보 말고도 <b>speech</b>도 포함됩니다. 문맥을 파악하기 위해선 이 전에 무슨 말을 했는지 기억해놓아야 하기 때문이죠. RNN은 대부분 speech data를 처리하기 위해 사용됩니다.

## RNN이 탄생한 이유
이런 순차 데이터는 기존 Forward Neural Network으로 처리하기 힘들었습니다. 그 이유는 그림에서 보시는 것처럼 Forward Neural Network는 직진밖에 못하는 네트워크였기 때문입니다. 반면에 RNN은 Hidden Layer에서 자기 자신으로 순환하는 구조입니다. 이것이 바로 RNN이 탄생한 이유이죠.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615728-27ba5780-d8c2-11ea-8771-9a19d1518323.PNG">
</figure>

## RNN의 단점
RNN 덕분에 sequential data를 처리할수 있게 되었습니다. 그런데 RNN에는 치명적 단점이 있었는데 그것은 바로 <b>'Vanishing gradient problem'</b> 이었습니다. target값과 예측값의 오류를 줄이는 방향으로 가중치를 업데이트 해주는 backpropagation을 진행하다보면 기울기가 0으로 수렴되어 버리는 현상입니다. 그럼 현재 모델의 성능이 좋든 나쁘든 더 이상 학습이 무의미해지겠죠.

<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615731-2852ee00-d8c2-11ea-8cd5-c70f4b8c9cad.PNG">
</figure>

이렇게 문장이 길어질수록, 신경망이 깊어질수록 한 없이 약해지는 RNN 구조였습니다...ㅠㅠ
그런데 이러한 단점을 극복하기 위해 RNN을 업그레이드 시킨 네트워크가 탄생했는데, 그것은 바로 다음 장에서 설명해드릴 <b>LSTM</b>입니다!

## Next
'수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN) 2장' 에서는 LSTM에 대해 소개해드리겠습니다.
[Next](https://akfmdl.github.io//ai_lstm_history/){: .btn}