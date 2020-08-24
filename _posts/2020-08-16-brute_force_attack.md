---
layout: post
section-type: post
title: "how to prevent brute force attack?"
category: Architect
tags: [ 'Architect']
comments: true
---
# What is a brute-force attack?

A brute-force attack occurs when someone wants to find a specific password, so they test various configurations of all potential passwords randomly.


# Kinds of brute-force attacks
The kinds of brute-force attacks include random sequential assignment and dictionary assignment.
- Random sequential assignment
- Dictionary assignment

## Random sequential assignment
This method implements the brute-force assignment strategy by trying to guess all the possible combined strings of characters that can form a password, in order, one-by-one. In theory, if given enough time for the attack, this method will eventually find the password. However, in reality, as the length and complexity of the password increases, the time required for an attack increases exponentially, so it is difficult to say that it could be one hundred percent successful. In order to reduce the time required, a list of predefined strings is sometimes used.

## Dictionary assignment
- representatives : rainbow table attack  
One example of a dictionary assignment is the rainbow table attack.
This is a method to shorten the time used compared to the random sequential assignment method, and it is a method of assigning a predefined list of strings. An attack using a dictionary file is called a dictionary attack. A predefined password dictionary is prepared and assigned one by one. The dictionary file is a file that has been used statistically, or that contains previously defined password combinations that people commonly use in the form of a list. Since people use surprisingly simple passwords a lot and sometimes use the same password across different sites, the pre-assignment method is a very efficient and effective attack technique that increases the attack success rate while dramatically reducing the time required for brute force attacks.


# Preventation
There are a couple of methods we can turn to in order to prevent brute-force attacks. First of all, from a user perspective, I would advise people to use long and complex passwords, and also to use unpredictable passwords - what that means is different passwords for each account or website.
Second of all, from a company perspective, I would advise adding several restrictions for passwords, increased logging and monitoring of server/user activity, and also regularly changing passwords. Finally, I would recommend companies to use a multi-factor login approach, such as Captcha.


Let me explain further:

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
