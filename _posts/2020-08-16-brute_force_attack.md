---
layout: post
section-type: post
title: "how to solve brute force attack?"
category: Architect
tags: [ 'Architect']
comments: true
---
# 1. Add a several restrictions for password
For instance, The length must be longer than 8 and mix alphabet and number, even special character. Because The longer and more complex the password, the less likely the attack will be successful. But this is a tradeoff that can make the user's experience bad, so If the user experience is important in service, I don't recommend making a lot of restrictions.




# 2. Increase comparison time between user’s input and password.
Most users don't complain even if the login time is increased from 0.1 seconds to one second. In other words, the fast processing speed of the login API provides greater convenience to attackers than users. Therefore, we can prevent brute force attacks by adding idle time during login. However, if attacker use parallel processing, this method would be useless. So we can use the scrypt, which is one of the powerful encryption method, is designed to have memory overhead when generating digests. Accordingly parallelization processing will be very difficult when attacker attempt a brute-force attack.




# 3. Regular suggestion of password change.
However, even with these restrictions above, attacking can be successful if there is enough time. Thus, password change emails should be sent regularly to user.




# 4. Captcha
However, users may not want to change their password periodically. Therefore, We need other way to solve problem. So If a certain user's login attempts are repeated or repeatedly fail, it is necessary to check unless this is user’s connection. we need to use something called captcha to distinguish people from computers.
