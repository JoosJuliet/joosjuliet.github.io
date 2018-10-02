---
layout: post
section-type: post
title: "[hacker_rank] Java BigDecimal with Java"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank' ]
comments: true
---

``` JAVA
import java.math.BigDecimal;
import java.util.*;
class Solution{

    public static void main(String []args){
        //Input
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        String []s = new String[n+2];
        for(int i = 0; i<n; i++){
            s[i] = sc.next();
        }
      	sc.close();

        //Write your code here
        String newArray[] = new String[n];
        for(int i= 0;i < newArray.length; i++){
            newArray[i] = s[i];
        }

        Arrays.sort(newArray, Collections.reverseOrder(new Comparator<String>() {
        @Override
            public int compare(String a1, String a2) {
                BigDecimal a = new BigDecimal(a1);
                BigDecimal b = new BigDecimal(a2);
                return a.compareTo(b);
            }
        }));

        s = newArray;
        for(int i=0; i<n; i++){
          System.out.println(s[i]);
        }
  }

}
```
