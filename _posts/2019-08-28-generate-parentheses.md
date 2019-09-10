---
layout: post
section-type: post
title: "[leet_code] 22. Generate Parentheses with python3"
categories: Algorithm
tags: [ 'algorithm', 'leet_code', 'python' ]
comments: true
---
문제 : https://leetcode.com/problems/generate-parentheses/



# solution1 :
- bruteforce로 다 만든다.
- 그리고 조건이 맞는지 valid검사와 길이 검사를 한다.
- 적합한 것만 넣는다.


```python
def generateParenthesis(n):
    def generate(A = []):
        if len(A) == 2*n: #개수되면
            if valid(A): #그게 적합하면
                ans.append("".join(A))
        else: # 모든 경우의 수를 여기서 다 만든다.
            A.append('(')
            generate(A)
            A.pop()
            A.append(')')
            generate(A)
            A.pop()

    def valid(A): # validation하기
        bal = 0
        for c in A:
            if c == '(': bal += 1
            else: bal -= 1
            if bal < 0: return False
        return bal == 0

    ans = []
    generate()
    return ans

```
# solution2:
- '('를 붙은 바로 뒤에 ')'가 붙게 만든다.
- 그럼 자동으로 조건에 맞는 string이 만들어진다.
- 그래서 오로지 길이만 조건문으로 걸 수 있다.

``` python

def generateParenthesis(N):
    ans = []
    def backtrack(S = '', left = 0, right = 0):
        if len(S) == 2 * N: #개수되면 append한다.
            ans.append(S)
            return
        if left < N: #left개수가 부족하면
            backtrack(S+'(', left+1, right)
        if right < left: #right 개수가 부족하면
            backtrack(S+')', left, right+1)
        # 바로 left후에 right를 붙을 수 있게 해놓았기 때문에 (다음에 )가 차례로 잘 올 수 있다.
    backtrack()
    return ans
# ()값이 나오는 이유가 (가 붙여진 후에 바로 밑에 if문이 들어가기 때문에 )가 붙어진다.
print(generateParenthesis(3))

```
---
reference:
https://leetcode.com/problems/generate-parentheses/solution/
