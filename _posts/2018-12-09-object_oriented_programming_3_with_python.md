---
layout: post
section-type: post
title: "[object_oriented_programming 3편] 상속, 서브 클래스 feat.python"
category: Computer_Science
tags: [ 'object_oriented_programming', '글또1기', 'python', 'computer_science' ]
comments: true
---

# 상속과 서브 클래스
상속이란
> 한 번 정의한 데이터 타입을 필요에 따라서 수정을 하고 다시 재활용해서 반복되는 코드를 줄이고자 하는 목적

``` python
class Unit(object):
    def __init__(self, rank, size, life):
        self.name = self.__class__.__name__
        self.rank = rank
        self.size = size
        self.life = life

    def show_status(self):
        print('이름: {}'.format(self.name))
        print('등급: {}'.format(self.rank))
        print('사이즈: {}'.format(self.size))
        print('라이프: {}'.format(self.life))


class Goblin(Unit):
    pass

goblin_1 = Goblin('병사', 'Small', 100)

goblin_1.show_status()
print(Goblin.__dict__)
#{'__doc__': None, '__module__': '__main__'}

print(help(Goblin))
```
을 보면
| Methods inherited from Unit: |
| init(self, rank, size, life) |
| show_status(self)
이렇게 나온다. 즉 Golin은 Unit을 상속 받아 innit,show_status를 참조한다.


``` python
class Unit(object):
    def __init__(self, rank, size, life):
        self.name = self.__class__.__name__
        self.rank = rank
        self.size = size
        self.life = life

    def show_status(self):
        print('이름: {}'.format(self.name))
        print('등급: {}'.format(self.rank))
        print('사이즈: {}'.format(self.size))
        print('라이프: {}'.format(self.life))


class Goblin(Unit):
    def __init__(self, rank, size, life, attack_type):
        self.name = self.__class__.__name__
        self.rank = rank
        self.size = size
        self.life = life
        self.attack_type = attack_type

    def show_status(self):
        print('이름: {}'.format(self.name))
        print('등급: {}'.format(self.rank))
        print('사이즈: {}'.format(self.size))
        print('라이프: {}'.format(self.life))
        print('공격 타입: {}'.format(self.attack_type))

goblin_1 = Goblin('병사', 'Small', 100, '근접 공격')

goblin_1.show_status()
```


출력결과:
```
$ python oop_5.py
이름: Goblin
등급: 병사
사이즈: Small
라이프: 100
공격 타입: 근접 공격
```
이렇게 상위 클래스의 메소드를 자신의 클래스 안에 다시 정의하는 것을 메소드 오버라이드라고 하며, 이런 경우에는 super() 함수를 사용하여 이미 부모 클래스에서 정의된 메소드를 호출하여 같은 코드를 반복하지 않도록 합니다.
super()를 사용해 리팩토링 해보겠습니다.

``` python
class Unit(object):
    def __init__(self, rank, size, life):
        self.name = self.__class__.__name__
        self.rank = rank
        self.size = size
        self.life = life

    def show_status(self):
        print('이름: {}'.format(self.name))
        print('등급: {}'.format(self.rank))
        print('사이즈: {}'.format(self.size))
        print('라이프: {}'.format(self.life))


class Goblin(Unit):
    def __init__(self, rank, size, life, attack_type):
        super(Goblin, self).__init__(rank, size, life)
        self.attack_type = attack_type

    def show_status(self):
        super(Goblin, self).show_status()
        print('공격 타입: {}'.format(self.attack_type))

goblin_1 = Goblin('병사', 'Small', 100, '근접 공격')

goblin_1.show_status()
```
이것이 메소드 오버라이드(method override)!!!

``` python
class Unit(object):
    def __init__(self, rank, size, life):
        self.name = self.__class__.__name__
        self.rank = rank
        self.size = size
        self.life = life

    def show_status(self):
        print('이름: {}'.format(self.name))
        print('등급: {}'.format(self.rank))
        print('사이즈: {}'.format(self.size))
        print('라이프: {}'.format(self.life))


class Goblin(Unit):
    # damage 속성 추가
    def __init__(self, rank, size, life, attack_type, damage):
        super(Goblin, self).__init__(rank, size, life)
        self.attack_type = attack_type
        self.damage = damage

    def show_status(self):
        super(Goblin, self).show_status()
        print('공격 타입: {}'.format(self.attack_type))
        # 오버라이드 메소드
        print ('데미지: {}'.format(self.damage))


    # 공격 메소드 추가
    def attack(self):
        print('[{}]이 공격합니다! 상대방 데미지({})'.format(self.name, self.damage))


class SphereGoblin(Goblin):
    def __init__(self, rank, size, life, attack_type, damage, sphere_type):
        super(SphereGoblin, self).__init__(rank, size, life, attack_type, damage)
        self.sphere_type = sphere_type

    def show_status(self):
        super(SphereGoblin, self).show_status()
        print('창 타입: {}'.format(self.sphere_type))


sphere_goblin_1 = SphereGoblin('병사', 'Small', 100, '레인지 공격', 10, '긴 창')

sphere_goblin_1.show_status()
# 출력 결과:
# $ python oop_5.py
# 이름: SphereGoblin
# 등급: 병사
# 사이즈: Small
# 라이프: 100
# 공격 타입: 레인지 공격
# 데미지: 10
# 창 타입: 긴 창
```
```python
class Unit(object):
    def __init__(self, rank, size, life):
        self.name = self.__class__.__name__
        self.rank = rank
        self.size = size
        self.life = life

    def show_status(self):
        print('이름: {}'.format(self.name))
        print('등급: {}'.format(self.rank))
        print('사이즈: {}'.format(self.size))
        print('라이프: {}'.format(self.life))


class Goblin(Unit):
    # damage 속성 추가
    def __init__(self, rank, size, life, attack_type, damage):
        super(Goblin, self).__init__(rank, size, life)
        self.attack_type = attack_type
        self.damage = damage

    def show_status(self):
        super(Goblin, self).show_status()
        print('공격 타입: {}'.format(self.attack_type))
        # 오버라이드 메소드
        print ('데미지: {}'.format(self.damage))


    # 공격 메소드 추가
    def attack(self):
        print('[{}]이 공격합니다! 상대방 데미지({})'.format(self.name, self.damage))


class SphereGoblin(Goblin):
    def __init__(self, rank, size, life, attack_type, damage, sphere_type):
        super(SphereGoblin, self).__init__(rank, size, life, attack_type, damage)
        self.sphere_type = sphere_type

    def show_status(self):
        super(SphereGoblin, self).show_status()
        print('창 타입: {}'.format(self.sphere_type))


class Hero(Unit):
    def __init__(self, rank, size, life, goblins=None):
        super(Hero, self).__init__(rank, size, life)
        if goblins is None:
            self.goblins = []
        else:
            self.goblins = goblins

    def show_own_goblins(self):
        num_of_goblins = len([x for x in self.goblins if isinstance(x, Goblin)])
        num_of_sphere_goblins = len([x for x in self.goblins if isinstance(x, SphereGoblin)])
        print('현재 영웅이 소유한 고블린은 {}명, 창 고블린은 {}명입니다.'.format(num_of_goblins, num_of_sphere_goblins))

    def make_goblins_attack(self):
        for goblin in self.goblins:
            goblin.attack()


# 고블린 오브젝트 생성
goblin_1 = Goblin('병사', 'Small', 100, '근접 공격', 15)
goblin_2 = Goblin('병사', 'Small', 100, '근접 공격', 15)
sphere_goblin_1 = SphereGoblin('병사', 'Small', 100, '레인지 공격', 10, '긴 창')

# 영웅 오브젝트 생성 후, 고블린 오브젝트 할당       
hero_1 = Hero('영웅', 'Big', 300, [goblin_1, goblin_2, sphere_goblin_1])
hero_1.show_own_goblins()
hero_1.make_goblins_attack()
# 출력결과:
# $ python oop_5.py
# 현재 영웅이 소유한 고블린은 3명, 창 고블린은 1명입니다.
# [Goblin]이 공격합니다! 상대방 데미지(15)
# [Goblin]이 공격합니다! 상대방 데미지(15)
# [SphereGoblin]이 공격합니다! 상대방 데미지(10)
```
가장 상위 클래스인 Unit 클래스로 부터 상속을 받는 Hero 클래스를 만들고 __init__()를 오버라이딩했습니다. 그리고, 자신이 소유하고 있는 고블린의 수를 표시하는 메소드와 소유한 고블린이 공격을 하도록 하는 메소드도 만들어 봤습니다.

```python
# -*- coding: utf-8 -*-

class Unit(object):
    def __init__(self, rank, size, life):
        self.name = self.__class__.__name__
        self.rank = rank
        self.size = size
        self.life = life

    def show_status(self):
        print('이름: {}'.format(self.name))
        print('등급: {}'.format(self.rank))
        print('사이즈: {}'.format(self.size))
        print('라이프: {}'.format(self.life))


class Goblin(Unit):
    # damage 속성 추가
    def __init__(self, rank, size, life, attack_type, damage):
        super(Goblin, self).__init__(rank, size, life)
        self.attack_type = attack_type
        self.damage = damage

    def show_status(self):
        super(Goblin, self).show_status()
        print('공격 타입: {}'.format(self.attack_type))
        # 오버라이드 메소드
        print ('데미지: {}'.format(self.damage))


    # 공격 메소드 추가
    def attack(self):
        print('[{}]이 공격합니다! 상대방 데미지({})'.format(self.name, self.damage))


class SphereGoblin(Goblin):
    def __init__(self, rank, size, life, attack_type, damage, sphere_type):
        super(SphereGoblin, self).__init__(rank, size, life, attack_type, damage)
        self.sphere_type = sphere_type

    def show_status(self):
        super(SphereGoblin, self).show_status()
        print('창 타입: {}'.format(self.sphere_type))


class Hero(Unit):
    def __init__(self, rank, size, life, goblins=None):
        super(Hero, self).__init__(rank, size, life)
        if goblins is None:
            self.goblins = []
        else:
            self.goblins = goblins

    def show_own_goblins(self):
        num_of_goblins = len([x for x in self.goblins if isinstance(x, Goblin)])
        num_of_sphere_goblins = len([x for x in self.goblins if isinstance(x, SphereGoblin)])
        print('현재 영웅이 소유한 고블린은 {}명, 창 고블린은 {}명입니다.'.format(num_of_goblins, num_of_sphere_goblins))

    def make_goblins_attack(self):
        for goblin in self.goblins:
            goblin.attack()

    def add_goblins(self, new_goblins):
        for goblin in new_goblins:
            if goblin not in self.goblins:
                self.goblins.append(goblin)
            else:
                print('이미 추가된 고블린입니다.')


    def remove_goblins(self, old_goblins):
        for goblin in old_goblins:
            try:
                self.goblins.remove(goblin)
            except:
                print('소유하고 있지 않은 고블린입니다.')


# 고블린 오브젝트 생성
goblin_1 = Goblin('병사', 'Small', 100, '근접 공격', 15)
goblin_2 = Goblin('병사', 'Small', 100, '근접 공격', 15)
sphere_goblin_1 = SphereGoblin('병사', 'Small', 100, '레인지 공격', 10, '긴 창')

# 영웅 오브젝트 생성 후, 고블린 오브젝트 할당       
hero_1 = Hero('영웅', 'Big', 300, [goblin_1, goblin_2, sphere_goblin_1])

# 새로운 고블린 생성
goblin_3 = Goblin('병사', 'Small', 100, '근접 공격', 20)
sphere_goblin_2 = SphereGoblin('병사', 'Small', 100, '레인지 공격', 5, '긴 창')

print('# 새로운 고블린 추가 전')
hero_1.show_own_goblins()
hero_1.make_goblins_attack()

# 새로운 고블린 추가
hero_1.add_goblins([goblin_3, sphere_goblin_2])

print('\n# 새로운 고블린 추가 후')
hero_1.show_own_goblins()
hero_1.make_goblins_attack()

# 추가한 고블린 삭제
hero_1.remove_goblins([goblin_3, sphere_goblin_2])

print('\n# 추가한 고블린 삭제 후')
hero_1.show_own_goblins()
hero_1.make_goblins_attack()

# 영웅에게 소유되지 않은 고블린 생성
goblin_4 = Goblin('병사', 'Small', 100, '근접 공격', 20)

# 이미 소유한 고블린 추가
print('\n# 에러 메세지 발생')
hero_1.add_goblins([goblin_1])
hero_1.remove_goblins([goblin_4])
```
출력결과
``` shell
$ python oop_5.py
# 새로운 고블린 추가 전
현재 영웅이 소유한 고블린은 3명, 창 고블린은 1명입니다.
[Goblin]이 공격합니다! 상대방 데미지(15)
[Goblin]이 공격합니다! 상대방 데미지(15)
[SphereGoblin]이 공격합니다! 상대방 데미지(10)

# 새로운 고블린 추가 후
현재 영웅이 소유한 고블린은 5명, 창 고블린은 2명입니다.
[Goblin]이 공격합니다! 상대방 데미지(15)
[Goblin]이 공격합니다! 상대방 데미지(15)
[SphereGoblin]이 공격합니다! 상대방 데미지(10)
[Goblin]이 공격합니다! 상대방 데미지(20)
[SphereGoblin]이 공격합니다! 상대방 데미지(5)

# 추가한 고블린 삭제 후
현재 영웅이 소유한 고블린은 3명, 창 고블린은 1명입니다.
[Goblin]이 공격합니다! 상대방 데미지(15)
[Goblin]이 공격합니다! 상대방 데미지(15)
[SphereGoblin]이 공격합니다! 상대방 데미지(10)

# 에러 메세지 발생
이미 추가된 고블린입니다.
소유하고 있지 않은 고블린입니다.
```
----


참고 자료
http://pythonstudy.xyz/python
https://wikidocs.net/book/search/result/1
http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-4-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%A9%94%EC%86%8C%EB%93%9C%EC%99%80-%EC%8A%A4%ED%83%9C%ED%8B%B1-%EB%A9%94%EC%86%8C%EB%93%9C-class-method-and-static-method/
