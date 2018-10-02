---
layout: post
section-type: post
title: "python operations time complexity"
categories: Python
tags: [ 'Python3', 'time_complexity', 'python_operations', 'python' ]
comments: true
---

## lists

Operation     | Example      | Big-O         | Notes|
--------------|--------------|---------------|-------------------------------|
Index         | l[i]         | O(1)	         ||
Store         | l[i] = 0     | O(1)	         ||
*Length*      | len(l)       | O(1)	         ||
Append        | l.append(5)  | O(1)	         ||
Pop	          | l.pop()      | O(1)	         |  l.pop(-1) 과 동일|
Clear         | l.clear()    | O(1)	         | l = [] 과 유사|
Slice         | l[a:b]       | O(b-a)	       | l[:] : O(len(l)-0) = O(N)|
Extend        | l.extend(...)| O(len(...))   | 확장 길이에 따라 |
Construction  | list(...)    | O(len(...))   | 요소 길이에 따라 |
check ==, !=  | l1 == l2     | O(N)          | 비교 |
Insert        | ㅣ.insert(i, v) | O(N)	       | i 위치에 v를 추가|
*Delete*      | del l[i]     | O(N)	         ||
Remove        | l.remove(...)| O(N)	         ||
*Containment* | x in/not in l| O(N)	         | 검색|
Copy          | l.copy()     | O(N)	         | l[:] 과 동일 - O(N)|
*Pop*	        | l.pop(i)     | O(N)	         | l.pop(0):O(N)|
*Extreme value* | min(l)/max(l)| O(N)	       | 검색|
*Reverse*	    | l.reverse()  | O(N)	         | 그대로 반대로|
Iteration     | for v in l:  | O(N)          ||
*Sort*        | l.sort()     | O(N Log N)    ||
Multiply      | k*l          | O(k N)        | [1,2,3] * 3 >> O(N**2)|


python sort 알고리즘은 Timsort이다.
참고자료 : [https://medium.com/@fiv3star/python-sorted-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-timsort-dca0ec7a08be]

## Dictionaries: dict and defaultdict


Operation     | Example      | Big-O     | Notes |
--------------|---------------|------------|---------|
Index         | d[k]         | O(1)	     ||
Store         | d[k] = v     | O(1)	     ||
*Length*      | len(d)       | O(1)	     ||
*Delete*      | del d[k]     | O(1)	     ||
get/setdefault| d.method     | O(1)	     ||
Pop           | d.pop(k)     | O(1)	     ||
Pop item      | d.popitem()  | O(1)	     ||
Clear         | d.clear()    | O(1)	     | s = {} or = dict() 유사|
View          | d.keys()     | O(1)	     | d.values() 동일|
Construction  | dict(...)    | O(len(...))   | |
Iteration     | for k in d:  | O(N)          | |

... dict 만세


## Sets

Operation     | Example      | Class         | Notes
--------------|--------------|---------------|-------------------------------
*Length*      | len(s)       | O(1)	     |
Add           | s.add(5)     | O(1)	     |
*Containment* | x in/not in s| O(1)	     | compare to list/tuple - O(N)
*Remove*      | s.remove(..) | O(1)	     | compare to list/tuple - O(N)
Discard       | s.discard(..)| O(1)	     |
Pop           | s.pop()      | O(1)	     | popped value "randomly" selected
Clear         | s.clear()    | O(1)	     | similar to s = set()
Construction  | set(...)     | O(len(...))   | depends on length of ... iterable
check ==, !=  | s != t       | O(len(s))     | same as len(t); False in O(1) if the lengths are different
<=/<          | s <= t       | O(len(s))     | issubset
`>=/>`        | s >= t       | O(len(t))     | issuperset s <= t == t >= s
Union         | s | t        | O(len(s)+len(t))
Intersection  | s & t        | O(len(s)+len(t))
Difference    | s - t        | O(len(s)+len(t))
Symmetric Diff| s ^ t        | O(len(s)+len(t))

Iteration     | for v in s:  | O(N)          | Worst: no return/break in loop
Copy          | s.copy()     | O(N)	     |


set 만세...

---
참고자료:
https://www.ics.uci.edu/~brgallar/week8_2.html
