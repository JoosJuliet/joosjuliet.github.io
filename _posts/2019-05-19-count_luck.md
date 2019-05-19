---
layout: post
section-type: post
title: "[hacker_rank] Count Luck with python3"
categories: Algorithm
tags: [ 'algorithm', 'hacker_rank', 'python' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
잘못된 부분이 있으면 덧글을 통해서 소통을 하면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
그렇지만 소통을 할 때 서로의 감정을 존중하는 선에서 해주셨으면 좋겠습니다.
감사합니다:)
---

문제 : https://www.hackerrank.com/challenges/count-luck/problem

일단 is_splited_way은 오로지 갈림길인지 확인하고 X를 준다.
그리고 어차피 M의 위치를 아니까 그걸 가지고 한다.
가는길에 갈림길인 곳만 1로 되고 그것이 바로... !
1의 개수가 바로 답이다.


``` python

result = 0

def check_out_of_bound(r, c, forest):
    # 바운드 나갔나 확인
    for i in forest:
        print(i)
    print('--------')
    return 0 > r or r >= len(forest) or 0 > c or c >= len(forest[0]) or forest[r][c] == 'X' or forest[r][c] == '1'

# 앞으로 나아가는 길이 갈림길이면 True를 반환
def is_splited_way(r, c, forest, ds):
    cnt = 0
    for d in ds:
        # 근처에 있는 길이 지나갈 수 있는 길인가 확인
        dr = r + d[0]
        dc = c + d[1]
        if (not check_out_of_bound(dr, dc, forest)) and (forest[dr][dc] == '.' or forest[dr][dc] == '*'):
        # bound 나가지 않는 애이면서, .과 * 중에 하나인데 cnt가 2보다 크다는 것은 이게 갈림길인 지 확인이 된다.
            cnt += 1
            if cnt >= 2:
                return True
    return False


def find_portkey(r, c, forest):
    global result
    if check_out_of_bound(r, c, forest):
        return False

    if forest[r][c] == '*':
        return True

    ds = [[1, 0], [-1, 0], [0, -1], [0, 1]]

    if is_splited_way(r, c, forest, ds):
        # 지금 위치가 갈림길인가?
        forest[r][c] = '1'
        # 응
    else:
        forest[r][c] = 'X'
        # 아니

    for d in ds:
        dr = r+d[0]
        dc = c+d[1]

        if find_portkey(dr, dc, forest):
            if forest[r][c] == '1':
                result += 1
            return True

    return False


def start():
    global result
    for _ in range(int(input())):
        result = 0
        n, m = map(int, input().split())
        forest = []

        sr, sc = 0, 0
        for r in range(n):
            forest.append(list(input()))
            try:
                c = forest[-1].index('M')
                sr, sc = r, c
            except:
                pass
        # sr, sc의 위치를 안다.
        find_portkey(sr, sc, forest)

        k = int(input())
        print("Impressed" if result == k else "Oops!")

start()

```
