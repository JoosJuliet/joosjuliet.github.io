---
layout: post
section-type: post
title: "3주차 과제"
category: Java
tags: [ 'Java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  
3주차 : 연산자

전반적으로 정리 잘한 것
- https://velog.io/@uhan2/Java-Operator
- https://blog.baesangwoo.dev/entry/Live-Study-3%EC%A3%BC%EC%B0%A8-%EA%B3%BC%EC%A0%9C-%EC%97%B0%EC%82%B0%EC%9E%90
- https://whereishq.blogspot.com/2020/11/3.html
- https://leemoono.tistory.com/9
- https://yadon079.github.io/2020/java%20study%20halle/week-03

->https://b-programmer.tistory.com/226 무려... 바이트 코드도 열어보고 글도 그림 통해서 했다
-> https://github.com/yeGenieee/java-live-study/blob/main/%5B3%5DJava%20Live%20Study.md 언사인드 인트를 써서
예제 : 45와 25를 비트 논리 연산
이부


ita와 iter이게 단축어 sout



# 산술 연산자 (arithmetic)와 관계 연산자 (relational)
->https://blog.naver.com/hsm622/222150928707 직접 다 실행 해봄
- 보통 수학을 할 때 쓰는 연산자와 같다.
- 산술 연산자

```
+ 	- 	/ 	* 	% 	++ 	--
```
- 관계 연산자

```
== 	!= 	> 	< 	>= 	<=
```



# 비트 연산자 (bitwise)

```
& 	| 	^ 	~ 	<< 	>> 	>>>
AND	OR 	XOR	NOT			Zero-fill Rshift
```


## 비트 연산

### &.|,^ 연산
<img alt="success" src = "/images/2018-08-19-bit/bit_operation.png"/>

두 수 A,B를 비트 연산 하는 경우, 가장 뒷 자리 부터 하나씩 연산을 수행하면 된다.

A = 27    B = 83</br>
  = 11011   = 1010011</br>

A&B = 19, A|B = 91, A^B = 73

<img alt="success" src = "/images/2018-08-19-bit/27_83_bit_operation.png"/>


### ~ 연산
A = 83 = 1010011
~A = 10101100 *8bit*
A = 01010011 -> 10101100
*8bit여서 젤 앞에 0이 붙는다.*

~A = 11111111 11111111 11111111 10101100
*32bit*

자료형이 signed랑 unsinged에도 값이 달라진다.

### shift 연산(<<, >>)

#### <<
A << B (A를 왼쪽으로 Bbit만큼 민다.)
= A * 2**B

- 1 << 0 = 1
- 1 << 1 = 2 (10)
- 1 << 2 = 4 (100)
- 1 << 3 = 8 (1000)
- 1 << 4 = 16 (10000)
- 3 << 3 = 24 (11000)
- 5 << 10 = 5120 (1010000000000)

#### >>
A >> B (A를 오른쪽으로 Bbit만큼 민다.)
= A // 2**B

- 1 >> 0 = 1
- 1 >> 1 = 0 (0)
- 10 >> 1 = 5 (101)
- 10 >> 2 = 2 (10)
- 10 >> 3 = 1 (1)
- 30 >> 1 = 15 (1111)
- 1024 >> 10 = 1 (1)

## 비트 마스크
True/False 로 구분하는 것이다.
True이면 1놓고 False이면 0을 놓는 것이다.

- 570 = 2+(2**3)+(2**4)+(2**5)+(2**9)</br>
    = {1,3,4,5,9}</br>
    = 1000111010

### 포함 되어있는지 검사
0이 포함되어 있는지 궁금하면 0번째 비트를 1로 표현을 해주고 &연산을 하면 된다.

```
1000111010
&        1
-----------
         0
```
즉 x가 들어있는지 궁금함으로 x번째 비트만 1로 만들면 되니 쉬프트 연산을 하면된다.


그렇게 하면 판단 할 수 있는 이유는 and 연산은 둘중 하나라도 0이면 0 이기 때문이다.
둘다 1이여야만 나오기 때문에 위치를 알려준다.

- 0 포함 되어있는지 검사</br>
  570 & (2**0) = 570 & (1 << 0) = 0
- 1 포함 되어있는지 검사</br>
  570 & (2**1) = 570 & (1 << 1) = 2
- 2 포함 되어있는지 검사</br>
  570 & (2**2) = 570 & (1 << 2) = 0
- 3 포함 되어있는지 검사</br>
  570 & (2**3) = 570 & (1 << 3) = 8





# 논리 연산자
```
&& 	||	!
```





# instanceof
객체 instanceof 객체타입 == true
자녀객체 instanceof 부모타입 == true
부모객체 instanceof 자녀타입 == false

``` java
class Main {
    class Parent { }
    class Child extends Parent { }

    void run() {
        Parent parent = new Parent();
        Child child = new Child();

        System.out.println(parent instanceof Parent);   // true
        System.out.println(child instanceof Child);     // true

        System.out.println(child instanceof Parent);    // true
        System.out.println(parent instanceof Child);    // false
    }

    public static void main(String[] args) {
        Main main = new Main();
        main.run();
    }
}
```
- type ${variable} : primitive types에 사용

# assignment(=) operator
```
= 	+= 	-= 	*= 	/= 	%= 	<<= 	>>= 	&= 	^= 	|=
					            	|bitwise assignment operator|
```
- Comma operator (in for-loop) : left to right

# 화살표(->) 연산자
- Lambda Expression" in java 8
- 일명 "익명함수"
- 문법
  (parameter...) -> {expression}
- 예제
``` java
Runnable givePizza = () -> {
  System.out.println("페페로니");
  System.out.println("하와이안");
}

```


# 3항 연산자

- 문법
``` java
boolean answer = condition ? true_value : false_value
```

# switch operator
https://blog.naver.com/hsm622/222150928707
스위치 문은 그대로 있고 swtich operator가 생긴 것일 뿐



참고
```
책에서는 &&나 ||가 왼쪽 피연산자 값에 따라 그 값만 확인해서 연산 결과를 도출할 수 있기 때문에 &와 | 보다 상대적으로 효율적이라고 나와있는데요

```

a||b 하면 a가 만약 맞다면 b를 연산하지 않고
a|b하면 a,b둘다 한다


예제코드
``` java
int i = 0;
int j = 0;

if (i++ == 0 || j++ == 0) {
  System.out.println("hello")
}

System.out.println(i)
System.out.println(j)


i = 0
j = 0


if (i++ == 0 | j++ == 0) {
  System.out.println("hello")
}

System.out.println(i)
System.out.println(j)

```


첫번째 output은 1 0
두번째 output은 1 1

--------------------------------
``` JAVA
int start = 2_000_000_000;
int end = 2_000_000_000;

int mid = (start+end)/2
System.out.print(mid)
```

오버플로우가 날 수 잇따.
만약 start와 end가 int의 최대값이라면 더하는 순간 스택 오버플로우가 발생

안전한 방법1
```
int mid = start + (end-start)/2
```
안전한 방법2
```
int mid = (start + end) >>> 1
```
비트를 한자리 옮기면 2로 나누는 것과 같다.
`>>>` 이렇게 먼가 긴 것은 부호가 달라지는 것 이다.
