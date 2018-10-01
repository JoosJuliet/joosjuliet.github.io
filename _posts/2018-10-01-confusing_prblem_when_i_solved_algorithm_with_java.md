---
layout: post
section-type: post
title: "[ 작성중 ] 알고리즘 풀 때 팁 (feat. java)"
categories: Algorithm
tags: [ 'algorithm' ]
comments: true
---


# Prime 알기

``` java

public class Main {
    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String args[]) {

        BigInteger n = scanner.nextBigInteger();
        System.out.println(n.isProbablePrime(100) ? "prime" : "not prime");
    }
}
```

# ArrayList

## ArrayList 초기화

``` java
import java.util.ArrayList;
import java.util.List;

List idolList = new ArrayList();
```

## ArrayList 값 추가

``` java
idolList.add("아이린");
idolList.add("예리");
idolList.add(new String("조이"));

idolList.add(1, "첫번째 요소값");
```

## ArrayList 인덱스를 통한 조회

``` java
// 인덱스를 통한 조회
String element0 = idolList.get(0).toString(); //아이린
String element1 = idolList.get(1).toString(); // 예리
String element3 = idolList.get(2).toString(); // 조이
```

## ArrayList의 Iterator 통한 전체 조회

``` java
import java.util.Iterator;

Iterator iterator = idolList.iterator();
while (iterator.hasNext()) {
    String element = (String) iterator.next();

}
```

## ArrayList의 for-loop 통한 전체 조회

``` java
for(Object object : idolList) {
    String element = (String) object;
}
```

## ArrayList의 특정 값 앞에 값 추가

``` java
int index = idolList.indexOf("아이린");
idolList.add(index, "아이린 앞에 값 추가");
```

## ArrayList의 존재 여부 확인
``` java
System.out.println(idolList.contains("아이린"));

```

## ArrayList의 값 삭제하는 방법
``` java
System.out.println(idolList.remove(0));
System.out.println(idolList.remove("아이린"));


```

# HashMap

## HashMap 초기화

``` java
import java.util.HashMap;
HashMap<String, Integer> idolMap = new HashMap();

```

## HashMap 값 추가

``` java
idolMap.put("아이유", 25);
idolMap.put("아이린", 20);
idolMap.put("설현", 30);
```

## HashMap key값으로 호출

``` java
// get() --> Key에 해당하는 Value를 출력한다.
System.out.println( idolMap.get("아이유") );   // 25

```

## HashMap 모든 값 list로 가져오기
``` java
// values() --> 저장된 모든 값 출력
System.out.println( idolMap.values() ); // [25, 20, 30]

```

## HashMap 하나씩 출력

``` java
import java.util.Iterator;
import java.util.Map;
import java.util.Set;
// HashMap에 넣은 Key와 Value를 Set에 넣고 iterator에 값으로 Set정보를 담에 준다.
// Interator itr = idolMap.entrySet().interator(); 와 같다.

Set<Entry<String, Integer>> set = idolMap.entrySet();
Interator<Entry<String, Integer>> itr = set.interator();

while (itr.hasNext()){
    Map.Entry<String, Integer> e = (Map.Entry<String, Integer>)itr.next();
    System.out.println("이름 : " + e.getKey() + ", 나이 : " + e.getValue());
}

```

# Array

## array 초기화

``` java
boolean [] bitList; // boolean 형태 list
bitList = new boolean[10]; //기본값으로 초기화
// 길이는 10
Arrays.fill(bitList, false); //특정 값으로 초기화
// false라는 값으로 초기화

//배열의 길이
bitList.length //10
```
## array 처음부터 끝까지 출력하기
``` java
import java.util.*;

public class Main {
    private static final Scanner scanner = new Scanner(System.in);
    public static void main(String args[]) {
        Scanner in = new Scanner(System.in);
        int size = in.nextInt();
        int[] arr = new int[size];
        for(int i=0; i<size; i++){
            arr[i] = in.nextInt();
        }
        for(int i=0; i<size; i++){
            System.out.print(arr[i]);
        }

    }

}
```


## 2차원 배열

``` java
int [] [] intArrays = new int [행][열];

intArrays // 여기에는 주소값이 들어있다.
intArrays[0] // 여기에도 주소값이 들어있다.
intArrays[0][0] // 여기에는 0이 들어간다.

intArrays.length // 행의 갯수를 리턴한다.
intArrays[0].length // 이때는 열의 갯수를 리턴한다.

//다차원 배열의 할당 선언
boolean [] [] booleanArrays = { {true, true}, {false, false, false}, ... };
```


## 배열 for in 문

``` java

//실제 예
for( int i : intArray ) {
	System.out.print( i ); //배열의 각 값이 i에 담겨진다.
}

// 2차원

for( String [] s : stringArrays ) // 행을 가져오기
	for( String t : s ) // 열을 가져오기
		System.out.print( t ); //2차원 배열의 각 값이 t에 담겨진다.
```
## array 정렬

``` java
Arrays.sort( 배열명 );
```



-----
참고 site:
http://mainia.tistory.com/2323 [녹두장군 - 상상을 현실로]
http://vaert.tistory.com/107 [Vaert Street]

https://www.hackerrank.com/challenges/java-negative-subarray/problem
