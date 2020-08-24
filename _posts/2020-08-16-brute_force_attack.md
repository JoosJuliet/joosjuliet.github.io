---
layout: post
section-type: post
title: "how to prevent brute force attack?"
category: Architect
tags: [ 'Architect']
comments: true
---
# What is brute force attack?
when we want to solve specific password, assign the number of all cases password randomly.


# Kinds of brute force attack
- Random sequential assignment
- Dictionary assignment

## Random sequential assignment
It implement the feature of brute-force assignment, They try to assign all the strings that can be combined all possibility in order one by one. In theory, given enough time for the attack, we will get the password. However, in reality, as the length and complexity of the password increases, the time required for an attack increases exponentially, so it is difficult to say that it is one hundred percent successful. In order to reduce the time required for a list of predefined strings is sometimes used.

## Dictionary assignment
- representatives : rainbow table attack  
This is a method to shorten the time compared to the random sequential assignment method, and is a method of assigning a predefined list of strings. An attack using a dictionary file is called a dictionary attack. Pre-defined password dictionary is prepared and assigned one by one. the dictionary file is a file that has been used statistically or is a file that has previously defined password combinations that people commonly use in the form of a list. Since people use surprisingly simple passwords a lot and sometimes use the same password across different sites, the pre-assignment method is a very efficient and effective attack technique that increases the attack success rate while dramatically reducing the time required for brute force attacks.


# Preventation
## User perspectives
1. Use of long and complex passwords
2. Use unpredictable password
## Company perspectives
1. Add a several restrictions for password
2. Logging and Monitoring
  - Increase comparison time between user’s input and password.
3. Regular suggestion of password change.
4. Use Multi-factor
  - Captcha



## Add a several restrictions for password
For instance, The length must be longer than 8 and mix alphabet and number, even special character. Because The longer and more complex the password, the less likely the attack will be successful. But this is a tradeoff that can make the user's experience bad, so If the user experience is important in service, I don't recommend making a lot of restrictions.


## Increase comparison time between user’s input and password.
Most users don't complain even if the login time is increased from 0.1 seconds to one second. In other words, the fast processing speed of the login API provides greater convenience to attackers than users. Therefore, we can prevent brute force attacks by adding idle time during login. However, if attacker use parallel processing, this method would be useless. So we can use the scrypt, which is one of the powerful encryption method, is designed to have memory overhead when generating digests. Accordingly parallelization processing will be very difficult when attacker attempt a brute-force attack.



## Regular suggestion of password change.
However, even with these restrictions above, attacking can be successful if there is enough time. Thus, password change emails should be sent regularly to user.




## Captcha
However, users may not want to change their password periodically. Therefore, We need other way to solve problem. So If a certain user's login attempts are repeated or repeatedly fail, it is necessary to check unless this is user’s connection. we need to use something called captcha to distinguish people from computers.


===
reference :
https://www.youtube.com/watch?v=tK9xOWU8q-I  
http://wiki.hash.kr/index.php/%EB%AC%B4%EC%B0%A8%EB%B3%84_%EB%8C%80%EC%9E%85_%EA%B3%B5%EA%B2%A9  
