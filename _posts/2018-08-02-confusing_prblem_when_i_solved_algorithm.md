---
layout: post
section-type: post
title: "[ 작성중 ] 알고리즘 풀 때 팁 (feat. python)"
categories: Algorithm
tags: [ 'algorithm' ]
comments: true
---

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
key파라미터에는 함수가 와야 한다. key 파라미터에 함수가 설정되면 소트해야 할 리스트들의 항목들이 하나씩 key 함수에 전달되어 key 함수가 실행되게 된다. 이 때 수행된 key 함수의 리턴값을 기준으로 소트가 진행된다.

위 예에서는 key함수에 students의 요소인 튜플데이터가 key함수의 입력으로 순차적으로 전달될 것이다. key함수는 입력된 튜플 데이터의 "나이"를 의미하는 2번째 항목을 리턴하는 lambda함수이다. 따라서 sorted수행 후 나이순으로 소트된 리스트가 리턴된다.

``` python
sorted(student_objects, key=attrgetter('age'), reverse=True)
# [('dave', 32, 'B'), ('jane', 22, 'A'), ('sally', 17, 'B')]
```

reverse=True 넣으면 역순으로 된다


## 역순 포문
``` python
>>> for i in range(10, 0, -1):    # 10에서 1까지 역순으로 숫자 생성
...     print('Hello, world!', i)

>>> for i in reversed(range(10)):    # range에 reversed를 사용하여 숫자의 순서를 반대로 뒤집음
...     print('Hello, world!', i)    # 9부터 0까지 10번 반복
```
## Counter
``` python
from collections import Counter # 콜렉션에서 불러옵니다.
def pickingNumbers(a):
  d = Counter(a)
```

## permutation
``` python
from itertools import permutations

# Complete the formingMagicSquare function below.
def formingMagicSquare(s):
  comb = permutations(range(1,10),9)
  # 1부터 10까지 9개를 permutation한다
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
