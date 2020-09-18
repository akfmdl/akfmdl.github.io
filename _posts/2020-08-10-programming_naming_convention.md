---
layout: post
title:  "[프로그래밍] 네이밍 컨벤션(feat. 변수명 잘짓기)"
date:   2020-08-10
excerpt: "Naming convention for programmers"
feature: https://github.com/amueller/word_cloud/raw/master/examples/parrot_new.png
tag:
- PROGRAMMING
comments: true
---

특정 프로그래밍 언어를 한정짓지 않은 general 네이밍 규칙을 위한 글입니다.

## 네이밍 종류
* UpperCamelCase = PascalCase
  * 모든 단어를 대문자로 표기하는 기법  
    예) ClassName
  * 고유명사나 호칭을 가리킬 때 사용
  * 클래스가 프로그래밍에서 가장 주요하고 높은 위치에 있기 때문에 이 방식을 사용
  <figure>
	<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/CamelCase.svg/1280px-CamelCase.svg.png" width=100 height=100>
  </figure>
* lowerCamelCase
  * 이름에서도 알 수 있듯이 첫 문자는 소문자로 적고 다음부터는 대문자로 적는 기법  
   예) className
  * 함수나 변수는 동작을 시키는 명령어 개념이므로 이 방식 사용
* snake_case
  * 각 단어의 사이를 언더바_로 구분해주는 표기법  
    예) class_name
* Hungarian notation(헝가리안 표기법)
  * 이름 앞에 변수의 타입을 접두어로 넣어주는 표기법  
  * C++에서 변수 이름 지을 때 변수유형을 나타내기 위해서 썼던 것 같음  
    예) boolean형 변수명을 지을 때 bInitialized, string형 파일 이름 저장 변수 naming : strFileName
* 모두 대문자
  * 상수는 모두 대문자로 쓰고 '_'로 단어를 연결  
    예) static int PERSON_MAX = 10;
* 모두 소문자
  * 패키지와 모듈을 쓸 때  
    예) import matplotlib.pyplot as plt


## 변수 이름 잘 짓는 법
* 약어를 쓸 때는 보편성을 기준으로 정하기  
  * 변수 temp를 굳이 temporary로 쓰기 않듯이
* 중요한 단어를 앞에 쓰기
  * totalVisitor, totalRegister 와 같은 변수들이 있을 경우, 검색시 Visitor나 Register를 검색하지 total을 검색하지 않는다.
* 좋은 변수명에는 주석이 없다
  * 좋은 예
	```
	int screenHeightMax = 480
	classifyUserAndReturnClass()
	```
  * 안 좋은 예
    ```
	// 스크린 최대 높이를 480으로 지정함
	int h = 480
	// 사용자 유형을 분류해서 등급 값을 리턴함
	levelUser()
	```

---------
> 중요한 네이밍 규칙들을 데이터로 증명한 사이트  
https://brunch.co.kr/@goodvc78/12

> Python Word Cloud Package
https://github.com/amueller/word_cloud/raw/master/examples/parrot_new.png

> 코드를 자동으로 highlighting 해주는 사이트  
https://colorscripter.com/

> 그외 ref  
https://ko.wikipedia.org/wiki/%EB%82%99%ED%83%80_%EB%8C%80%EB%AC%B8%EC%9E%90
http://guswnsxodlf.github.io/camelcase-pascalcase-snakecase  
https://justmakeyourself.tistory.com/entry/python-comment  
위키북스의 개발자의 글쓰기