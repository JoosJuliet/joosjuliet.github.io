---
layout: post
section-type: post
title: "[hacker_rank] Flipping the Matrix with python3, java8"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---

제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)


문제 : https://www.hackerrank.com/challenges/flipping-the-matrix/problem

``` python
for _ in range(int(input())):
    n = int(input())
    accumulated = 0
    matrix = [list(map(int, input().split())) for _ in range(2*n)]

    for i in range(n):
        for j in range(n):
            accumulated += max(matrix[i][j],
                        matrix[2*n-i-1][j],
                        matrix[i][2*n-j-1],
                        matrix[n*2-i-1][n*2-j-1])

    print(accumulated)

```

``` java

import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int q = in.nextInt();
        while (q-- > 0) {
            int n = in.nextInt();
            int[][] matrix = new int[2 * n][2 * n];
            for (int i = 0; i < 2 * n; ++i) {
                for (int j = 0; j < 2 * n; ++j) {
                    matrix[i][j] = in.nextInt();
                }
            }

            int accumulated = 0;
            for (int i = 0; i < n; ++i) {
                for (int j = 0; j < n; ++j) {
                    accumulated +=
                            Math.max(
                                    Math.max(matrix[i][j], matrix[2 * n - 1 - i][j]),
                                    Math.max(matrix[i][2 * n - 1 - j], matrix[2 * n - 1 - i][2 * n - 1 - j])
                            );
                }
            }

            System.out.println(accumulated);
        }
    }
}

```
