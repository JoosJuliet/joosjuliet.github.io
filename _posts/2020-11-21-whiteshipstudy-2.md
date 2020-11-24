---
layout: post
section-type: post
title: "2주차 자바 데이터 타입, 변수 그리고 배열"
category: Java
tags: [ 'Java', 'whiteship' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  

전반적 다 좋아
https://github.com/yeo311/java-study-with-whiteship/tree/main/week2

https://catch-me-java.tistory.com/14 ->https://docs.google.com/presentation/d/1Ni0FMbVBSTxiOWHvp928quGT8sTjTG_ZuAWxaCFGT1E/edit#slide=id.p
# 2주차 자바 데이터 타입, 변수 그리고 배열


## 프리미티브 타입 종류와 값의 범위 그리고 기본 값

```
구분       프리미티브 타입   메모리 크기        기본값       표현 범위
-----------------------------------------------------------
논리형      boolean       1 bit	         false      true,false
-----------------------------------------------------------
          byte          1 byte          false       - 128 ~ 127
          short         2 bytes         0           -32,768 ~ 32,767
          int           4 bytes         0           -2,147,483,648 ~ 2,147,483,647
정수형      long          8 bytes         0L          -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
-----------------------------------------------------------
          float         4 bytes         0.0f         (3.4 X 10^-38) ~ (3.4 X 10^38) 의 근사값
실수형      double       8 bytes         0.0d          (1.7 X 10^-308) ~ (1.7 X 10^308) 의 근사값
-----------------------------------------------------------
문자형      char         2 bytes         '\u0000'      0 ~ 65,535


```
unsigned int있다.
근데 좀 사용하기 힘들어서 그냥 bigint쓰장
찬고: https://www.notion.so/2-38b5d67c7f5a48238529bb8f1617ea0d

->->> https://blog.naver.com/hsm622/222144931396 혹은 https://github.com/kksb0831/Practice_project/blob/master/Java_Study_02.md
왜 저 영역인지 설명

돈은 bigdecimal로 해야한다. float이나 long안돼!

## 프리미티브 타입과 레퍼런스 타입

프리미티브 타입은 진짜 값을 저장하고
레퍼런스 타입은 그 값을 저장해 놓은 곳의 주소를 저장하는 것이다.



## 리터럴이란?
- 변수에 넣은 변하지 못하는 데이터를 의미하는 것이다.
- 아래 코드에서 number는 상수이고 리터럴은 1이다.
```
final int number = 1;
```
- immutable class를 제외한 클래스들은 동적으로 값을 변화시키기 때문에 리터럴이 될 수 없다.
```
class Bus:
  string handle;
  int tire;


final bus Bus = new Bus();
```
->정수 리터럴
정수를 표현하는 방법은 여러가지가 있다. 일반적으로 사용하는 10진법 부터 2진법 8진법 과 같은 방법이 있고 자바에서는 다양한 진법을 지원한다.
10진수 26을 다양한 리터럴로 표현해보자.

  int decimal = 26;	   // 일반적인 형태 10진법
  int ocatal = 032;        // 제일 앞에 0 이 붙으면 8진법
  int heaxaDecimal = 0x1a; // 0x가 붙으면 16진법
  int binary = 0b11010;    // 0b가 붙으면 2진법
정수 리터럴은 기본적으로 int 형이고, long 타입을 표현하려면 l,L을 마지막에 붙여야 한다.

https://velog.io/@jaden_94/2%EC%A3%BC%EC%B0%A8-%ED%95%AD%ED%95%B4%EC%9D%BC%EC%A7%80


## 변수 선언 및 초기화하는 방법



## 변수의 스코프와 라이프타임
참고: https://catsbi.oopy.io/6541026f-1e19-4117-8fef-aea145e4fc1b
언제 메모리에 올라오는지가 중요하다
``` java
public class test{

    int instanceVariable = 10; //인스턴스 변수
    static int classVariable = 100; //클래스변수

    public void block(){

        int localVariable = 20; //지역변수
        System.out.println(localVariable);

    }

    public static void main(String[] args) {

        System.out.println(instanceVariable);
        System.out.println(localVariable); //에러
        block()

    }  

}


```

- 인스턴스 변수
범위 : 정적 메서드를 제외한 클래스 전체
수명 : 개체가 메모리에 남아있을 때까지.

- 클래스 (스태틱) 변수
범위 : class 전체
수명 : 프로그램이 끝날 때까지 또는 클래스가 메모리에 로드되어 있을 때까지

- 지역 (로컬) 변수
범위 : 선언 된 블록 내
수명 : 컨트롤이 선언 된 블록을 떠날 때까지.


## 타입 변환, 캐스팅 그리고 타입 프로모션
### 타입 캐스팅
자신의 표현할 수 있는 범위내에서 데이터 타입으로 변화시키는 것
만약 표현 할 수 없는 범위를 내면 문제가 데이터에 문제가 생긴다.
```java
int a = 10;     
byte b = (byte)a;
System.out.println(b); //  -> 10

```




### 타입 프로모션
자신의 표현 범위를 모두 포함하지 못한 데이터 타입으로의 변환하는 것.
타입캐스팅과 반대로 크기가 더 작은 자료형을 더 큰 자료형에 대입하는 것을 의미한다. 예를들어 byte(1byte)타입의 데이터를 int(4byte) 타입에 대입하는 경우이다.
그리고 이 경우에는 데이터 손실이나, 변형이 오지 않음으로 캐스팅할 때 처럼 명시적으로 적지 않아도 자동으로 변환이 가능하다.

``` java
byte a = 10;
int b = a;
System.out.println(b); //  -> 10
```




## 1차 및 2차 배열 선언하기
``` Java
int[] a = {1,3,5,7,9};  
int[][] b = {{00, 01, 02}, {10, 11, 12}, {20, 21, 22}, {31, 32, 33}};

System.out.println(b[1][2]); // 12
System.out.println(b[2][1]); // 20

```
배열을 어떻게 하는지 좀 볼 수 있는 것
참고 : https://b-programmer.tistory.com/225


## 타입 추론과 var
- 타입추론이란?
  - 컴파일러가 스스로 타입 매개 변수가 무엇인지 알아내는 것
  - java의 경우 초기값을 기본적으로 넣어준다.
  - 이때 사용하는 type이 `var`
  - 전역변수에서는 작동하지 않는다.
  ``` java
  var a ; // error
  var a = 1; // fine
  ````
-> 제너릭이랑 관련된
찬고: https://www.notion.so/2-38b5d67c7f5a48238529bb8f1617ea0d
->타입추론 좋은 글
참고: https://www.notion.so/2-00ffb2aeb41d450aa446675b8a9e91d5
---

참고 url:
https://velog.io/@bk_log/Java-%ED%83%80%EC%9E%85-%EC%B6%94%EB%A1%A0  
https://hsm622.blog.me/221558629592  
https://mommoo.tistory.com/14 [개발자로 홀로 서기]  
https://zhaogo.tistory.com/3  
https://velog.io/@jaden_94/2%EC%A3%BC%EC%B0%A8-%ED%95%AD%ED%95%B4%EC%9D%BC%EC%A7%80  
