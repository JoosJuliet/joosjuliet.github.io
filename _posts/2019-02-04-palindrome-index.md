---
layout: post
section-type: post
title: "[hacker_rank]Palindrome Index with python3, Java8"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python3', 'Java8' ]
comments: true
---

https://www.hackerrank.com/challenges/palindrome-index/problem



로직은 같다.
단지 java와 python의 차이일뿐
java에서 string을 한글자 씩 다룰 때는 charAt을 쓰는게 가장 편하다는 것을 깨달았다.
회사에서 java를 쓰고 있느데 아직 익숙치 않아서 easy는 java로도 풀 예정이다.

# JAVA8


``` JAVA
import java.util.*;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        for(int n = sc.nextInt(); n>0; n-- ){
            String s = sc.next();
            int a = 0;
            int b = s.length()-1;

            int result = -1;
            if(a == b){
                System.out.println(result);
            } else{
                while(a != b){
                    if (a == s.length()-1 || b == 0){
                        break;
                    }
                    if (s.charAt(a) == s.charAt(b)){
                        a +=1;
                        b-=1;
                    }else{
                        if (s.charAt(b-1) == s.charAt(a) && s.charAt(a+1) == s.charAt(b-2)){
                            result = b;
                            break;
                        }else{
                            result = a;
                            break;
                        }
                    }
                }
                System.out.println(result);
            }
        }
    }
}
```

# PYTHON3

``` python
for _ in range(int(input())):
    s = input()
    a, b = 0, len(s)-1
    result = -1
    if a == b:
        print(-1)
    else:
      while a != b:
          if a == len(s)-1 or b == 0:
              break
          if s[a] == s[b]:
              a, b = a+1 , b-1
          else:
              if s[a] == s[b-1] and s[a+1] == s[b-2]:
                  result = b
                  break
              else :
                  result = a
                  break

      print(result)

```
