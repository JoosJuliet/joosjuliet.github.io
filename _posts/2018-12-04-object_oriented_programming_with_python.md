---
layout: post
section-type: post
title: "[object_oriented_programming 1편] python 객체 속의 함수 feat.python"
category: Computer_Science
tags: [ 'object_oriented_programming', '글또1기', 'python', 'computer_science' ]
comments: true
---

# object_oriented_programming_with_python

# 1. 글을 쓴 이유
장고를 하다보니 python을 객체지향적으로 짜고 싶은 생각을 갖게 되었습니다.
그래서 이런저런 글들을 찾다보니 많은 좋은 블로그의 글들이 있었습니다. 아직 파이선도 객체지향 코딩도 공부가 부족하지만 한번 정리하고 싶은 마음에 포스팅 합니다.
[아마 여러번 업그레이드가 될 듯합니다.]

# 2. 본문
## 객체 지향이란?

기본적으로 객체지향의 특징은
1. 새코드를 작성시 기존 코드를 이용하기에 코드의 재사용성이 높습니다.
2. 각 코드에 관계를 맺어주었고 재사용성을 높여주었기에 관리가 쉽습니다.
3. 제어자와 메서드를 이용해 데이터가 보호받고 있으며, 코드 중복을 제거해 코드에 신뢰도가 높습니다.

결국 상속등을 이용해 재사용성을 높이는 것이 핵심 인 것 같습니다.

# 파이선 오브젝트의 이해

일단 object(객체)는 객체지향 변태들이 만든 JAVA의 경우 변수와 메서드로 이루어 진 무언가를 계속 재생산 할 수 있는 틀인 것입니다.
그런데 파이선의 경우 함수나 모듈 등 그냥 모든게 다 object입니다. 그리고 또한 (First Class Function)이기도 하죠. 물론 그의 대표주자는 JS이긴 하지만요.
관련 포스팅은 추후에 할 예정입니다.

``` python
class Student(object):
    def __init__(self, name, year, class_num, student_id): # 파이썬 키워드인 class는 인수 이름으로 사용하지 못 합니다.
        self.name = name
        self.year = year
        self.class_num = class_num
        self.student_id = student_id

    def introduce_myself(self):
        return '{}, {}학년 {}반 {}번'.format(self.name, self.year, self.class_num, self.student_id)

student = Student('이상희', 2, 3, 35)
#student는 instance
print(student.introduce_myself())
```

오브젝트는 str 데이터 타입에 기본적으로 object에 정의된 모든 속성과 메소드를 상속 받습니다.
그 중 가장 대표적으로 ```  __int__  ``` 메소드가 있습니다.



``` python
def my_function():
    # '''my_function에 대한 설명입니다~!'’'
    pass
# my_function의 속성 확인
print (dir(my_function))

# my_function의 docstring 출력
print( my_function.__doc__)

# my_function에 새로운 속성 추가
my_function.new_variable = '새로운 변수입니다.’

# 추가된 속성 확인
print (dir(my_function) )

# 추가한 속성값 출력
print (my_function.new_variable)
```

oop_2.py를 실행하면
```
['__call__', '__class__', '__closure__', '__code__', '__defaults__', '__delattr__', '__dict__', '__doc__', '__format__', '__get__', '__getattribute__', '__globals__', '__hash__', '__init__', '__module__', '__name__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'func_closure', 'func_code', 'func_defaults', 'func_dict', 'func_doc', 'func_globals', 'func_name']
```
my_function에 대한 설명입니다~!
```
['__call__', '__class__', '__closure__', '__code__', '__defaults__', '__delattr__', '__dict__', '__doc__', '__format__', '__get__', '__getattribute__', '__globals__', '__hash__', '__init__', '__module__', '__name__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'func_closure', 'func_code', 'func_defaults', 'func_dict', 'func_doc', 'func_globals', 'func_name', 'new_variable']
```
새로운 변수입니다.
위 코드를 보면 새로운 속성을 추가하는 것이지 예전부터 들어있던 object의 모든 속성과 메소드가 없어지는 것이 아닙니다.

## ```__init__```메소드
 ‘이니셜라이져’이며 다른 언어에서는 ‘constructer’입니다.
 이 메소드는 인스턴스 생성시 자동 호출, 호출 순간 자동으로 인스턴스 오브젝트를 self라는 인자로 받는다.
``` python
class Employee(object):
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first.lower() + '.' + last.lower() + '@schoolofweb.net’
    def full_name(self):
        return '{} {}'.format(self.first, self.last)

emp_1 = Employee('Sanghee', 'Lee', 50000)
emp_2 = Employee('Minjung', 'Kim', 60000) # 클래스를 통해서 full_name 메소드 호출

print (Employee.full_name(emp_1))

```
```
$ python oop_2.py
Sanghee Lee
```
저기에서  full_name 속에  self를 넣지 않는 실수를 많은 사람들이 하게된다.

마지막행의 코드를 보시면 클래스를 통해서 메소드를 실행하였는데, 이런 경우에는 클래스(Employee)는 어떤 인스턴스(emp_1)의 메소드(full_name)를 호출해야 하는지 모르기 때문에 대상이 될 인스턴스(emp_1)를 인자로 전달해야 합니다.
사실 "emp_1.full_name()"를 실행하면 백그라운드에서는 "Employee.full_name(emp_1)"가 실행되는 것입니다.

## ```__str__```메소드
``` python
class Food(object):
    def __init__(self, name, price):
        self.name = name
        self.price = price
    def __str__(self):
        return '아이템: {}, 가격: {}'.format(self.name, self.price)

food_1 = Food('아이스크림', 3000)

# 인스턴스 출력
print(food_1)
```
```
$ python oop_6.py
아이템: 아이스크림, 가격: 3000
```

----


참고 자료
http://pythonstudy.xyz/python
https://wikidocs.net/book/search/result/1
http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-4-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%A9%94%EC%86%8C%EB%93%9C%EC%99%80-%EC%8A%A4%ED%83%9C%ED%8B%B1-%EB%A9%94%EC%86%8C%EB%93%9C-class-method-and-static-method/
