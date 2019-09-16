---
layout: post
section-type: post
title: "[sort 시리즈 2탄] 삽입정렬(insertion sort) with python3"
category: Algorithm
tags: [ '삽입정렬', 'insertion_sort', 'sort' ]
comments: true
---
이 컨텐츠는 시리즈물입니다.  

- [sort 시리즈 intro]
  - sorting algorithm (with. python3)
    - https://joosjuliet.github.io/sort/

- [sort 시리즈]
  - [sort 시리즈 1탄] [merge sort] sort algorithm with python3
    - https://joosjuliet.github.io/merge_sort/
  - [sort 시리즈 2탄] 삽입정렬(insertion sort) with python3
    - https://joosjuliet.github.io/insertion_sort/

- [sort 시리즈 번외편]
  - [python] python의 기본 sort tim_sort란!
    - https://joosjuliet.github.io/tim_sort/

---



# insertion sort의 과정
![insertion_sort_process](/images/2019-08-15-insertion_sort/insertion-sort-process.png)

- 1회전: 두 번째 자료인 5를 Key로 해서 그 이전의 자료들과 비교한다.  
  - Key 값 5와 첫 번째 자료인 8을 비교한다. 8이 5보다 크므로 8을 5자리에 넣고 Key 값 5를 8의 자리인 첫 번째에 기억시킨다.
- 2회전: 세 번째 자료인 6을 Key 값으로 해서 그 이전의 자료들과 비교한다.
  - Key 값 6과 두 번째 자료인 8을 비교한다. 8이 Key 값보다 크므로 8을 6이 있던 세 번째 자리에 기억시킨다.
  - Key 값 6과 첫 번째 자료인 5를 비교한다.
  - 5가 Key 값보다 작으므로 Key 값 6을 두 번째 자리에 기억시킨다.




# 삽입 정렬(insertion sort) 알고리즘의 구체적인 개념
- 삽입 정렬은 두 번째 숫자부터 시작한다.
- 그 앞(왼쪽)의 숫자들과 비교하여 삽입할 위치를 지정한 후 숫자를 뒤로 옮기고 지정한 자리에 숫자를 삽입하여 정렬하는 알고리즘이다.
- 두 번째 숫자는 첫 번째 숫자, 세 번째 숫자는 두 번째와 첫 번째 숫자,
- 즉 최악의 경우 n번째 숫자가 n-1 개의 숫자를 비교할 수 있다.
- 숫자가 삽입될 위치를 찾았다면 그 위치에 삽입하기 위해 숫자를 한 칸씩 뒤로 이동시킨다.




# 삽입 정렬(insertion sort) 알고리즘의 특징
- 장점
  - 레코드의 수가 적을 경우 알고리즘 자체가 매우 간단하므로 다른 복잡한 정렬 방법보다 유리할 수 있다.
  - 대부분의 레코드가 이미 정렬되어 있는 경우에 매우 효율적일 수 있다.
- 단점
  - 비교적 많은 레코드들의 이동을 포함한다.
  - 레코드 수가 많고 레코드 크기가 클 경우에 적합하지 않다.




# 삽입 정렬(insertion sort)의 시간복잡도
- 최선의 경우
  - 비교를 바로 앞만 하기 때문에 O(1)이고, array를 한번 도는 n의 시간복잡도만 필요해진다.
  - 이동 없이 1번의 비교만 이루어진다면 *O(n)*
- 최악(Worst)의 경우(입력 자료가 역순일 경우)
  - 비교
    - 각 n번째 마다 n-1번의 비교를 한다.
    - (n-1) + (n-2) + … + 2 + 1 = n(n-1)/2 = O(n^2)
  - 교환
    - 교환을 할 때 각 숫자마다 다 비켜줘야한다.
    - (n-1) + (n-2) + … + 2 + 1 = n(n-1)/2 = O(n^2)




# python으로 개발하기
``` python
def insertionSort(arr):
    for i in range(1, len(arr)): # 2번째 숫자부터 한다.
        key = arr[i] # 미리 key에다가 arr[i]값을 저장해 놓는다.
        j = i-1 # 바로 직전의 index에 있는 숫자부터 한다.

        while j >= 0 and key < arr[j] : # 적합한 자리를 주기 위해 이동을 시킨다.
                arr[j + 1] = arr[j]
                j -= 1
        # j로 적합한 자리를 찾는다.

        arr[j + 1] = key
        break

arr = [12, 11, 13, 5, 6]
insertionSort(arr)
```

---
참고 :
https://gmlwjd9405.github.io/images/algorithm-insertion-sort/insertion-sort.png
geek for geeks

insertion_sort_process 사진출처:
https://gmlwjd9405.github.io/images/algorithm-insertion-sort/insertion-sort.png
