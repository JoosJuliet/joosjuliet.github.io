---
layout: post
section-type: post
title: "[Hibernate에 대해서 제대로 알자!] 3탄 Hibernate가 어떻게 obejct를 만드는가?"
category: Spring
tags: [ 'Spring', 'Java', 'JPA', '글또2기', '시리즈물' ]
comments: true
---

제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---
이 글은 시리즈 물이며, 해당 글은 번역글입니다.  
번역 출처는 : https://www.javatpoint.com/steps-to-create-first-hibernate-application 입니다.

[1탄 ORM이란? JPA란? Hibernate란?] https://joosjuliet.github.io/orm_jpa_hibernate/  
[2탄 Hibernate의 구조를 알자!] https://joosjuliet.github.io/hibernate_structure/  
[3탄 Hibernate가 어떻게 obejct를 만드는가?] https://joosjuliet.github.io/hibernate_first_step/  

# hibernate가 객체를 만들 때 일어나는 일

- Persistent 클래스를 만들기
- Persistent 클래스에 대한 매핑 파일 만들기
- Configuration file을 만들기
- persistent object를 검색하거나 저장하는 클래스를 만들기
- jar 파일 로드
- first hibernate application을 실행




# 1. Persistent 클래스를 만들기

rule이 있다.
- A no-arg constructor
  - newInstance() 메소드에 의해 Persistent 클래스의 인스턴스를 생성 할 수 있도록, 적어도 패키지 가시성 (visibility) 이상의 디폴트 생성자 (default constructor)가 있는 것이 권장
- Provide an identifier property
  - id를 각 attribute에 할당하는 것이 좋다. database안에서는 primary key로 attribute들이 움직이기 때문이다.
- Declare getter and setter methods
  - The Hibernate는 기본적으로 getter, setter method로 인식한다.
- Prefer non-final class
  - Hibernate는 영속 클래스에 의존하는 프록시의 개념을 사용한다. 개발하는 lazy association fetching에 프록시를 사용할 수 없습니다.


Employee.java
``` java

public class Employee {  
  private int id;  
  private String firstName,lastName;  

  public int getId() {  
      return id;  
  }  
  public void setId(int id) {  
      this.id = id;  
  }  
  public String getFirstName() {  
      return firstName;  
  }  
  public void setFirstName(String firstName) {  
      this.firstName = firstName;  
  }  
  public String getLastName() {  
      return lastName;  
  }  
  public void setLastName(String lastName) {  
      this.lastName = lastName;  
  }  

}  

```




# 2. Persistent 클래스를 매핑할 파일 만들기

mapping 하는 파일은 전통적으로 이름을 class_name.hbm.xml으로 짓는다.


- hibernate-mapping
  - mapping file안에 root element가 있다. 그 파일에는 모든 mapping elemnts들이 있다.
- class
  - 이것은 hibernate 의 mapping element가 될 sub-element이다.
  - Persistent 클래스를 지정합니다.
- id
  - 그것은 클래스의 하위 요소입니다. 클래스의 기본 키 속성을 지정합니다.
- generator
  - id의 sub-element입니다. 기본 키를 생성하는 데 사용됩니다.
  - 많은 generator classes 들이 있다.(예. assigned, increment, hilo, sequence, native etc.)
- property
  - Persistent class의 속성 이름을 지정하는 클래스의 하위 요소입니다.

employee.hbm.xml

``` xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-mapping PUBLIC  
 "-//Hibernate/Hibernate Mapping DTD 5.3//EN"  
 "http://hibernate.sourceforge.net/hibernate-mapping-5.3.dtd">  

 <hibernate-mapping>  
  <class name="com.javatpoint.mypackage.Employee" table="emp1000">  
    <id name="id">  
     <generator class="assigned"></generator>  
    </id>  

    <property name="firstName"></property>  
    <property name="lastName"></property>  

  </class>  

 </hibernate-mapping>  
```




# 3. Configuration file 만들기
구성 파일에는 데이터베이스 및 매핑 파일에 대한 정보가 들어 있습니다. 일반적으로 그 이름은 hibernate.cfg.xml이어야합니다.

hibernate.cfg.xml
``` xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-configuration PUBLIC  
          "-//Hibernate/Hibernate Configuration DTD 5.3//EN"  
          "http://hibernate.sourceforge.net/hibernate-configuration-5.3.dtd">  

<hibernate-configuration>  

    <session-factory>  
        <property name="hbm2ddl.auto">update</property>  
        <property name="dialect">org.hibernate.dialect.Oracle9Dialect</property>  
        <property name="connection.url">jdbc:oracle:thin:@localhost:1521:xe</property>  
        <property name="connection.username">system</property>  
        <property name="connection.password">jtp</property>  
        <property name="connection.driver_class">oracle.jdbc.driver.OracleDriver</property>  
    <mapping resource="employee.hbm.xml"/>  
    </session-factory>  

</hibernate-configuration>  
```




# 4. 객체를 가져 오거나 저장하는 클래스를 만든다.
이 클래스에서는 employee 객체를 데이터베이스에 저장하기 만하면됩니다.

``` java

import org.hibernate.Session;    
import org.hibernate.SessionFactory;    
import org.hibernate.Transaction;  
import org.hibernate.boot.Metadata;  
import org.hibernate.boot.MetadataSources;  
import org.hibernate.boot.registry.StandardServiceRegistry;  
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;  


public class StoreData {    
  public static void main(String[] args) {    

      //Create typesafe ServiceRegistry object    
      StandardServiceRegistry ssr = new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  

      Metadata meta = new MetadataSources(ssr).getMetadataBuilder().build();  

      SessionFactory factory = meta.getSessionFactoryBuilder().build();  
      Session session = factory.openSession();  
      Transaction t = session.beginTransaction();   

      Employee e1=new Employee();    
      e1.setId(101);    
      e1.setFirstName("Gaurav");    
      e1.setLastName("Chawla");    

      session.save(e1);  
      t.commit();  
      System.out.println("successfully saved");    
      factory.close();  
      session.close();    

  }    
}   
```




# 5. jar 파일로드
Hibernate 애플리케이션을 성공적으로 실행하려면, hibernate5.jar 파일이 있어야한다.



---
