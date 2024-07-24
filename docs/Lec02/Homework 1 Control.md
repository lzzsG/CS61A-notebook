---
layout: page
title: Homework 1 Control
permalink: /HW01/
nav_order: 0
parent: Lecture 2. Functions



---

# Homework 1: Control

## 作业说明

下载 hw01.zip

参考阅读教材 1.1-1.5

### 必做题目

### Q1: A Plus Abs B

Python 的 `operator` 模块定义了*二元函数*用于 Python 的内置算术运算符。例如，调用 `operator.add(2,3)` 等同于调用表达式 `2 + 3`；两者都会返回 `5`。

> 注意，当 `operator` 模块被导入命名空间时，例如在 `hw01.py` 文件顶部，你可以直接调用 `add(2,3)` 而不是 `operator.add(2,3)`。

填补以下函数中的空白部分，以便在不调用 `abs` 的情况下将 `a` 加到 `b` 的绝对值上。你**不能**修改提供的代码，除了两个空白部分。

```python
def a_plus_abs_b(a, b):
    """Return a+abs(b), but without calling abs.

    >>> a_plus_abs_b(2, 3)
    5
    >>> a_plus_abs_b(2, -3)
    5
    >>> a_plus_abs_b(-1, 4)
    3
    >>> a_plus_abs_b(-1, -4)
    3
    """
    if b < 0:
        f = _____
    else:
        f = _____
    return f(a, b)
```

使用 Ok 测试你的代码：

```bash
python3 ok -q a_plus_abs_b
```

### Q2: Two of Three

编写一个函数，该函数接受三个*正数*作为参数，并返回其中两个最小数的平方和。**函数体仅使用一行代码。**

```python
def two_of_three(i, j, k):
    """Return m*m + n*n, where m and n are the two smallest members of the
    positive numbers i, j, and k.

    >>> two_of_three(1, 2, 3)
    5
    >>> two_of_three(5, 3, 1)
    10
    >>> two_of_three(10, 2, 8)
    68
    >>> two_of_three(5, 5, 5)
    50
    """
    return _____
```

> **提示:** 考虑使用 `max` 或 `min` 函数：

> ```python
> >>> max(1, 2, 3)
> 3
> >>> min(-1, -2, -3)
> -3
> ```

使用 Ok 测试你的代码：

```bash
python3 ok -q two_of_three
```

### Q3: 最大因子

编写一个函数，该函数接受一个大于1的整数 `n`，并返回小于 `n` 且能整除 `n` 的最大整数。

```python
def largest_factor(n):
    """Return the largest factor of n that is smaller than n.

    >>> largest_factor(15) # factors are 1, 3, 5
    5
    >>> largest_factor(80) # factors are 1, 2, 4, 5, 8, 10, 16, 20, 40
    40
    >>> largest_factor(13) # factor is 1 since 13 is prime
    1
    """
    "*** YOUR CODE HERE ***"
```

> **提示:** 要检查 `b` 是否能整除 `a`，可以使用表达式 `a % b == 0`，可以读作 “`a` 除以 `b` 的余数是0”。

使用 Ok 测试你的代码：

```bash
python3 ok -q largest_factor
```

### Q4: 冰雹序列

Douglas Hofstadter 的普利策奖获奖书籍《Gödel, Escher, Bach》提出了以下数学谜题。

1. 选择一个正整数 `n` 作为起点。
2. 如果 `n` 是偶数，将其除以2。
3. 如果 `n` 是奇数，将其乘以3并加1。
4. 继续这个过程，直到 `n` 变为1。

数字 `n` 会上下波动，但最终会到达1（至少对所有尝试过的数字都是如此——没有人曾证明这个序列会终止）。类似地，冰雹在大气中上下波动，然后最终落到地面。

这个 `n` 值的序列通常被称为冰雹序列。编写一个函数，该函数接受一个名为 `n` 的单一参数，打印出以 `n` 开始的冰雹序列，并返回序列中的步数：

```python
def hailstone(n):
    """Print the hailstone sequence starting at n and return its
    length.

    >>> a = hailstone(10)
    10
    5
    16
    8
    4
    2
    1
    >>> a
    7
    >>> b = hailstone(1)
    1
    >>> b
    1
    """
    "*** YOUR CODE HERE ***"
```

冰雹序列可以非常长！试试27。你能找到最长的吗？

> 注意，如果 `n == 1` 初始，那么序列的长度是一步。
> **提示:** 回忆一下使用常规除法 `/` 和地板除法 `//` 的不同输出。

使用 Ok 测试你的代码：

```bash
python3 ok -q hailstone
```
