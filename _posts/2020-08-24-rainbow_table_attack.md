---
layout: post
section-type: post
title: "(in progress)rainbow table attack"
category: Security
tags: [ 'Security', 'english' ]
comments: true
---

### rainbow table attack (따로 파야할듯)
- Why this attack is born?
because hash have no decryption algorithm. so just compare hash value and anticipate decrypted password.
so this is need to beforehand attack first, and make dictionary table for searching password.

- Process

1. Create a hash dictionary using a hash function from 0 to 9999.
2. Hacker steals a DB that contains various hash passwords.
3. Find out what the original password is.

- What is rainbow table?
A table that contains a lot of values that can be generated using a hash function

- Prevent Solution
using salt
that means, encrypt with random word in password.

---
reference : https://namu.wiki/w/%EB%A0%88%EC%9D%B8%EB%B3%B4%EC%9A%B0%20%ED%85%8C%EC%9D%B4%EB%B8%94
