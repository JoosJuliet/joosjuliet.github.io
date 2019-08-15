---
layout: post
section-type: post
title: "[sort 시리즈 1탄] [merge sort] sort algorithm with python3"
category: Algorithm
tags: [ 'algorithm', 'python', 'merge_sort' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
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

``` python
number_list = [21, 10, 12, 20, 25, 13, 15, 22]
n = len(number_list)

# 2개의 인접한 배열 list[left...mid]와 list[mid+1...right]의 합병 과정
# (실제로 숫자들이 정렬되는 과정)
def merge(number_list, left, mid, right):
    print("이거",number_list)
    sorted = [0] * n
    i = left # 정렬된 왼쪽 리스트에 대한 인덱스
    j = mid+1 # 정렬된 오른쪽 리스트에 대한 인덱스
    k = left # 정렬될 리스트에 대한 인덱스
    while i <= mid and j <= right: # 분할 정렬된 list 합병
        if number_list[i] <= number_list[j]:
            sorted[k] = number_list[i]
            k+=1; i+=1
        else:
            sorted[k] = number_list[j]
            k+=1; j+=1

    if i > mid:
        # 남아 있는 것들 일괄 복사
        if right <= 7:
            for l in range(j, right+1):
                sorted[k]= number_list[l]
                k += 1
    else:
        for l in range(i, mid+1):
            sorted[k]= number_list[l]
            k += 1

    # 배열 sorted[](임시 배열)의 리스트를 배열 number_list로 재복사
    for l in range(left, right+1):
        if right <= 7:
            number_list[l] = sorted[l]

def merge_sort(number_list, left, right):
    if left < right:
        # 둘이 역전 되면 끝나는 것이다...
        mid = (left + right)//2 # 중간 위치를 계산하여 리스트를 균등 분할 - Divide
        # print('number_list, left, mid', number_list, left, mid)
        merge_sort(number_list, left, mid) # 앞쪽 부분 리스트 정렬 - Conquer
        # print('number_list, mid+1, right', number_list, mid+1, right)
        merge_sort(number_list, mid+1, right) # 뒤쪽 부분 리스트 정렬 - Conquer
        merge(number_list, left, mid, right) # 정렬된 2개의 부분 배열을 합병하는 과정 - Combine

# 합병 정렬 수행(left: 배열의 시작, right: 배열의 끝)
merge_sort(number_list, 0, n-1)
print(number_list)
```


---
참고자료:
https://programmingfbf7290.tistory.com/entry/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%EC%9B%90%EB%A6%AC4-%EB%8B%A4%ED%98%95%EC%84%B1-%ED%94%BC%ED%84%B0-%EC%BD%94%EB%93%9C%EC%9D%98-%EC%83%81%EC%86%8D-%EA%B7%9C%EC%B9%99?category=666986

https://ratsgo.github.io/data%20structure&algorithm/2017/10/03/mergesort/
