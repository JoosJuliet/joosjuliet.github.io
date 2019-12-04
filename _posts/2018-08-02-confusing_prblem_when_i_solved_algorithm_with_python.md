---
layout: post
section-type: post
title: "[ 작성중 ] 알고리즘 풀 때 팁 (feat. python)"
categories: Algorithm
tags: [ 'algorithm' ]
comments: true
---


# Binary
``` Python
python('{0:08b}'.format(6))
# '00000110'
# Just to explain the parts of the formatting string:
```

{} -> places a variable into a string  
0 -> takes the variable at argument position 0  
: -> adds formatting options for this variable (otherwise it would represent decimal 6)  
08 -> formats the number to eight digits zero-padded on the left  
b -> converts the number to its binary representation  


same with  
``` python
print(f'{6:08b}')
# '00000110'
```

same with  

``` python
print(bin(8))
# '0b10011010010'
```

# 0부터 시작하는지 1부터 시작하는지 헷갈릴 때

0부터 시작하는 것이 있음 그건 인덱스라고 생각하고
1 부터 생각하는 게 으면 그걸 카운트로 생각해서,
인덱스를 카운트로 맞춰주기 위해서는 +1을 해줘야 하는 거고
카운트는 인덱스에 맞춰주기 위해서는 -1 을 해준다.

아니면 그냥 *insert* 해서 맞추는 것도 좋은 방법이다.
그럴 때는
> list.insert(index, value)

를 쓰면 된다.

``` python
array = [1,2,3]
array.insert(0,0)
print(array)
# [0,1,2,3]
```
이렇게 중간에 원하는 index에 값을 넣는 방법이다.

혹은...
``` python
array = [1,2,3]
array = [0] + array
print(array)
# [0,1,2,3]

```
초간단하고 더 짧은 코드도 있다

# list +1씩하게 하기
``` python
a = list(range(0,101))
print(a)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
```
<!-- [i in range(0,10)] -->
user_name -> userName
# sorted

``` python
students = [
    ("jane", 22, 'A'),
    ("dave", 32, 'B'),
    ("sally", 17, 'B'),
]
```
students라는 리스트는 총 3개의 튜플을 가지고 있다. 각 튜플은 순서대로 "이름", "나이", "성적"에 해당되는 데이터를 갖는다.

이 리스트를 나이 순으로 소트하려면 어떻게 해야 할까?

이런 경우에는 sort 또는 sorted의 key파라미터를 이용하여 소트해야 한다.
``` python
students = [
  ("jane", 22, 'A'),
  ("dave", 32, 'B'),
  ("sally", 17, 'B'),
]
sorted(students, key=lambda student: student[1])
#  [('sally', 17, 'B'), ('jane', 22, 'A'), ('dave', 32, 'B')]
```
*key파라미터에는 함수가 와야 한다.{ex) len}* key 파라미터에 함수가 설정되면 소트해야 할 리스트들의 항목들이 하나씩 key 함수에 전달되어 key 함수가 실행되게 된다. 이 때 수행된 key 함수의 리턴값을 기준으로 소트가 진행된다.


위 예에서는 key함수에 students의 요소인 튜플데이터가 key함수의 입력으로 순차적으로 전달될 것이다. key함수는 입력된 튜플 데이터의 "나이"를 의미하는 2번째 항목을 리턴하는 lambda함수이다. 따라서 sorted수행 후 나이순으로 소트된 리스트가 리턴된다.

``` python
sorted(student_objects, key=attrgetter('age'), reverse=True)
# [('dave', 32, 'B'), ('jane', 22, 'A'), ('sally', 17, 'B')]
```

reverse=True 넣으면 역순으로 된다


## dictionary key와 value로 sort하기

``` python
import operator
x = {1:2, 3:4,4:3,2:1,0:0}

# value 기준으로 정렬하기
sorted_v_x = sorted(x.items(), key=operator.itemgetter(1))
# key 기준으로 정렬
sorted_k_x = sorted(x.items(), key=operator.itemgetter(0))
```


# 역순 포문
``` python
>>> for i in range(10, 0, -1):    # 10에서 1까지 역순으로 숫자 생성
...     print('Hello, world!', i)

>>> for i in reversed(range(10)):    # range에 reversed를 사용하여 숫자의 순서를 반대로 뒤집음
...     print('Hello, world!', i)    # 9부터 0까지 10번 반복
```


# Counter
``` python
from collections import Counter # 콜렉션에서 불러옵니다.
def pickingNumbers(a):
  d = Counter(a)
```

# sqrt
``` python
from math import sqrt

print('{:04.2f}'.format(sqrt(2)))
# 1.41

```

# defaultdict
orderd 되지 않는 다는 것을 주의

``` python
from collections import defaultdict # 콜렉션에서 불러옵니다.
d = defaultdict(lambda: 0) # Default 값을 0으로 설정합니다.
k =[1,2,3,3]
for a in k:
  d[a] += 1
print(d)
# defaultdict(<function <lambda> at 0x100a81f28>, {1: 1, 2: 1, 3: 2})

```

# set

시간복잡도 찾는데 O(1)

``` python
seen = {1,2,3}
print(4 in seen)
# False
seen = {1,2,3}
print(1 in seen)
# True

```

# 숫자 -> alphabet, alphabet -> 숫자

``` python
print(chr(97))
#'a'
print(chr(65))
#'A'
print(ord('a'))
#97
```




# combinations nCr
순서를 생각하지 않은 순열

``` python
import itertools
import operator

shapes = ['circle', 'triangle', 'square',]
result = itertools.combinations(shapes, 2)
for each in result:
  print(each)
# ('circle', 'triangle')
# ('circle', 'square')
# ('triangle', 'square')
```

nCr 직접 구현
``` python
from math import factorial

def ncr(n, r):
  if n < 2 : return 0
  return factorial(n) // (factorial(n-r) * factorial(r))
```

# permutations nPr
시간복잡도 O(N!)
순서를 생각한 순열


## string

``` python
import itertools
import operator

alpha_data = ['a', 'b', 'c']
result = itertools.permutations(alpha_data)
for each in result:
  print(each)
# ('a', 'b', 'c')
# ('a', 'c', 'b')
# ('b', 'a', 'c')
# ('b', 'c', 'a')
# ('c', 'a', 'b')
# ('c', 'b', 'a')
```


## number
``` python
from itertools import permutations

# Complete the formingMagicSquare function below.
def formingMagicSquare(s):
  comb = permutations(range(1,10),9)
  # 1부터 10까지 9개를 permutation한다
```


nPr 직접 구현
``` python
from math import factorial

def npr(n, r):
  if n < 2 : return 0
  return factorial(n) // factorial(n-r)
```



# String Part

## 특정 문자, 단어에서 찾기
time complexity : O(nm)
The time complexity is O(N) on average, O(NM) worst case (N being the length of the longer string, M, the shorter string you search for).

index 반환

``` python
a = 'abc'
a.find('b') # 1
```

## 한 단어인 string을 list로 만들기

``` python
s1 = 'python'
print(list(s1))
# ['p', 'y', 't', 'h', 'o', 'n']
```

## 스트링 문제 풀 때 유용했던 것(지울 예정)

원래 글자는 msg
``` python
while True:
  # 여기서 돌면서 j라는 변수의 길이를 늘린다.
  if j>=len(msg):
  # j가 더 커지거나 같아지는 순간
    break
  # break로 끝-
```

## string 뒤집기

``` python
string = 'aio'
print(string[::-1])
# oia
```

## step 뒤집기

slice한 값의 범위에서 step 값을 주어 그 값만큼 건너뛰어 가져오는 기능

- 문법
``` python
list[ 시작값:끝값:step ]
```

- 실전
``` python
list1 = list(range(20))
print(list1)
#[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]

print(list1[5:15:3])
#[5, 8, 11, 14]
# 5부터 15까지 3씩 뛰어넘기

print(list1[15:5:-1])
# [15, 14, 13, 12, 11, 10, 9, 8, 7, 6]
# 15부터 5까지 index를 거꾸로 1씩 가게하기

print(list1[::3])
#[0, 3, 6, 9, 12, 15, 18]
# 처음부터 3씩 마지막까지 가게 하기

print(list1[::-3])
# [19, 16, 13, 10, 7, 4, 1]
# 마지막부터 3씩 처음까지 가게 하기

```


## 원하는 문자가 string에 있는 확인하기
list도 string과 문법이 같기에 list역시 여기다 쓴다

``` python
my_list = [1, 9, 8, 5, 0, 6]
print(5 in my_list)
# True
my_str = 'hello world'
print('e' in my_str)
# True
```

## 문자열 => 리스트, 공백시 스페이스 기준

- 문법
``` python
list = str.split()
```

- 실전
``` python
char = list('hello')
print(char)
#['h', 'e', 'l', 'l', 'o']
```

# 리스트 => 문자열, 리스트에서 문자열으로

- 문법
``` python
” “.join( list )
```

- 실전
``` python
char = list('hello')
print(char)
# ['h', 'e', 'l', 'l', 'o']
```

# 문자열의 구성요소 쉽게 아는 함수

isdigit(), islower(), isupper()

isdigit()은 문자열에서 사용되는 메소드로 '문자열이 숫자로 구성되어 있는가' 라는 것을 확인해 주는 메소드일 뿐이다.


``` python
>>> is_digit("123")
True
>>> is_digit("-123")
True
>>> is_digit("23.45")
True
>>> is_digit("a12")
False
```

# bisect Part

## bisect_left

``` python
def get_grade(score):
  r = (50, 60, 70, 90, 100)
  g = 'FDCBA'
  return g[bisect_left(r, score)]
```

``` python
print(get_grade(55)) # D
print(get_grade(50)) # F
print(get_grade(100)) # A
```

주어진 r에서 score가 <= 로 index를 알려준다.
즉 < <= n

100이상은 하면 깨진다.


# 가장 큰 수, 가장 작은 수

``` python
import sys
max = sys.maxsize
min = -sys.maxsize -1
```

``` python
math.inf #integer중 가장 큰 수
```
# max에서 key사용
https://stackoverflow.com/questions/18296755/python-max-function-using-key-and-lambda-expression


ddc[n]의 값을 기준으로 sort한다.

lambda is an anonymous function, it is equivalent to:
``` python
def func(p):
    return p.totalScore
```
Now max becomes:
``` python
max(players, key=func)
```

# 비트연산으로 나누기 2와 제곱승 하기

``` python

 1<<3 이면 1을 왼쪽으로 세 칸 시프트 한 것이기 때문에 2^3=8
4 >> 1
# 2
```

# list Part

## list 돌 때 편한 것

``` python
l = ['a', 'b', 'c']
for i,h in enumerate(l):
  print(i, v)

# 0 a
# 1 b
# 2 c
```

## list 의 top 구하기

``` python
s = [1,2,3]
print(s[-1])

# 3
```

# 재귀 푸는법

## sol1
1. 트리를 그림으로 그린다.
2. 말단 노드일 경우를 처리한다. -> 반환 하는 타입을 일치시켜야 함.
3. 각 자식노드에서 부모노드를 올라올 때 어떻게 처리되는지 보고 그걸 코드로 옮겨서 반환하도록 한다.

## sol2

1. 최소 패턴의 값을 저장한다.
2. 중복되는 패턴은 함수화 시켜 재귀 호출을 한다.
  - 이때 특히 신경써야할 것은 매개변수, return값
3. 최대한 크게 패턴을 나눈다.
4. 패턴의 기준점을 정한다.
5. 그 걸 기준으로 계속 함수를 시키고 쪼갤수 없는 상황일 때 패턴을 그린다.

# python에서 def 에서 return값 까지 주기

``` python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
  def definition_name(self, l1: ListNode, l2: ListNode) -> ListNode:
    return
```


-------
참고 자료:
http://seorenn.blogspot.com/2011/04/python-isdigit.html
https://wayhome25.github.io/
