---
layout: post
section-type: post
title: "Serializer/ deserializer"
category: ComputerScience
tags: [ 'computer-science' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)  
---  

# 직렬화 / 역직렬화
- 직렬화(Serialize)
    - 시스템 내부에서 사용되는 데이터를 외부의 시스템에서도 사용할 수 있도록 변환하는 기술.
    - "자바 시스템적으로 이야기하자면"
        - JVM(Java Virtual Machine 이하 JVM)의 메모리에 상주(힙 또는 스택)되어 있는 객체 데이터를 바이트 형태로 변환하는 기술

- 역질렬화(Deserialize)
    - 변환된 Data를 기존 데이터 형태로 변환하는 기술.
    - "자바 시스템적으로 이야기하자면"
        - 직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM으로 상주시키는 형태.




# 자바의 직렬화 조건
- 자바 기본(primitive) 타입
- `java.io.Serializable` 인터페이스를 상속받은 객체




# Java Serializable이란?
- Java에서는 자동으로 직렬화를 위한 인터페이스를 제공
- 사용법은 단순히 사용할 곳에 java.io.Serializable을 implements하면 된다. 
- implements하면 JVM내부에서 자동으로 직렬화, 역직렬화를 처리한다.
- 장점
    - 사용하기 편리하다는 것이다. 직렬화나 역직렬화에 대한 추가 코드가 필요없이 Serializable만 implements하면 된다.
- 단점
    - Serializable 은 내부에서 Reflection 을 사용하여 직렬화를 처리하기에 cost가 많이든다.




# 예제

- 코드
    - All of the fields in the class must be serializable. If a field is not serializable, it must be marked transient.
``` java
public class Employee implements java.io.Serializable {
   public String name;
   public String address;
   public transient int SSN;
   public int number;
   
   public void mailCheck() {
      System.out.println("Mailing a check to " + name + " " + address);
   }
}

```


``` java

public class SerializeDemo {

   public static void main(String [] args) {
      Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
      
      try {
         FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in /tmp/employee.ser");
      } catch (IOException i) {
         i.printStackTrace();
      }
   }
}
```

``` java
import java.io.*;
public class DeserializeDemo {

   public static void main(String [] args) {
      Employee e = null;
      try {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      } catch (IOException i) {
         i.printStackTrace();
         return;
      } catch (ClassNotFoundException c) {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("Address: " + e.address);
      System.out.println("SSN: " + e.SSN);
      System.out.println("Number: " + e.number);
   }
}
```

- 결과 : 
``` 
Deserialized Employee...
Name: Reyan Ali
Address:Phokka Kuan, Ambehta Peer
SSN: 0
Number:101

```


# 직렬화 법
- 문자열 형태의 직렬화 방법
    - csv, json
- 이진 직렬화 방법
    - 데이터 변환 및 전송 속도에 최적화하여 별도의 직렬화 방법
    - Protobuf,avro
- 자바 직렬화
    - 자바 프레임워크 끼리 주고 받을 수 있는 데이터로 직렬화



---
참고자료 : https://www.tutorialspoint.com/java/java_serialization.htm  