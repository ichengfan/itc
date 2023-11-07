# CS1602: Introduction to Computation
程帆

信息与计算实验室 (Information and Computing Lab)

上海交通大学计算机系

chengfan85@gmail.com

---

CS1602《计算导论》课程主要面向零起点的大学一年级新生，无专业背景要求。

从计算文化、计算语言、计算工具、以及问题求解四个方面培养本科生对计算科学与工具的使用能力。致力于改善目前本科生由于区域背景、教育环境差异巨大，计算能力参差不齐的局面。熟练掌握现代专业的计算工具的使用。为未来计算机及其它学科的学习，补齐短板。

全部16周，每周4学时，包括实验练习。以Python（3.11）语言为核心工具。

从2017年开始，每年秋季大一上学期授课。课程内容经过不断迭代更新，历年学生投票评教优秀。具备开放条件，准备逐步开放。

## 课程大纲 

1. Introduction

2. Fundamental (I)

3. Fundamental (II)

4. Condition, Loop and Function

5. List

6. Tuple, Dict, String and Set

7. Recursion

8. Problems

9. Class and Module (I)

10. Class and Module (II)

11. Complexity and Exception

12. Random and File

13. Pythonic

14. FP and LEGB

15. Multitaksing and RE

16. Review

    (由于国庆假期，可能会减少一个学时)

## 工具类

1. Visual Studio Code
2. Jupyter
3. Pip
4. Ubuntu环境以及59个Linux常用命令

## 课程视频

1. 交大内部可以OC看课堂录像
2. Bilibili: fcieee

## 测试部分

def hanoi_plus(n: int, x: str, y: str, z: str):
    if n == 1:
        print(f"{x}->{y}")
        print(f"{y}->{z}")
        return
    hanoi_plus(n - 1, x, y, z)
    print(f"{x}->{y}")
    hanoi_plus(n - 1, z, y, x)
    print(f"{y}->{z}")
    hanoi_plus(n - 1, x, y, z)


hanoi_plus(int(input("n")), input("x"), input("y"), input("z"))


def circle1(n: int):
    lst = [i for i in range(1, n + 1)]
    k = 1
    index = 0
    while len(lst) > 1:
        if k % 2 == 0:
            lst.pop(index)
        else:
            index += 1
        if index >= len(lst):
            index = 0
        k += 1
    return lst[0]


print(circle1(int(input("n"))))


def circle2(n: int):
    if n == 1:
        return 1
    if n % 2 == 0:
        return 2 * circle2(n // 2) - 1
    else:
        return 2 * circle2(n // 2) + 1


print(circle2(int(input("n"))))


def circle3(n: int):
    m = 0
    while not (2**m <= n and 2 ** (m + 1) > n):
        m += 1
    return 2 * (n - 2**m) + 1


print(circle3(int(input("n"))))


import pprint


def GridCover(k: int, i: int, j: int) -> list[list[int]]:
    d = {
        (1, 1): [[0, 4], [4, 4]],
        (1, 2): [[3, 0], [3, 3]],
        (2, 1): [[2, 2], [0, 2]],
        (2, 2): [[1, 1], [1, 0]],
    }
    if k == 1:
        return d[(i, j)]
    a, b = 0, 0
    if i > 2 ** (k - 1):
        i -= 2 ** (k - 1)
        a = 1
    if j > 2 ** (k - 1):
        j -= 2 ** (k - 1)
        b = 1
    judge = {(0, 0): 1, (0, 1): 2, (1, 0): 3, (1, 1): 4}
    spl = [[] for _ in range(4)]
    spl[judge[(a, b)] - 1] = GridCover(k - 1, i, j)
    if spl[0] == []:
        spl[0] = GridCover(k - 1, 2 ** (k - 1), 2 ** (k - 1))
        spl[0][2 ** (k - 1) - 1][2 ** (k - 1) - 1] = 5 - judge[(a, b)]
    if spl[1] == []:
        spl[1] = GridCover(k - 1, 2 ** (k - 1), 1)
        spl[1][2 ** (k - 1) - 1][0] = 5 - judge[(a, b)]
    if spl[2] == []:
        spl[2] = GridCover(k - 1, 1, 2 ** (k - 1))
        spl[2][0][2 ** (k - 1) - 1] = 5 - judge[(a, b)]
    if spl[3] == []:
        spl[3] = GridCover(k - 1, 1, 1)
        spl[3][0][0] = 5 - judge[(a, b)]
    return [spl[0][p] + spl[1][p] for p in range(2 ** (k - 1))] + [
        spl[2][p] + spl[3][p] for p in range(2 ** (k - 1))
    ]


pprint.pprint(GridCover(int(input("k")), int(input("i")), int(input("j"))))
