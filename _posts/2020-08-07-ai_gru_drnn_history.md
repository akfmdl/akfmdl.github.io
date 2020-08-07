---
layout: post
title:  "수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN) 3장"
date:   2020-08-07
excerpt: "GRU, DRNN의 탄생"
feature: https://blog.exxactcorp.com/wp-content/uploads/2019/03/Recurrent-Networks.png
tag:
- AI
comments: true
---
<iframe width="560" height="315" src="https://www.youtube.com/embed/ylIOZ8FQRMY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

본 포스트는 위 동영상을 글로 요약한 버전입니다. 그리고 이 영상은 제 <a href="https://www.youtube.com/channel/UCNdk6BMd8bTtCpngkBxA4ow"><b>Youtube</b></a>에 있는 강의입니다.

## GRU의 탄생
GRU는 LSTM만 잘 이해하셨다면 아래 슬라이드에 있는 내용처럼 별거 없습니다. 그냥 LSTM보단 빠르지만 성능은 비슷한 네트워크구나~ 라고 이해하시면 될 것 같습니다.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615758-2db03880-d8c2-11ea-932c-f9a48bf3a7df.PNG">
</figure>

## DRNN의 탄생
DRNN도 별거 없습니다. 이 친구는 자기 식구들인 RNN or LSTM or GRU를 엄청 쌓아서 성능을 높인다는 네트워크거든요.  
RNN과 LSTM만 이해해도 이렇게 응용이 가능하다는 게 기분 좋지 않나요?
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615760-2e48cf00-d8c2-11ea-97d4-d01d3850c6a4.PNG">
</figure>
DRNN은 다음과 같이 긴 문장을 제대로 예측을 못하는 RNN 식구들을 위해 탄생한 알고리즘입니다.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615761-2ee16580-d8c2-11ea-9b8d-42462c45f4a4.PNG">
</figure>
그런데 엄청 쌓아서 성능을 어떻게 높인다는 걸까요?

CNN에서 deep하게 layer를 쌓을 경우 아래와 같은 이점이 있습니다.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615762-2ee16580-d8c2-11ea-911f-8688e1b89afa.PNG">
</figure>
DRNN도 이와 비슷한 이점을 얻을 수 있는데요.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615764-2f79fc00-d8c2-11ea-8695-eab5f5167780.PNG">
</figure>
이미 LSTM과 GRU가 Vanishing gradient 문제를 어느정도 극복한 알고리즘이기 때문에 얘네들을 deep하고 wide하게 만들어 DRNN으로 사용하게 된다면 정말 좋겠죠?

<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615766-2f79fc00-d8c2-11ea-93c4-8819715b8835.PNG">
</figure>
우린 '수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN)' 시리즈에서 RNN에 대한 내용을 공부했는데 어떠셨나요? 내용이 어려웠나요? 아무쪼록 여러분들에게 도움이 되었으면 합니다.

## Before
'수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN) 2장' 에는 GRU의 조상인 LSTM에 대한 설명이 있습니다.  
go to -> [Before](https://akfmdl.github.io//ai_lstm_history){: .btn}