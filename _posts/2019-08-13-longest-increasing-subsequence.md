---
layout: post
section-type: post
title: "[leet_code] 300. Longest Increasing Subsequence
 with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/longest-increasing-subsequence/

# 목표:
- 가장 긴 증가하는 수열을 구하여라

# 조건:
- O(N**2)이 상한선이고, O(NlogN)이 권장이다.

# solution 1 설명 :
- O(N**2)
- dp를 써서 하는 것이다.

``` python
def lengthOfLIS(nums) -> int:
    ln = len(nums)
    if ln <= 1: return ln
    res = 1
    ls = [1]*ln
    for i in range(1, ln):
        for j in range(0,i):
            if nums[j] < nums[i]:
                ls[i] = max(ls[i], 1 + ls[j]) #j번째 수를 포함한 ls의 길이
                # 각 자리수별로 해보고 그중에서 가장 큰 것 더한다.
                # ls값들이 누적이 되있기 때문에 이미 앞에 있는 값들도 누적이 되어있다.
        res = max(res, ls[i])
    return res
```

# solution 2 설명 :
- binary search tree를 활용해서 하는 것이다.
- 일단 ls는 증가하는 수열을 담는 array이다.

- 키 포인트는 ls속의 값이 꼭 실제로 counting 되는 숫자일 필요는 없다.
- 그 속의 숫자가 중요한 게 아니라 길이가 중요한 것이니까.

- 한바퀴 돌면서 가장 큰 값보다 크면 ls에 넣는다.
- 작으면
  - 만약에 젤 작은 수보다 작으면 바꾼다.
  - 중간에 끼워 넣을 만한 곳이 있으면 자기와 가장 근접했던 큰 값을 지우고 넣는다.
- 이렇게 하는 이유는 뒤에 더 길게 이을 수 있는 substring이 있을수도 있기 때문이다.
- 그러므로 ls속의 숫자가 lengthOfLIS([1,9,10,6]) 일 때 (1,9,10)이어야 하는 데  
1,6,10이어도 상관없다.
- 어차피 그 속의 숫자가 중요한 게 아니라 길이가 중요한 것이니까.(미래에 더 긴 것이 있을 때를 위한것이다.)
  - [1,9,10,6,7]이 들어올 시 1,6,7로 가지고 있는게 뒤에 더 유리하다.


``` python
def lengthOfLIS(nums) -> int:
   ln = len(nums)
   if ln <= 1:
       return ln
   ls = [nums[0]] # 증가하는 수열을 담는 array
   for i in range(1, ln):
       if nums[i] > ls[-1]: # ls에서 가장 큰 수가 새 수보다 작으면 (증가하는 수열에 만족되면 )ls에 넣는다.
           ls.append(nums[i])
       elif nums[i] < ls[-1]: # ls에서 가장 큰 수 보다 더 작은 수면 적합한 위치에 놓는다.
           idx = binary(ls, nums[i]) # ls에 들어갈 적합한 위치를 찾아본다.
           if ls[idx] < nums[i]: continue
           ls[idx] = nums[i]

   return len(ls)
def binary(ls, num):
    ln = len(ls)
    s, e = 0, ln-1
    # print('ls',ls)
    while s <= e:
        print('ls',ls)
        mid = (e+s)//2
        if ls[mid] == num: # num이 ls의 가운대면 return -> 이미 존재한 값인것이다.
            return mid
        elif ls[mid] < num: # num이 가운데 보다 크면
            if ls[mid+1] > num: # 값이 없는 경우 이와 근접한 것보다 큰 것이니 +1
               return mid+1
            s = mid+1 # 손절
        else:
            if mid == 0:
               return mid # mid가 0이 될정도라면 젤 앞이라는 것이구먼...
            e = mid - 1 # 손절
print(lengthOfLIS([1,2,5,4]))
```
