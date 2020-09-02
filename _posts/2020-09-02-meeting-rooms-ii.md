---
layout: post
section-type: post
title: "meeting-rooms-ii solution"
category: Algorithm
tags: [ 'algorithm', 'python' ]
comments: true
---
# 목표:
# 조건:
# solution 설명 :

문제 : https://leetcode.com/problems/meeting-rooms-ii/  

``` python
from queue import PriorityQueue
# 그 당시에 가장 작은 end의 값을 저장해 놓는다. pq에 -> minheap
def minMeetingRooms(intervals) -> int:

    if not intervals:
        return 0

    intervals.sort()
    pq = PriorityQueue()
    # Add the first element into pq
    pq.put(intervals[0][1])
#         end를 큐에 넣는다.

    for start, end in intervals[1:]:
        print(len(pq.queue))
        if start >= pq.queue[0]:
#               전의 것 엔드보다 스타트가 크거나 같으면 확인 만약에 그러면 뺀다
            pq.get()
#         그다음에 end를 pq에 저장한다.
        pq.put(end)

    for i in pq.queue:
        print(i)
    return len(pq.queue)

minMeetingRooms([[0,30],[5,10],[15,20]])

# - 우리는 미팅을 솔팅한다. 스타트 타임으로, 그다음에 순차적으로 각 방에 미팅을 할당한다.

# - 미팅이 끝나면 그거슨 재사용할 수 있으니 체크를 해준다.
# - 가장 빠른 종료회의를 추적하기 위해 최소 힙을 사용한다.
# - 새 회의가 시작되기 전에 이전 회의가 종료 될 때마다 회의실을 재사용합니다.
```
