---
layout: post
section-type: post
title: "[leet_code] Search in Rotated Sorted Array with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---

문제 :
https://leetcode.com/problems/add-two-numbers/

# 목표:
- array속에서 target 숫자의 위치를 찾자.


# 조건:
- 복잡도 O(logN)
- array의 원소에 중복된 값은 없다.
- rotate로 인해 섞인 곳을 제외하고는 연속된 수들은 증가한다.


# solution 설명 :
- keypoint는 반으로 나눴을 때 오른쪽이든, 왼쪽이든 무조건 오름차순인 부분이 있다.
- 오름차순 구간은 값이 보장되어 있으니 값의 범위를 줄이는데 사용할 수 있다.
  - 오름차순인 부분에 값이 들어 있으면 rotate가 들어간 부분을 날린다.
  - rotate된 부분에 값이 들어 있으면 오름차순으로 되어있는 부분을 날린다.

``` python
class Solution:
  def search(self, nums: List[int], target: int) -> int:
    if not nums:
      return -1

    low, high = 0, len(nums) - 1

    while low <= high: # 멈출 수 있는 제한조건
      mid = (low + high) // 2
      if target == nums[mid]:
        return mid #값을 찾는다.
      if nums[low] <= nums[mid]: # 왼쪽이 오름차순일 때
        if nums[low] <= target <= nums[mid]: # target이 오름차순 속에 있을 때
          high = mid - 1
        else: # target이 ratoate된 곳 속에 있을 때
          low = mid + 1
      else: # 오른쪽이 오름차순일 때
        if nums[mid] <= target <= nums[high]: # target이 오름차순 속에 있을 때
          low = mid + 1
        else: # target이 ratoate된 곳 속에 있을 때
          high = mid - 1
  return -1
```

---
출처:
https://leetcode.com/problems/search-in-rotated-sorted-array/discuss/14437/Python-binary-search-solution-O(logn)-48ms
코드
