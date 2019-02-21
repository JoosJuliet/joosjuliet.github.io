---
layout: post
section-type: post
title: "[hacker_rank] Service_Lane Solution with python3, java8"
category: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python', 'JAVA' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)

문제 : https://www.hackerrank.com/challenges/service-lane/problem

# sol1
``` python
n, t = map(int, input().rstrip().split())
width = list(map(int, input().rstrip().split()))

for _ in range(t):
    s, e = map(int, input().rstrip().split())
    print(min(width[s:e+1]))
```

# sol2
``` java
import java.util.Scanner;
import java.util.ArrayList;

public class Solution {
    public static void main (String[] args) {
        Scanner stdin = new Scanner(System.in);
        int freewayLength = stdin.nextInt();
        int numTestCases = stdin.nextInt();
        ArrayList<Integer> freeway = new ArrayList<>(freewayLength);
        for (int i = 0; i < freewayLength; i++) {
            freeway.add(stdin.nextInt());
        }
        for (int i = 0; i < numTestCases; i++) {
            int entrance = stdin.nextInt();
            int exit = stdin.nextInt();
            System.out.println(freeway.subList(entrance, exit + 1).stream().mapToInt(a -> a).min().getAsInt());
            //min의 return값이 optional이다.
        }
    }
}
```
