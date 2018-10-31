---
layout: post
section-type: post
title: "[ 작성중 ] 부동소수점 (with. python3, java)"
categories: Computer_Science
tags: [ 'computer_science' ]
comments: true
---

불행히도, 대부분의 십진 소수는 정확하게 이진 소수로 표현될 수 없다.
결과적으로, 일반적으로 입력하는 십진 부동 소수점 숫자가 실제로 기계에 저장될 때는 이진 부동 소수점 수로 근사 될 뿐이다.

분수 1/3로 생각해보면 쉽다.

1/3을 십진 소수로 근사하면 아무리 정확하게 해도
```
0.333333333
```
이어서 아무리 많은 자릿수를 적어도 결과가 정확하게 1/3이 될 수 없지만, 점점 더 1/3에 가까운 근사치가 됩니다.

같은 방식으로, 아무리 많은 자릿수의 숫자를 사용해도, 십진수 0.1은 이진 소수로 정확하게 표현될 수 없습니다. 이진법에서, 1/10은 무한히 반복되는 소수입니다
```
0.0001100110011001100110011001100110011001100110011...
```

유한 한 비트 수에서 멈추면, 근삿값을 얻게 됩니다.

많은 사용자는 값이 표시되는 방식 때문에 근사를 인식하지 못합니다. 파이썬은 기계에 저장된 이진 근삿값의 진짜 십진 값에 대한 십진 근삿값을 인쇄할 뿐입니다. 대부분 기계에서, 만약 파이썬이 0.1로 저장된 이진 근삿값의 진짜 십진 값을 출력한다면 다음과 같이 표시해야 합니다

```
>>> 0.1
0.1000000000000000055511151231257827021181583404541015625
```
이것은 대부분 사람이 유용하다고 생각하는 것보다 많은 숫자이므로, 파이썬은 반올림된 값을 대신 표시하여 숫자를 다룰만하게 만듭니다

```
>>> 1 / 10
0.1
```
*인쇄된 결과가 정확히 1/10인 것처럼 보여도, 실제 저장된 값은 가장 가까운 표현 가능한 이진 소수임을 기억하세요.*

좀 더 만족스러운 결과를 얻으려면,
```
>>> format(math.pi, '.12g')  # give 12 significant digits
'3.14159265359'

>>> format(math.pi, '.2f')   # give 2 digits after the point
'3.14'

>>> repr(math.pi)
'3.141592653589793'
```
*이것이 환영임을 깨닫는 것이 중요합니다*
단순히 진짜 기곗값의 표시 를 반올림하는 것일 뿐입니다.

# 환영임을 보여주는 예
```
>>> .1 + .1 + .1 == .3
False
```

나아지게 하기 위해

```
>>> round(.1, 1) + round(.1, 1) + round(.1, 1) == round(.3, 1)
False
```
이런식으로 해도 소용없습니다.

0.1은 1/10의 정확한 값에 더 가까워질 수 없고, 0.3도 3/10의 정확한 값에 더 가까워질 수 없으므로, round() 함수로 미리 반올림하는 것은 도움이 되지 않습니다.

```
>>> round(.1 + .1 + .1, 10) == round(.3, 10)
True
```

숫자를 의도한 정확한 값에 더 가깝게 만들 수는 없지만, round() 함수는 사후 반올림에 유용하여 부정확한 값을 가진 결과를 서로 비교할 수 있게 합니다:


부동 소수점수를 지나치게 경계할 필요는 없습니다!
파이썬 float 연산의 에러는 연산당 2**53분의 1을 넘지 않는 규모이다


그러나 정확하게 사용해야 하는 경우
decimal 모듈과 fractions 모듈을 사용하면 된다.

# float의 정확한 값 아는 법

```
>>> x = 3.14159
>>> x.as_integer_ratio()
(3537115888337719, 1125899906842624)
```

# sum을 더 정확하게 아는 법
누적 합계에 값이 더해지면서 "잃어버린 숫자들"을 추적합니다.
```
>>> sum([0.1] * 10) == 1.0
False
>>> math.fsum([0.1] * 10) == 1.0
True
```

# fractions와 decimal

## fractions

``` python
>>> from fractions import Fraction

>>> Fraction.from_float(0.1)
Fraction(3602879701896397, 36028797018963968)

>>> (0.1).as_integer_ratio()
(3602879701896397, 36028797018963968)
```

## decimal 쓰는 법


``` python
>>> from decimal import Decimal
>>> Decimal.from_float(0.1)
Decimal('0.1000000000000000055511151231257827021181583404541015625')

>>> format(Decimal.from_float(0.1), '.17')
# 0.1을 17자리 수 까지 정확하게 나타내는 법
'0.10000000000000001'
```




# JAVA로 보자

``` java
float floatValue() //값을 float형으로 반환
double doubleValue() //값을 double형으로 반환
BigInteger toBigInteger() //값을 BigInteger로 반환 (소수점 아래는 날아감)



BigDecimal add(BigDecimal augend) //덧셈 + 연산
BigDecimal subtract(BigDecimal subtrahend) //뺄셈 - 연산
BigDecimal multiply(BigDecimal multiplicand) //곱셈 * 연산
BigDecimal divide(BigDecimal divisor) //나눗셈 / 연산
BigDecimal remainder(BigDecimal divisor) //나머지 % 연산


// 일반 실수형을 연산할 때는 어떤 결과가 일어나는지 살펴보자.


//        double d1 = 1.0;
//        double d2 = 0.1;
//
//
//
//        for(int i=0; i<5; ++i){
//            d1 += d2;
//            System.out.println(d1);
//        }



//        결과 :

//        1.1
//        1.2000000000000002
//        1.3000000000000003
//        1.4000000000000004
//        1.5000000000000004
BigDecimal의 생성자는 여러가지가 있지만,

가장 정확한 계산을 하려면 문자열을 인자로 하는 생성자를 사용해야 한다.

실수형 인자를 사용하면 정확한 계산의 의미가 없어진다


double d1 = 1.0;
double d2 = 0.1;



BigDecimal bd1 = new BigDecimal(String.valueOf(d1));
BigDecimal bd2 = new BigDecimal(String.valueOf(d2));



for(int i=0; i<5; ++i){
    bd1 = bd1.add(bd2);
    System.out.println(bd1.toString());
}



//        결과 :
//
//        1.1
//        1.2
//        1.3
//        1.4
//        1.5
```
차후에 추가할 내용
https://www.evernote.com/l/Akzeei1_maZP_7JA8YUqaXOLPDi_X1aOqxU
madeby(wkdtjsgur100)

---
참고자료:
https://docs.python.org/ko/3.6/tutorial/floatingpoint.html
