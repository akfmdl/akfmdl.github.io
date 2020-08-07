---
layout: post
title:  "수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN) 2장"
date:   2020-08-07
excerpt: "LSTM의 탄생"
feature: http://colah.github.io/posts/2015-08-Understanding-LSTMs/img/LSTM3-chain.png
tag:
- AI
comments: true
---
<iframe width="560" height="315" src="https://www.youtube.com/embed/ylIOZ8FQRMY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

본 포스트는 위 동영상을 글로 요약한 버전입니다. 그리고 이 영상은 제 <a href="https://www.youtube.com/channel/UCNdk6BMd8bTtCpngkBxA4ow"><b>Youtube</b></a>에 있는 강의입니다.

## LSTM이란?
LSTM을 구글에 쳐보면 아래와 같이 '롱 숏텀 메모리..장단기 기억 어쩌구 ...' 라고 나옵니다. 아니 딥러닝 네트워크가 무슨 반도체도 아니고 메모리 얘기가 왜 나와..ㅠㅠ 듣기만 해도 뭔소린지 모르겠죠? 제 설명을 다 듣고나면 왜 이렇게 이름을 지었는지 알게 되실거에요! 차근차근 따라와주세요!  
라고 자신있게 말씀드렸지만.. 아래 구조를 보시면 도망가고 싶으실겁니다. (저도 그랬으니..) 가실 땐 가시더라도 제 설명 좀 듣고 가세요..!
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615742-2be67500-d8c2-11ea-96ee-310b5430139e.PNG">
</figure>
위에 있는 구조를 보시면 Forget Gate, Input Gate, Output Gate가 있습니다. LSTM은 이 gate들을 조합하여 불필요한 기억을 지우고, 기억해야할 것들을 정한다고 합니다. 지금은 구조에 대해 이해가 잘 안가셔도 게이트들을 이용해서 입력을 지우거나 저장할 수 있어서 이름에 'memory'가 들어가는구나! 라고 이해하시면 될 것 같습니다.

## RNN vs LSTM 구조 비교
RNN과 LSTM는 다음과 같은 차이점 들이 있습니다.  
* 차이점 1 : 이전 Cell에서 받는 입력 개수와 다음 Cell로 출력되는 개수가 다르다  
RNN은 입력 1 : 출력 1  
LSTM은 입력 2 : 출력 2
* 차이점 2 : 새로운 입력 값인 Xt와 이전 값이 결합되어 뻗어가는 layer의 개수가 다르다  
RNN은 1개  
LSTM은 4개
* 차이점 3 : tanh 함수만 사용한 RNN에 비해 LSTM은 sigmoid(σ) 함수와 tanh 두개를 사용했다. 이 함수들에 대해서는 다다음장에서 설명드리겠습니다.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615746-2c7f0b80-d8c2-11ea-971f-f09cca6ed5db.PNG">
</figure>

## Gate들의 역할
LSTM의 구조를 설명드리기 전에 짚고 넘어가야할 부분입니다. RNN과 크게 다른점이 LSTM에는 gate가 있다는 점인데 3개의 gate들은 각각 아래와 같은 역할을 합니다.
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615747-2c7f0b80-d8c2-11ea-9a20-2b158662a0bd.PNG">
</figure>

## sigmoid & tanh의 역할
sigmoid함수는 활성화 함수의 한 종류입니다. 활성화 함수가 뭔지 잘 모르시겠다면 자세히 설명해 드린 포스트가 있으니 <a href=""><b>'여기'</b></a>를 참고하시기 바랍니다.  
tanh의 정식명칭은 Hyperbolic Tangent입니다. 이 함수 역시 sigmoid와 마찬가지로 활성화 함수입니다.  
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615749-2d17a200-d8c2-11ea-91c1-70984cb18458.PNG">
</figure>
왜 두 가지 활성화 함수나 사용하는 걸까요? 두 함수의 큰 차이점은 sigmoid함수를 씌우면 0 또는 1의 값을 내보내는 반면에 tanh함수를 씌우면 -1에서 1사이의 값을 내보냅니다.   

회로에서 0 또는 1의 값만 출력하는 소자는 <b>스위치</b>로 사용하는데 LSTM에서 sigmoid 함수도 그런 역할을 합니다. '정보를 저장할지 말지' 이런식의 이분법적인 역할을 하는 것이죠. 반면에 -1 ~ 1사이의 값을 내보내는 tanh함수는 scale역할을 하게 됩니다. '정보를 얼마나 저장할지' 이런식으로 말이죠.

## LSTM의 원리
드디어 LSTM이 어떻게 메모리 역할을 하는지, Vanishing gradient를 어떻게 극복하는지 설명드릴 수 있게 되었습니다. 

아래 그림을 보시는것처럼 새로운 Input값인 X<sub>t</sub>와 이전 hidden state인 h<sub>t-1</sub>이 만나서 4개의 layer로 뻗어나가게 됩니다. 각각의 layer들은 sigmoid 함수나 tanh함수를 만나서 활성화 된 값으로 출력이 되고 다른값과 곱해지거나 더해집니다.  

전체적인 Flow를 좀 더 쉽게 보고싶으시면 맨 위에 있는 제 유튜브 강의를 보시기 바랍니다. ppt의 고급진 애니메이션 기능을 사용하여 화려하게(?) 설명이 되어있답니다. 글로 설명하긴 한계가 있네요..영상으로 보면 훨씬 더 이해가 잘 가실 겁니다!!
<figure>
	<img src="https://user-images.githubusercontent.com/31917080/89615751-2db03880-d8c2-11ea-93fd-315231aaa657.PNG">
</figure>

어쨌든, LSTM은 이렇게 선택적으로 잊거나 저장하는 원리로 Vanishing gradient 문제를 극복할 수 있게 되는 겁니다. 

## Before
'수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN) 1장' 에는 LSTM의 조상인 RNN에 대한 설명이 있습니다.  
go to -> [Before](https://akfmdl.github.io//ai_rnn_history){: .btn}

## Next
'수식없이 RNN 식구들 소개하기(LSTM, GRU, DRNN) 3장' 에서는 GRU와 DRNN에 대해 소개해드리겠습니다.  
go to -> [Next](https://akfmdl.github.io//ai_gru_drnn_history){: .btn}