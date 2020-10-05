---
layout: post
title:  "파이썬의 특징과 병렬 프로그래밍 with GIL"
date:   2020-09-17
excerpt: "python parallel programming"
feature: https://miro.medium.com/max/700/1*7E8FmqFW488FASvN0nNcdQ.png
tag:
- PROGRAMMING
comments: true
---

파이썬의 특징을 알아보고 그 특징에 맞는 병렬 프로그래밍의 여러 가지 방법론에 대해 설명드리겠습니다.

## 순서
1. Python 구현체 종류
2. GIL(Global Interpreter Lock)이란?
3. GIL의 필요성
4. Python 병렬 프로그래밍 방법  
---------

## Python 구현체 종류
Python은 언어의 한 종류 일뿐, Python 언어를 바이트 언어로 해석하고 메모리 관리자를 하는 역할을 하는 것을 바로 구현체라고 합니다.
보통 말하는 Python은 C로 구현되었으며, Cpython이라는 구현체를 사용해 코딩을 하게 됩니다.
* Cython : 파이썬을 C언어로 컴파일해주는 구현체
* Jython : 자바로 구현
* IronPython : C#으로 구현
* PyPy : 파이썬으로 구현된 파이썬. 아예 JIT 컴파일러를 사용해서 파이썬을 처음부터 다시 구현했다고 합니다. 왜 이런 짓을 했을까요? 기존 Cpython의 단점을 보완하여 성능을 높이기 위함이라고 합니다.
<img src="https://user-images.githubusercontent.com/31917080/93556412-a58a7c00-f9b3-11ea-95a5-e49f57fd15cf.png">

### Cython의 특징
사이썬은 파이썬 코드를 C언어로 컴파일을 하는 특성을 갖고 있습니다. 이를 통해 같은 매트릭스 크기의 연산시 C와 같은 수행 성능을 낸다는 연구결과도 있습니다.
또한 설치가 쉽습니다.
![image](https://user-images.githubusercontent.com/31917080/93732672-52136a80-fc0d-11ea-8629-3561b7668d89.png)

### pypy의 특징
앞에서 설명해드린 Cython에 크게 밀리지 않을 정도로 속도가 빠른 파이썬 구현체인 pypy은 역시 setup이 쉽고 기존 Cpython 코드와 높은 호환성을 갖고 있기 때문에 기존 Python을 이용해서 코드를 짜신 분들이 쉽게 입문할 수 있습니다. 그래서 pypy를 먼저 사용해 속도를 비교한뒤 Cython을 적용하는 것을 추천하는 분도 있습니다.  
그리고 pypy의 큰 특징인 JIT컴파일러는 인터프리터의 단점을 보완하기 위해 도입된 것입니다. 처음에는 인터프리터 방식으로 실행하다가 어느 시점에 바이트코드 전체를 컴파일하여 네이티브 코드로 변경하고, 이후에는 더 이상 인터프리팅을 하지 않습니다. 캐시 메모리에 보관된 네이티브 코드를 바로바로 실행하는 거죠. 이렇게 실행하는 게 하나씩 인터프리팅하는 CPython보다 당연히 빠르겠죠?
<img src="https://user-images.githubusercontent.com/31917080/93556467-bf2bc380-f9b3-11ea-814f-de69d1c69cae.png">

### CPython, Cython, pypy의 공통점
앞에서 설명해드린 CPython, Cython, pypy의 공통점은 바로 GIL이 있는 인터프리터라는 것입니다.
<img src="https://user-images.githubusercontent.com/31917080/93556482-ca7eef00-f9b3-11ea-8f42-3c34ed6d6e42.png">

## GIL(Global Interpreter Lock)이란?
### GIL의 정의 : 여러 스레드를 사용할 경우, 단 하나의 스레드만 접근을 허용 하는것

GIL의 정의에 스레드가 있네요? 스레드의 정의는 다음과 같습니다.
> 프로세스가 할당 받은 자원을 이용하는 실행의 단위

여기서 프로세스는 무엇일까요?
> 컴퓨터에서 연속적으로 실행되고 있는 프로그램

둘 사이에 뭔가 연관이 있는 것 같죠?  
아래 그림에서도 볼 수 있듯이 스레드는 프로세스와는 달리 stack영역을 제외한 나머지 부분을 다른 스레드들과 공유하고 있습니다.
<img src="https://user-images.githubusercontent.com/31917080/93556518-dcf92880-f9b3-11ea-900c-62451ef457be.png">

### 멀티 프로세싱 vs 멀티 스레딩
앞에서 GIL이란 '여러 스레드를 사용할 경우, 단 하나의 스레드만 접근을 허용 하는것' 이라고 했죠? 여기서 여러 스레드를 사용한다는 것을 전문용어로 '멀티스레딩'이라고 합니다.  
아래 그림은 멀티 프로세싱과 멀티 스레딩 구조의 차이를 보여주는데요. 프로세스는 여러 개 있어도 공유하는 자원이 없죠? 반면에 멀티 스레딩은 아까도 보셨듯이 stack영역을 제외한 나머지 자원은 서로 공유하고 있습니다.
<img src="https://user-images.githubusercontent.com/31917080/93556537-e97d8100-f9b3-11ea-9539-8984c1bc881d.png">
GIL의 정의에서 알 수 있듯이, 여러 스레드를 사용할 경우, 즉 멀티 스레딩을 할 경우 단 하나의 스레드만 접근을 허용하는 것입니다.  
> 다시 말해 GIL은 멀티 프로세싱에는 해당하는 바가 없으며 멀티 스레딩에 해당하는 것입니다.

## GIL의 필요성
### 왜 단 하나의 스레드만 접근을 허용하도록 제한했던 것일까?
'Reference counting' 때문입니다. C나 C++은 한줄씩 해석하는 인터프리터 언어인 Python과 달리 코드 통째로 해석합니다.
변수 크기도 프로그래머가 미리 지정해놓기 때문에 컴파일 이후에 메모리에 해당 값이 바로 박히지만 파이썬에서는 힙에 int형 object를 만들어 놓고 각 변수들이 그것을 가르키는 형태입니다.  
C나 C++처럼 프로그래머가 메모리를 할당하거나 해제할 필요가 없는 이유는 Garbage Collector 덕분인데 다음 단계에서 더 자세히 살펴보죠.
<img src="https://user-images.githubusercontent.com/31917080/93556570-0023d800-f9b4-11ea-8dcf-e722dfd0f82d.png">

### Garbage Collector의 메모리 해제 과정
Garbage Collector의 메모리 해제 과정을 살펴보겠습니다. 참고로 stack의 메모리 해제 방식은 다음과 같습니다.
> Last In Frist Out방식  
마지막으로 입력된 자료가 제일 먼저 삭제 하는 방식

아래 그림을 봐주시기 바랍니다.  
함수 f2와 f1을 호출하는 main 함수로 이루어진 코드가 있습니다. 코드를 실행하면 stack memory안에 main -> f1 -> f2의 순으로 아래부터 쌓이게 됩니다. 실행이 끝나면 Last In Frist Out방식이기 때문에 위에서 부터 차례대로 해제하기 시작하겠죠? 그래서 f2 함수를 먼저 해제합니다. 그 다음 f1 함수를 해제할텐데요. f1함수의 변수 x가 없어짐에 따라 '10 int object'도 없어지게 됩니다. '10 int object'의 reference count가 0이 되기 때문이죠.  
마지막으로 main 함수가 모두 실행되면 모든 reference count가 0이 되므로 object 메모리들이 해제됩니다.
<img src="https://user-images.githubusercontent.com/31917080/93556592-0f0a8a80-f9b4-11ea-9a1f-99bc332d7430.png">

따라서, Reference Counting은 파이썬의 Garbage Collector가 메모리를 해제하는 방식이라고 생각하시면 됩니다.

### GIL이 존재하는 이유가 Reference Counting 때문이라고 말씀드렸는데, 왜일까요?  
아래 그림은 GIL이 없을 경우 멀티 스레딩 구조에서 Reference Counting을 사용할 경우 발생할 수 있는 일입니다.  
먼저 실행된 스레드 1이 Reference counting을 시작합니다.그런데 스레드 1과 같은 자원을 공유하고 있는 늦게 실행된 스레드 2가 그 x 변수에 접근합니다. 이미 스레드 1이 지우고 난 후에 말이죠. 병렬 프로그래밍을 하셨던 분이라면 이럴 경우 어떤 끔찍한 일이 발생할지 상상이 가시겠죠?  
이상적으로 강아지(스레드)가 사료(변수)를 1:1로 할당 받으면 얼마나 좋겠어요?
그런데 현실은 그렇게 녹록지 않았죠. 그래서 이걸 GIL로 막았다는 겁니다.
<img src="https://user-images.githubusercontent.com/31917080/93556632-23e71e00-f9b4-11ea-8dfe-80d5cb111dfd.png">

### 왜 Python에는 GIL이 있어야 했는가?
그래서 사람들이 따졌습니다.
* 변수를 스레드들이 동시 접근할 경우에만 lock을 걸면 되지 왜 굳이 그걸 global하게 막냐..
* 멀티 스레딩을 못하면 병렬처리는 어떻게 하냐..

등등..  
Python이 태동하던 시기에는 thread라는 개념이 없었을 당시였고, 쉽고 간결한 컨셉인 Python인지라.. C, C++과 차별성을 두고 싶었던 것 같습니다. 'C나 C++과 달리 Python은 알아서 효율적으로 관리해주니까 편하게 코딩할 수 있다' 라는 걸 강조하고 싶었겠죠.

지금보니 좀 노답이죠?
<img src="https://user-images.githubusercontent.com/31917080/93556645-2e091c80-f9b4-11ea-9ec2-db35e4816e67.png">
근데 GIL이 혜택을 보는 작업이 있긴 있다고 하는데요.

### I/O 작업이 많은 멀티스레딩 구조에서 진가(?)를 발휘하는 GIL
아래 그림을 보시면 Thread 1이 실행되고 있을 때 Thread 2에게 제어권을 주면 역시나 GIL답게 병렬 처리가 안되어 Thread 2만 수행하게 됩니다.  
그렇게 제어권을 받고 작업을 하던 Thread 2가 갑자기 I/O 작업으로 인해 블로킹이 발생하면 그 동안 다른 스레드로 제어권이 자동으로 넘어가서 일을 처리하기 때문에 전체적으로 봤을 때에는 효율적이라는 겁니다.  
![image](https://user-images.githubusercontent.com/31917080/93556666-3a8d7500-f9b4-11ea-9895-a5203fd7dd00.png)

근데 이마저도 어떤 쓰레드가 점유권을 가져 갈지는 거의 랜덤에 가깝다고 합니다.  
또한, 아까 설명드렸듯이 CPU 작업이 많은 멀티 쓰레딩에서는 파이썬이 효율적이지 않을 수 있다는 점을 알아두어야 합니다.

## Python 병렬 프로그래밍 방법
그렇다면 CPython은 병렬 처리를 할 수 없을까요? 당연히 있겠죠! 4가지 방법들을 소개해드립니다.
![image](https://user-images.githubusercontent.com/31917080/93563020-1173e100-f9c2-11ea-87f5-b78c2b99da48.png)

### 다른 Python 사용하기
만약 다른 Python을 사용해서 병렬 프로그램을 하겠다면 다음과 같이 GIL이 없는 파이썬 구현체들을 사용하면 됩니다.  
Jython은 자바로 구현한 파이썬이라고 말씀드렸잖아요? Jython이 GIL이 없는 이유는 jave garbage collector로 메모리를 관리하기 때문입니다. 
![image](https://user-images.githubusercontent.com/31917080/93556768-76283f00-f9b4-11ea-9c00-7b67ad30c13d.png)  
C#으로 작성된 IronPython은 .net garbage collector로 메모리를 관리합니다.  
이 둘의 공통점은 Python처럼 reference counting 방식으로 메모리를 관리하지 않습니다. 그래서 GIL이 없는 것이죠. 그럼 멀티스레딩도 가능하겠죠?
![image](https://user-images.githubusercontent.com/31917080/93556785-7de7e380-f9b4-11ea-8441-1e2b29397194.png)


### Multi-Processing 사용하기
파이썬은 기본적으로 ‘multiprocessing’이라는 라이브러리를 제공하여 멀티 프로세싱 기능을 제공하는데요.
다음과 같이 child process가 parent proces에 종속되어 있는 구조입니다.  
프로세스의 구조는 다음과 같이 공유 메모리가 없기 때문에 stack 메모리를 공유하는 스레드의 동시 접근을 제한하는 것과 상관없이 병렬처리가 가능합니다.
![image](https://user-images.githubusercontent.com/31917080/93562940-ed180480-f9c1-11ea-8936-b09cd5e8e0f1.png)

### 업무를 나누기
마지막으로 C로 구현된 라이브러리를 사용하는 방법인데요. 저희가 잘 알고 있는 numpy도 C로 구현되어 있어 상당히 빠르다고 합니다. 특히 멀티 프로세싱과 함께 사용한다면 좋은 성능을 보인다고 합니다.
![image](https://user-images.githubusercontent.com/31917080/93563059-205a9380-f9c2-11ea-9399-a15fc60c0c6c.png)

### 그냥 기다리기
그럼 그냥 기다리는게 최선일까요?  
Python의 창시자인 Guido van Rossum은 GIL에 대한 개선을 하고 싶은 사람들에게 이렇게 말했다고 합니다.  

> I’d welcome a set of patches into Py3k only if the performance for a single-threaded program (and for a multi-threaded but I/O-bound program) does not decrease.  
단일 thread 프로그램에서의 성능을 저하시키지 않고 GIL의 문제점을 개선할 수 있다면, 나는 그 개선안을 기꺼이 받아들일 것이다.

그리고 지금까지도 개선안은 없다고 합니다.
![image](https://user-images.githubusercontent.com/31917080/93563093-2c465580-f9c2-11ea-8664-338a01dbdd04.png)


## 마치며
파이썬은 C, C++에 비해 속도가 느리며 GIL이라는 단점이 있습니다. 하지만 그의 하지만 높은 생산성, 방대한 라이브러리와 툴들 때문에 포기할 순 없죠. 때문에 파이썬을 사용할 수 밖에 없다면 속도와 생산성 사이에서 적절한 'Trade off'를 해야한다는 것이 제 생각입니다.

## 부록(asyncio)
파이썬은 3.4버전부터 비동기적인 처리를 지원하는 asyncio 라이브러리를 제공하였습니다. 위 그림과 같이 이전 테스크를 기다려야 다음 테스트를 수행할 수 있는 동기적 처리에 반해, 비동기적 처리는 다른 테스크를 기다리지 않고 바로 수행이 가능합니다.  
이 라이브러리를 이용해 여러 개의 쓰레드를 사용해서 효율적인 동시 처리가 가능합니다. 단, 이 역시 I/O 작업을 할 때에만 해당합니다.

![image](https://user-images.githubusercontent.com/31917080/93563126-3d8f6200-f9c2-11ea-9c03-1d485a58f219.png)



> ref  
파이썬 병렬 프로그래밍(얀 팔라흐)  
http://masnun.rocks/2016/09/28/can-cython-make-python-great-in-programming-contests/  
https://dmtn-013.lsst.io/  
https://towardsdatascience.com/how-to-speed-up-your-python-code-d31927691012  
https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html  
https://leemoney93.tistory.com/25  
https://m.blog.naver.com/alice_k106/221566619995  
http://www.bnikolic.co.uk/blog/python-numerical-gil.html  
https://www.crocus.co.kr/1686  
https://devopedia.org/asynchronous-programming-in-python



