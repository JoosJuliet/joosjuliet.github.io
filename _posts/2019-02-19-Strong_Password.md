---
layout: post
section-type: post
title: "[hacker_rank] Strong_Password with python3, java8"
category: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python', 'JAVA' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

문제 : https://www.hackerrank.com/challenges/strong-password/problem

# sol1
O(2N)
``` python
def minimumNumber(n, password):
    numbers = set("0123456789")
    lower_case = set("abcdefghijklmnopqrstuvwxyz")
    upper_case = set("ABCDEFGHIJKLMNOPQRSTUVWXYZ")
    special_characters = set("!@#$%^&*()-+")
    password_set = set(password)
    count = 0
    if len(password_set & numbers) == 0:
        count+=1
    if len(password_set & lower_case) == 0:
        count+=1
    if len(password_set & upper_case) == 0:
        count+=1
    if len(password_set & special_characters) == 0:
        count+=1

    # count는 1이여야 한다.
    return max(count,6-n)
```

#sol2
O(N)

``` python
def minimumNumber(n, password):
    count = 0    
    if any(i.isdigit() for i in password)==False:
        count+=1
    if any(i.islower() for i in password)==False:
        count+=1
    if any(i.isupper() for i in password)==False:
        count+=1
    if any(i in '!@#$%^&*()-+' for i in password)==False:
        count+=1
    return max(count,6-n)
```
https://www.hackerrank.com/challenges/strong-password/forum
jay_mistry456's answer


# solution3

``` java
static int minimumNumber(int n, String password) {
        boolean lowercase = false;
        boolean uppercase = false;
        boolean number = false;
        boolean special = false;
        char[] schars = "!@#$%^&*()-+".toCharArray();
        Set<Character> cs = new HashSet<>();
        for (char c : schars) {
            cs.add(c);
        }
        for (int i = 0; i < n; i++) {
            char c = password.charAt(i);
            if (c >= '0' && c <= '9') number = true;
            if (c >= 'a' && c <= 'z') lowercase = true;
            if (c >= 'A' && c <= 'Z') uppercase = true;
            if (cs.contains(c)) special = true;
        }
        int need = 0;
        need += lowercase ? 0 : 1;
        need += uppercase ? 0 : 1;
        need += number ? 0 : 1;
        need += special ? 0 : 1;
        return n + need < 6 ? 6 - n : need;
    }
```
