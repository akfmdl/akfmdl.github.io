---
layout: post
title:  "컴퓨터는 프로그램을 어떻게 실행시키는 걸까?"
date:   2021-05-18
excerpt: "How do computers run programs?"
feature: https://user-images.githubusercontent.com/31917080/118598847-b4972780-b7e9-11eb-8982-d35385809f0b.JPG
tag:
- PROGRAMMING
comments: true
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/UXDhcUi7_co" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

본 포스트는 위 동영상을 글로 요약한 버전입니다. 그리고 이 영상은 제 <a href="https://youtu.be/UXDhcUi7_co"><b>Youtube</b></a>에 있는 강의입니다.

---

컴퓨터는 프로그램을 어떻게 실행시키는 걸까? 컴알못과 함께 알아보도록 해요.

## 컴알못 소개
* 이름 : 컴알못
* 직업 : 소프트웨어 엔지니어
* 직급 : 신입사원(2년차)
* 성격 : 호기심이 많음
* 특징 : 시키는 일은 뭐든 열심히 하는 편, 컴퓨터에 대해 잘 알지 못함

## 알못이는 오늘도 코딩을 한다
그렇게 오늘도 시켜서 하는 코딩을 열심히 하던 도중, 알못이는 문득 궁금해졌어요.

* 내가 지금 하루 종일 컴퓨터 앞에서 뭐하는 걸까?
* 왜 내가 프로그래밍을 하면 이 착한 컴퓨터는 작성한대로 실행시켜주는 걸까?
* 이게 어떻게 동작하는 걸까?

그래서 알못이는 자신의 사수인 머대리님을 찾아가서 물었어요.
![슬라이드4](https://user-images.githubusercontent.com/31917080/118598854-b5c85480-b7e9-11eb-82f2-f5a95223c662.JPG)

사수인 머대리님의 간단한 대답에 알못이는 오히려 궁금한 것들이 더 많이 생겼어요.
![슬라이드5](https://user-images.githubusercontent.com/31917080/118598855-b5c85480-b7e9-11eb-874e-f064c978a459.JPG)

하지만 한꺼번에 물어보면 싫어하실까봐 하나씩 물어보기로 결정했어요.

## 프로그램을 누가, 어떻게, 왜 번역하는가?
![슬라이드6](https://user-images.githubusercontent.com/31917080/118598857-b660eb00-b7e9-11eb-969f-c9a07afc7352.JPG)
![슬라이드7](https://user-images.githubusercontent.com/31917080/118598859-b660eb00-b7e9-11eb-9d66-3ee145ef4afc.JPG)
![슬라이드8](https://user-images.githubusercontent.com/31917080/118598862-b6f98180-b7e9-11eb-825e-e8451307e117.JPG)
스크립트 언어는 소스 코드를 실행 시키면 인터프리터가 한줄 한줄씩 번역 및 실행시키고, 컴파일 언어는 소스 코드를 한꺼번에 번역해서 실행시키지.
![슬라이드9](https://user-images.githubusercontent.com/31917080/118598863-b6f98180-b7e9-11eb-80d5-692f5906f1e8.JPG)

## 프로그램은 어디에, 왜 저장하는가?
![슬라이드10](https://user-images.githubusercontent.com/31917080/118598865-b7921800-b7e9-11eb-91d8-a6d4a5f0320b.JPG)
![슬라이드11](https://user-images.githubusercontent.com/31917080/118598867-b7921800-b7e9-11eb-9184-9204d550d69b.JPG)
추가로 주메모리와 레지스터 사이엔 캐시 메모리도 존재하지
![슬라이드12](https://user-images.githubusercontent.com/31917080/118598868-b82aae80-b7e9-11eb-92b9-c2b0d432464f.JPG)
![슬라이드13](https://user-images.githubusercontent.com/31917080/118598870-b8c34500-b7e9-11eb-9c14-21b0c5b8a1dc.JPG)
냉장고는 집에 있어서 먹고 싶은 게 있을 때 바로바로 꺼낼 수 있지만 넣을 수 있는 음식의 개수는 가장 한정적이야.

편의점은 냉장고보단 물건이 들어갈 공간이 더 많지만 물건을 가져오려면 시간이 좀 더 걸려.

마트는 편의점보다 물건이 더 다양하고 많지만 훨씬 멀리 있고,
물류창고는 개인이 접근하기로 어렵고 물건을 사지 못해. 도매업자만 물건을 떼올 수 있지.

![슬라이드14](https://user-images.githubusercontent.com/31917080/118598874-b95bdb80-b7e9-11eb-8116-fd080cbbc9ed.JPG)

## 번역된 프로그램을 누가 어떻게 실행하는가?
![슬라이드15](https://user-images.githubusercontent.com/31917080/118598877-b9f47200-b7e9-11eb-8ac9-7e65edd44fc1.JPG)
머대리가 바빠서인지 CPU의 대한 질문을 회피하자, 알못이는 컴퓨터 공학 출신 컴과장님을 찾아갔어요.

## CPU가 어떻게 프로그램을 실행시키나?
![슬라이드16](https://user-images.githubusercontent.com/31917080/118598879-ba8d0880-b7e9-11eb-9b22-7a3c44802a47.JPG)
컴과장님은 알못이가 갑자기 무슨 바람이 들었나 생각했지만 친절하게 가르쳐주고 싶었어요.
![슬라이드17](https://user-images.githubusercontent.com/31917080/118598882-ba8d0880-b7e9-11eb-894b-79ad8ea3516c.JPG)
![슬라이드18](https://user-images.githubusercontent.com/31917080/118598884-bb259f00-b7e9-11eb-8381-d39d3ae106fd.JPG)
![슬라이드19](https://user-images.githubusercontent.com/31917080/118598888-bb259f00-b7e9-11eb-8ddf-a4c7c8772d54.JPG)
![슬라이드20](https://user-images.githubusercontent.com/31917080/118598889-bbbe3580-b7e9-11eb-9315-d1feb2eb1c32.JPG)
성격이 급한 알못이는 아직도 CPU 동작원리를 모르겠다면서 징징댔어요.

## CPU의 구성요소
![슬라이드21](https://user-images.githubusercontent.com/31917080/118598891-bbbe3580-b7e9-11eb-9e82-9df7e6c02631.JPG)
![슬라이드22](https://user-images.githubusercontent.com/31917080/118598892-bc56cc00-b7e9-11eb-990a-4777c5071ed6.JPG)

## 프로그램 카운터
프로그램을 실행하면 제어장치가 먼저 프로그램 카운터라는 레지스터를 이용해서 명령어가 담긴 메모리의 주소 값을 찾아.  
메모리는 집이 빈틈없이 늘어선 거리와 같은데 제어장치 안에 있는 프로그램 카운터라는 애가 돌아다니면서 쪽지 찾기를 해.  
각 집에는 명령어가 담긴 쪽지가 있을 수도 있고 없을 수도 있는데, 명령어가 담긴 쪽지를 찾으면 그 집의 주소를 적어놔.  
그렇게 찾은 쪽지는 메모리 주소 레지스터, 메모리 데이터 레지스터, 명령어 레지스터, 어큐뮬레이터를 통해 이동되고, 마침내 산술 논리 장치(ALU)가 연산을 마친 후 다시 빈 집에 결과가 적힌 쪽지를 보관해
![프로그램 카운터](https://user-images.githubusercontent.com/31917080/118604460-283c3300-b7f0-11eb-8260-1cef61988970.png)
![슬라이드23](https://user-images.githubusercontent.com/31917080/118598893-bc56cc00-b7e9-11eb-882e-ef2bbfedc5a6.JPG)

## 레지스터랑 프로그램 카운터란?
![슬라이드24](https://user-images.githubusercontent.com/31917080/118598894-bcef6280-b7e9-11eb-996a-9ea9605c107a.JPG)
계속되는 컴알못의 질문에 컴과장님은 지쳐버렸고, 옆에서 흐뭇하게 바라보던 전자공학 출신 전부장님이 나섰어요.

![슬라이드25](https://user-images.githubusercontent.com/31917080/118598897-bcef6280-b7e9-11eb-806c-a26c6d7dfeca.JPG)
![슬라이드26](https://user-images.githubusercontent.com/31917080/118598898-bd87f900-b7e9-11eb-836c-f3c0a7a4d956.JPG)
NOT GATE는 이 Truth Table에 나와있는 것처럼 무조건 입력 값의 반대의 출력을 내보내는 회로야. 자 밑에 Feed Back 회로를 살펴보자. 이 회로는 출력을 다시 입력으로 되먹임하는 회로인데, 이전 출력 값이 0이라고 치자. 그럼 출력이 입력이 되고, 그 입력이 다시 출력으로 나오는 무한 반복의 원리로 기억기능이 구현되는 것이지. 그런데 이렇게 간단한 걸로는 뭘 만들 수 없잖아?

![슬라이드27](https://user-images.githubusercontent.com/31917080/118598900-bd87f900-b7e9-11eb-93dc-95d8e69e51d2.JPG)
NAND Gate는 Truth Table에 나와있는 것처럼 둘 다 1일 경우에만 0이고 나머지는 모두 1을 출력해줘.
그리고 플립플롭의 종류에도 회로의 구성에 따라 여러 가지가 있는데, CPU의 레지스터는 D 플립플롭이라는 회로를 써.

## NOT Gate와 NAND Gate
![슬라이드28](https://user-images.githubusercontent.com/31917080/118598902-be208f80-b7e9-11eb-94e1-b64b69799dcb.JPG)
회로까지 설명해주니까 도망치고 싶었던 알못이는 급하게 자리를 뜨려했지만 실패했어요.

![슬라이드29](https://user-images.githubusercontent.com/31917080/118598904-be208f80-b7e9-11eb-985f-0b2b7322360f.JPG)
![슬라이드30](https://user-images.githubusercontent.com/31917080/118598906-beb92600-b7e9-11eb-994e-20e811c89129.JPG)
![슬라이드31](https://user-images.githubusercontent.com/31917080/118598907-beb92600-b7e9-11eb-89c9-e96315e5b6a8.JPG)
![슬라이드32](https://user-images.githubusercontent.com/31917080/118598908-bf51bc80-b7e9-11eb-94de-24e5932a91c5.JPG)
![슬라이드33](https://user-images.githubusercontent.com/31917080/118598910-bf51bc80-b7e9-11eb-9850-959eb420cf5e.JPG)
![슬라이드34](https://user-images.githubusercontent.com/31917080/118598912-bfea5300-b7e9-11eb-92be-881e104994fd.JPG)
![슬라이드35](https://user-images.githubusercontent.com/31917080/118598913-bfea5300-b7e9-11eb-8020-f937d7cdc4a0.JPG)
![슬라이드36](https://user-images.githubusercontent.com/31917080/118598914-c082e980-b7e9-11eb-8de4-47258e92fefe.JPG)
![슬라이드37](https://user-images.githubusercontent.com/31917080/118598916-c082e980-b7e9-11eb-9e3e-63f66e0315a2.JPG)
![슬라이드38](https://user-images.githubusercontent.com/31917080/118598917-c11b8000-b7e9-11eb-903b-facc8cfee5ff.JPG)

## CPU와 RAM을 구성하는 소자들
![슬라이드39](https://user-images.githubusercontent.com/31917080/118598918-c11b8000-b7e9-11eb-978b-bcd0b176289d.JPG)

## 사람이 10진법을 사용하는 이유
![슬라이드40](https://user-images.githubusercontent.com/31917080/118598922-c24cad00-b7e9-11eb-98c3-d18b5d8acbd4.JPG)
이쯤되니 직원들이 하나 둘씩 모여 대표님까지 구경하게 되었습니다. 그럼에도 불구하고 알못이는 지치지도 않는지 질문을 이어나갔어요.

그런데 생각해보니까.. 컴퓨터는 2진법을 사용하는데, 왜 저희는 10진법을 사용 하는 걸까요?

몇 분간 침묵이 이어지다가 철학과 출신 대표님이 
![슬라이드41](https://user-images.githubusercontent.com/31917080/118598924-c2e54380-b7e9-11eb-8647-5a86f90df049.JPG)
라고 말하자 모두 수긍을 했어요. 알못이는 수긍은 했지만 찜찜한 게 남았는지 그럼 왜 컴퓨터는 10진수를 안쓰고 2진수를 쓰나요? 손가락이 없어서 그런가요? 라고 따지듯이 질문을 했어요.

그러자, 대표님은 트랜지스터를 설명해주시면서,
![슬라이드43](https://user-images.githubusercontent.com/31917080/118598928-c37dda00-b7e9-11eb-91eb-fb32f19030c1.JPG)
자, 보자. 아까 전부장이 모든 회로는 기본적으로 transistor로 이루어져 있다고 했지? 저항은 무시하고, 신호를 조절하고 제어하는 가장 기본적인 장치가 이 트랜지스터거든. 트랜지스터는 전류가 지나가는 길의 문을 전압을 이용해 열고 닫아주는 `스위치` 역할을 해

![슬라이드44](https://user-images.githubusercontent.com/31917080/118598930-c4167080-b7e9-11eb-8b0a-5de524014347.JPG)
숫자를 0부터 9까지 표현한다고 치자. 너가 말했던 것처럼 전류의 세기로 0~1A사이는 1, 1~2A는 2로 정하려면 전류를 스위치로 미세하게 조정할 수 있어야 하지.  
반면에 2진법으로 0부터 9까지 표현하기 위해서는 4개의 스위치가 필요하지만 미세 조정할 필요가 없어. 왜냐면 각 스위치별로 바로 이 문턱값 이상의 힘만 주면 되기 때문이지. 그러면 각 자리수별로 조합해서 10진수로 변환하기만 하면 되거든.

![슬라이드45](https://user-images.githubusercontent.com/31917080/118598933-c4167080-b7e9-11eb-88e8-a5dfbe917f36.JPG)
이건 비커에 물을 부어서 눈금을 조절하는 거랑 비슷해. 8이라는 숫자를 만들기 위해 10L짜리 비커를 미세하게 계량하는 것과 1L짜리 비커 4개를 대충 계량하는 것 중에 어떤 게 쉬울지 생각해봐. 대신, 모든 건 컴퓨터 입장에서 생각해야 한단다.

![슬라이드46](https://user-images.githubusercontent.com/31917080/118598934-c4af0700-b7e9-11eb-88e7-0947e048e86e.JPG)
이렇게 모든 깨달음을 얻은 직원들은 컴알못 때문에 못한 업무를 하느라 행복하게 야근을 하게 되었답니다. 이상 컴알못 이야기 끝~



> ref  
한 권으로 읽는 컴퓨터 구조와 프로그래밍(조너선 스타인하트)