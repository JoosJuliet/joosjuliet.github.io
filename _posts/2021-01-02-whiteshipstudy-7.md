---
layout: post
section-type: post
title: "7주차 과제: 패키지"
category: Java
tags: [ 'Java' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---






# 목차
- package 키워드
- import 키워드
- 클래스패스
- CLASSPATH 환경변수
- `-classpath` 옵션
- 접근지시자


-> bootloader




# package 키워드

- 고유성을 보장하고,서로 관련된 것을 그룹화해 효율적으로 관리하기 위해 사용
- 각 파일의 가장 상위에 위치하며 설정하지 않으면 패키지가 자동으로 설정이 된다.
- 문법
  - `package com.joos.app`
  - 점(.)을 구분자로 하여 계층구조로 구성
  - 소문자를 원칙
- 두가지 종류
  - 빌트인 패키지
  - 사용자 정의 패키지
- `FQCN`(Fully Qualified Class Name)로 사용가능
  - 클래스가 속한 패키지명을 모두 포함한 이름
  - String 클래스를 선언하는 방법 예
    - `java.lang.String s = new java.lang.String();`
    -  java.lang 패키지는 자동으로 import 되기 때문에 `String s = new String();` 이리 할 수 있다.
- 빌트-인 패키지(Built-in Package)
  - 빌트인 패키지는 개발자들이 사용할 수 있도록 여러 많은 패키지 및 클래스를 제공해 import를 통해 부르지 않아도 쓸 수 있는 것으로 String이 대표 예
  - 가장 자주 쓰이는 패키지로는 java.lang, java.util




# import 키워드
- 다른 파일에 있는 클래스를 이용하기 위해 사용
- 두가지 방법
  - 패키지와 클래스를 모두 기술하는 방법
    - `FQCN`(Fully Qualified Class Name)
    - 예
      -  `com.cube` 패키지에 소속된 GIdle 클래스를 이용해서 필드 선언 후 객체 생성
      ``` java
      package com.cube;

      public class MAMA{
        com.cube.GIdle soojin = new com.cube.GIdle(); // 객체생성
      }
      ```
    - 쓸만한 상황
      - mama package에 singer class가 있다
      - 아는형님 package에 singer class가 있다.
      - 이렇게 같은 리파지토리에 있는 package 속 class가 같을 때 broadcast에서 singer class를 부를 때 헷갈릴 수 있으니 써야한다.
  - import 문 사용
    - 사용하고자 하는 패키지와 디렉토리를 import 문으로 선언하고, 클래스를 사용시에는 패키지 생략
    - 예)  
    GIdle.java  
    ``` java
    package com.cube;
    public class GIdle{
      String position;

    }

    ```
    - Singer.java  
    ```java
    package com.cube;

    import com.cube.GIdle;

    public class Singer{
    	GIdle soojin = new GIdle();
    }
    ```
- 컴파일 시에 컴파일러는 import문을 통해 소스파일에 사용된 클래스들의 패키지를 알아 낸 다음, 모든 클래스 이름 앞에 패키지명을 붙여준다.
- 패키지에 다수의 클래스를 import 하는 경우 import 패키지명.* 처럼 import 가능
- intelij 단축키 -> `Option +Enter`
- `import static`의 경우
  - static 한 변수(클래스 변수)와 static 한 메소드를 사용하고자 할때 용이
  - 예
  ``` java
  import static java.lang.Math.random;
  ```
  - static import 문 선언 전
  ``` java
  System.out.println(Math.random());
  ```
  - static import 문 선언
  ``` java
  System.out.println(random());
    ```



# 클래스패스, `-classpath` 옵션  
자바를 설치할 때, 자연스럽게 따라하는 몇 가지 설정이 있다.   
$JAVA_HOME과 $CLASSPATH 설정이다. 이 중 클래스 패스가 무엇인지 먼저 알아본다.  

- 클래스패스는 JVM 혹은 Java 컴파일러가 사용하는 파라미터인데
- 기본적으로는 java 명령을 실행하는 위치를 의미


- jvm은 class loader를 통해 class 파일을 jvm에 로딩하고 Execution Engine을 통해 해석
- 이를 위해 클래스나 패키지를 찾을 때 기준이 되는 경로가 필요
- 즉 클래스 패스는 자바의 가상머신 (JVM)이 컴파일된 클래스 파일(.class)을 실행시킬 때, 클래스패스에 설정된 경로에서 해당 파일을 찾아 실행
- 그래서 자바파일을 컴파일 할 때는 아래와 같이 클래스패스 경로를 지정해주어야 한다.  
```
java -classpath ".:lib" ClasspathTest
```
옵션 -classpath를 사용하여 자바를 실행할 때 사용할 클래스들의 위치를 가상머신에 알려주는 역할을 합니다.  


- `.;lib`
  - `.` -> 현재 디렉터리에서 클래스를 찾는다는 의미
  - `;` -> 경로와 경로를 구분해주는 구분자
  - `lib` -> 현재 디렉터리에 없다면 현재 디렉터리의 하위 디렉터리 중 lib에서 클래스를 찾는다는 의미  

만약 .을 제외한다면, 현재 디렉토리의 클래스를 찾지 못한다. 하지만 하위 lib 디렉토리에 있는 클래스는 찾을 수 있다.  




# CLASSPATH 환경변수
classpath옵션은 javac, java둘다 쓸 수 있다. -> runtime할 때도 된다.
다운받아주고 external library 얘들이 다 classpath로 연결이 된다.
libraries들이 다 class path가 된다.
maven이 자기 로컬저장소 -> /.m2/repository,

org/koshuke 및에 github-api밑에 막 있다.

mvnw 이렇게 빌드할 때도

mvn에 scope가 있다.
compile 등등...
공부를 해야한다고 한다...



클래스를 찾기위한 경로이다.
classpath 를 지정하기 위한 두 가지 방법이 있는데

- CLASSPATH 환경변수 사용
  - 이건 해보고 지워야 한다. 왜냐면...실행할 때마다 매번 바꿔줘야 하니까.
  - 그리고 우리는 intelij쓸꺼여서 실제로 할일은 거의 없다.
  - 컴퓨터 시스템 변수 설정을 통해 지정할 수 있어 JVM이 시작될 때 JVM의 클래스 로더는 이 환경 변수를 호출
- java runtime 에 -classpath 옵션 사용
  - 예
```
exec java -cp "$CLASSPATH" $JVMFLAGS $MAIN $ZK_CONFIG_FILE
```
- `-classpath` 옵션
- classpath 옵션은 컴파일 할 때도 쓸 수 있는 것이다. 실행도 되지
옵션은 뭐 계속 바뀌는데

알아서 찾아주는 똑똑한 intelij
like this

# 접근지시자

접근제어자는 클래스, 메소드, 인스턴스 및 클래스 변수를 선언할 때, 사용

- public
  - 누구나 접근 가능
- protected
  - 같은 패키지에 있거나, 상속 받는 경우 사용 가능
- package-private(default)
  - 아무 접근제어자를 적어주지 않은 경우이며, package-private라 불린다. 같은 패키지 내에서 접근 가능
- private
  - 해당 클래스 내에서만 접근 가능



----

https://www.geeksforgeeks.org/java-gq/packages-gq/ -> 퀴즈



https://www.notion.so/ed8e346f88f54849a06ff968b1877ca5
https://velog.io/@jaden_94/7%EC%A3%BC%EC%B0%A8-%ED%95%AD%ED%95%B4%EC%9D%BC%EC%A7%80
->클래스로더 계층구조 ->rt.jar파일도 읽어봐 이거 옛날일수 있다. 9부터 없어졌다. 지금 버전 대신 src.zip이 있다.
