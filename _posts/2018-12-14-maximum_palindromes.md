---
layout: post
section-type: post
title: "(작성중)[hacker_rank] Maximum Palindromes with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

문제 :
https://www.hackerrank.com/challenges/maximum-palindromes/problem

밑에 풀이는 시간초과가 나는데 이 것을 해결하기 위해서

So to review what we needed to know to implement the solution: 1. A billion and 7 is prime. 2. Basic modular arithmetic 3. Fermat's little theorem 4. Exponentiation by squaring 5. Precomputing tricks

를 알아야한다.

``` python
from collections import Counter # 콜렉션에서 불러옵니다.
from math import factorial

# 홀수개의 2로 나눈 나머지들의 개수
s = input()
for _ in range(int(input())):
    l, r = map(int, input().split())
    print(s[l-1:r])
    count_s = Counter(s[l-1:r])
    print(count_s)
    odd_number = 0

    sum_of_even_numbers_factorial = 1
    sum_of_even_number = 0
    for i in count_s:
        sum_of_even_numbers_factorial *= factorial(count_s[i]//2)
        sum_of_even_number += count_s[i]//2
        if count_s[i]%2 == 1 :# 홀수인것은 더해줘야한다.
            odd_number += 1

    ans = 0
    if odd_number == 0:
        ans = factorial(sum_of_even_number) // sum_of_even_numbers_factorial
    else:
        ans = factorial(sum_of_even_number) // sum_of_even_numbers_factorial * odd_number

    print(ans % (10**9+7))
    # print('----------')

```


https://www.hackerrank.com/challenges/maximum-palindromes/forum
에서 RocketshipToastr의 답변

즉 공부를 해야안다.

----

Hints for people tearing their hair out

I'm assuming you've come to the conclusion that you're trying to calculate

(A + B + ... + Z)!/(A! B! ... Z!) mod M

where A, B, ..., Z are the number of a's, b's, ..., z's in the given interval (of course, you also have to take into account the number of characters that can be used in the middle of the palindrome).

First off, make sure you're properly working in mod M. Don't just apply "% M" to all the numbers before dividing.

Take for example the number of ways to arrange the letters of the word "cool". The answers is 4!/2! = 12. The answer mod 7 is 5. Here's what happens when we just take all the factorials mod 7 before using them.

4! mod 7 = 24 mod 7 = 3. 2! mod 7 = 2

Now if we divide, we'd get 3/2.

The problem is that dividing by 2! in mod 7 is actually multiplying by 4. (Compare this to how dividing by 2 in normal arithmetic is actually multiplying by 0.5)

So how do we find the modular multiplicative inverses? There's a couple of ways but since M is prime (it is!) we can use Fermat's Little Theorem to help us out. Fermat's Little Theorem states that if p is prime then a^(p-1) = 1 mod p. Note that this means a^(p-2) is the multiplicative inverse of a. Since M is over a billion, this seems infeasible given that we have to do this for a bunch of numbers. However, that's where the exponentiation by squaring comes in. Don't forget to take your answer mod M after every square and multiplication.

Finally, precompute your factorials, their inverses, as wells as the frequencies of each character up to i for i in [0, |s|].

So to review what we needed to know to implement the solution: 1. A billion and 7 is prime. 2. Basic modular arithmetic 3. Fermat's little theorem 4. Exponentiation by squaring 5. Precomputing tricks
