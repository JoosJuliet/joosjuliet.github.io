---
layout: post
section-type: post
title: "[object_oriented_programming 2편] 클래스 변수 와 클래스 메소드, 스태틱 메소드 feat.python"
category: Computer_Science
tags: [ 'object_oriented_programming', '글또1기', 'python', 'computer_science' ]
comments: true
---

# object_oriented_programming_with_python

# 클래스 변수(Class Variable)

인스턴스 변수란 각각의 인스턴스마다 가지고 있는 고유한 데이터이다.
위의 경우 Sanghee, Lee, 50000
클래스변수란 클래스로 만들어진 모든 인스턴스가 공유하는 데이터

``` python
class Employee(object):

    raise_amount = 1.1 #클래스변수

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first.lower() + '.' + last.lower() + '@schoolofweb.net'

    def full_name(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * Employee.raise_amount)  

emp_1 = Employee('Sanghee', 'Lee', 50000)
emp_2 = Employee('Minjung', 'Kim', 60000)

print (emp_1.pay)  # 기존 연봉
emp_1.apply_raise()  # 인상률 적용
print (emp_1.pay)  # 오른 연봉
```
주목해야할 점 클래스 Employee를 사용하여 클래스 변수에 접근한다
그런데 self.raise_amount로 해도 찾아진다!’
왜냐면 "인스턴스 네임스페이스" -> "클래스 네임스페이스" -> "수퍼 클래스 네임스페이스"의 순서로 변수명을 찾기 때문이다.(거꾸로는 안된다)

좀 더 보기 좋은 상태를 찍어보면

``` python
class Employee(object):
    raise_amount = 1.1
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first.lower() + '.' + last.lower() + '@schoolofweb.net'

    def full_name(self):
        return '{} {}'.format(self.first, self.last)

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)

emp_1 = Employee('Sanghee', 'Lee', 50000)
emp_2 = Employee('Minjung', 'Kim', 60000)

print (emp_1.__dict__)  # 인스턴스의 네임스페이스 참조
print (Employee.__dict__)  # 클래스의 네임스페이스 참조
```

``` python
# python oop_3.py
{'pay': 50000, 'last': 'Lee', 'email': 'sanghee.lee@schoolofweb.net', 'first': 'Sanghee'}

{'__module__': '__main__', 'apply_raise': , 'full_name': , 'raise_amount': 1.1, '__dict__': , '__weakref__': , '__doc__': None, '__init__': }
```
보면  Employee클래스 오브젝트의 네임스페이스에만 ‘raise_mount’가 있는 걸 볼 수 있다.

``` python

class SuperClass(object):
    super_var = '수퍼 네임스페이스에 있는 변수입니다.'

class MyClass(SuperClass):
    class_var = '클래스 네임스페이스에 있는 변수입니다.'

    def __init__(self):
        self.instance_var = '인스턴스 네임스페이스에 있는 변수입니다.'


my_instance = MyClass()

# 엑세스 가능한 경우
print (my_instance.instance_var)
print (my_instance.class_var)
print (my_instance.super_var)
print (MyClass.class_var)
print (MyClass.super_var)
print (SuperClass.super_var)
```

이걸 보면 위에 있는 그림을 더 이해하기 쉽습니다..

``` python
class Employee(object):
    raise_amount = 1.1  # 클래스 변수를 사용하여 모든 직원에 적용
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first.lower() + '.' + last.lower() + '@schoolofweb.net'


    def full_name(self):
        return '{} {}'.format(self.first, self.last)


    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)  #1 인스턴스 변수부터 참조를 합니다.

emp_1 = Employee('Sanghee', 'Lee', 50000)
emp_2 = Employee('Minjung', 'Kim', 60000)

emp_1.raise_amount = 1.2  # 인스턴스 변수를 사용하여 특별 인상률 적용

print( '# emp_1 연봉 20% 인상')
print( emp_1.pay)
emp_1.apply_raise()
print (emp_1.pay)
print ('# emp_2 연봉 10% 인상')
print (emp_2.pay)
emp_2.apply_raise()
print (emp_2.pay)


# $ python oop_3.py
# emp_1 연봉 20% 인상
# 50000
# 60000
# emp_2 연봉 10% 인상
# 60000
# 66000
```
emp_1은 인스턴스 변수 네임스페이스에 raise_amount가 있어서 참조가 되고, emp_2는 없으니까 자동으로 클래스 변수인 raise_amount를 참조하는

#클래스 메소드(Class Method)와 스태틱 메소드(static method)

인스턴스 메소드는 'self'인 인스턴스를 인자로 받고 인스턴스 변수와 같이 하나의 인스턴스에만 한정된 데이터를 생성, 변경, 참조 한다면,
클래스 메소드는 'cls'인 클래스를 인자로 받고 모든 인스턴스가 공유하는 클래스 변수와 같은 데이터를 생성, 변경 또는 참조하기 위한 메소드(?)


# 1. 클래스 메소드
클래스 메소드는
1. 원래 만들어져 있는 constructer를  변경
2. constructer를 만드는데
이용됩니다.

``` python
class Employee(object):

    raise_amount = 1.1  #1 연봉 인상율 클래스 변수

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        self.email = first.lower() + '.' + last.lower() + '@schoolofweb.net'

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)

    def full_name(self):
        return '{} {}'.format(self.first, self.last)

    def get_pay(self):
        return '현재 "{}"의 연봉은 "{}"입니다.'.format(self.full_name(), self.pay)

emp_1 = Employee('Sanghee', 'Lee', 50000)

# 연봉 인상 전
print(emp_1.get_pay())# 현재 "Sanghee Lee"의 연봉은 "50000"입니다.

# 연봉 인상
emp_1.apply_raise()

# 연봉 인상 후
print(emp_1.get_pay()) # 현재 "Sanghee Lee"의 연봉은 "55000"입니다.
```
연봉 인상율을 다르게 하고 싶으면...

``` python
import sys

class Employee(object):

    raise_amount = 1.1  # 연봉 인상율 클래스 변수

    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay

    def apply_raise(self):
        self.pay = int(self.pay * self.raise_amount)

    def full_name(self):
        return '{} {}'.format(self.first, self.last)
        return '현재 "{}"의 연봉은 "{}"입니다.'.format(self.full_name(), self.pay)

    #1 클래스 메소드 데코레이터를 사용하여 클래스 메소드 정의
    @classmethod
    def change_raise_amount(cls, amount):
        #2 인상율이 "1" 보다 작으면 재입력 요청
        while amount < 1:
            print('[경고] 인상율은 "1"보다 작을 수 없습니다.')
            amount = input('[입력] 인상율을 다시 입력하여 주십시오.\n=> ')
            amount = float(amount)
        cls.raise_amount = amount
        print('인상율 "{}"가 적용 되었습니다.'.format(amount))

emp_1 = Employee('Sanghee', 'Lee', 50000)

# 연봉 인상 전
print(emp_1.get_pay()) # 현재 "Sanghee Lee"의 연봉은 "50000"입니다.

# 연봉 인상율 변경
Employee.change_raise_amount(0.9)
#[경고] 인상율은 "1"보다 작을 수 없습니다.
#[입력] 인상율을 다시 입력하여 주십시오.
#=>
#1.2 입력?
#인상율 "1.2"가 적용 되었습니다.

# 연봉 인상
emp_1.apply_raise()

# 연봉 인상 후
print(emp_1.get_pay()) #현재 "Sanghee Lee"의 연봉은 "60000"입니다.

```
여기서 보면 #1클래스 메소드 데코레이터를 사용하여 클래스 메소드를 정의
#2에서는 데이터 무결성 검사를 실시한 후, 데이터가 1보다 큰 경우에만 클래스변수를 변경하였습니다. 클래스 메소드는 인스턴스 생성자(constructor)와 같은 용도로 사용하는 경우


종종 class에 있는 것을 활용해서 무언가를 만들고 싶은 생각이 들겁니다,
그럴 때는

``` python
class Person(object):
    def __init__(self, year, month, day, sex):
        self.year = year
        self.month = month
        self.day = day
        self.sex = sex

    def __str__(self):
        return '{}년 {}월 {}일생 {}입니다.'.format(self.year, self.month, self.day, self.sex)

ssn_1 = '900829-1034356'

def ssn_parser(ssn):
        front, back = ssn.split('-')
        sex = back[0]

        if sex == '1' or sex == '2':
            year = '19' + front[:2]
        else:
            year = '20' + front[:2]

        if (int(sex) % 2) == 0:
            sex = '여성'
        else:
            sex = '남성'

        month = front[2:4]
        day = front[4:6]

        return year, month, day, sex

person_1 = Person(*ssn_parser(ssn_1))
print(person_1) #1990년 08월 29일생 남성입니다.

```
이렇게 할 수 도 있습니다.
하지만 저렇게 하는 것 보다는
``` python
class Person(object):
    def __init__(self, year, month, day, sex):
        self.year = year
        self.month = month
        self.day = day
        self.sex = sex

    def __str__(self):
        return '{}년 {}월 {}일생 {}입니다.'.format(self.year, self.month, self.day, self.sex)

    @classmethod
    def ssn_constructor(cls, ssn):
        front, back = ssn.split('-')
        sex = back[0]

        if sex == '1' or sex == '2':
            year = '19' + front[:2]
        else:
            year = '20' + front[:2]

        if (int(sex) % 2) == 0:
            sex = '여성'
        else:
            sex = '남성'

        month = front[2:4]
        day = front[4:6]

        return cls(year, month, day, sex)

ssn_1 = '900829-1034356'

person_1 = Person.ssn_constructor(ssn_1)
print(person_1) #1990년 08월 29일생 남성입니다.

```
이렇게 만드는 것이 더 우아하죠.

#2.스태틱 메소드
클래스 안에서 정의 되는 메소드
1.인스턴스 메소드, 2.클래스 메소드, 3.스태틱 메소드

1.인스턴스 메소드는 인스턴스를 통해서 호출이 됩니다.
     첫 번째 인자로 인스턴스 자신을 자동으로 전달합니다. 관습적으로 이 인수를 'self'라고 칭합니다.
2.클래스 메소드는 클래스를 통해서 호출이 되고, ``` @classmethod ```라는 데코레이터로 정의합니다.
    첫 번째 인자로는 클래스 자신이 자동으로 전달되고 이 인수를 관습적으로 'cls'라고 칭합니다.
3.스태틱 메소드는 클래스 안에서 정의되어 클래스 네임스페이스 안에는 있을뿐 일반 함수와 전혀 다를게 없다.
    첫번째 인자를 특별하게 받아야 하는 것은 없습니다.

스태틱 메소드의 경우 클래스 안에 연관성 있는 메소드를 넣으면 편하기 때문에 쓰는 것 입니다.

``` python
class Person(object):
    my_class_var = 'sanghee'

    def __init__(self, year, month, day, sex):
        self.year = year
        self.month = month
        self.day = day
        self.sex = sex


    def __str__(self):
        return '{}년 {}월 {}일생 {}입니다.'.format(self.year, self.month, self.day, self.sex)


    @classmethod
    def ssn_constructor(cls, ssn):
        front, back = ssn.split('-')
        sex = back[0]

        if sex == '1' or sex == '2':
            year = '19' + front[:2]
        else:
            year = '20' + front[:2]

        if (int(sex) % 2) == 0:
            sex = '여성'
        else:
            sex = '남성'

        month = front[2:4]
        day = front[4:6]

        return cls(year, month, day, sex)


    @staticmethod
    def is_work_day(day):
        # weekday() 함수의 리턴값은
        # 월: 0, 화: 1, 수: 2, 목: 3, 금: 4, 토: 5, 일: 6
        if day.weekday() == 5 or day.weekday() == 6:
            return False
        return True

ssn_1 = '900829-1034356'

person_1 = Person.ssn_constructor(ssn_1)
print(person_1) #1990년 08월 29일생 남성입니다.
```

``` python
import datetime
# 일요일 날짜 오브젝트 생성
my_date = datetime.date(2016, 10, 9)

# 클래스를 통하여 스태틱 메소드 호출
print(Person.is_work_day(my_date)) #False
# 인스턴스를 통하여 스태틱 메소드 호출
print(person_1.is_work_day(my_date)) #False
@staticmethod 데코레이터를 사용하여 'is_work_day'라는 이름과 어떤 날짜에 근무 여부를 리턴하는 기능을 가진 스태틱 메소드를 만들어 봤습니다.
```

----


참고 자료
http://pythonstudy.xyz/python
https://wikidocs.net/book/search/result/1
http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-4-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%A9%94%EC%86%8C%EB%93%9C%EC%99%80-%EC%8A%A4%ED%83%9C%ED%8B%B1-%EB%A9%94%EC%86%8C%EB%93%9C-class-method-and-static-method/
