---
layout: page
title: Homework 1 Control
permalink: /HW01/
nav_order: 0
parent: Lecture 2. Functions



---

# Homework 1: Control

## Instructions指示

Download [hw01.zip](https://inst.eecs.berkeley.edu/~cs61a/sp20/hw/hw01/hw01.zip).下载 hw01.zip。

**Submission:** When you are done, submit with `python3 ok --submit`. You may submit more than once before the deadline; only the final submission will be scored. Check that you have successfully submitted your code on [okpy.org](https://okpy.org/). See [Lab 0](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00#submitting-the-assignment) for more instructions on submitting assignments.提交：完成后，使用 python3 ok --submit 提交。您可以在截止日期前多次提交；仅对最终提交的作品进行评分。检查您是否已在 okpy.org 上成功提交代码。有关提交作业的更多说明，请参阅实验 0。

**Using Ok:** If you have any questions about using Ok, please refer to [this guide.](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/using-ok.html)使用 Ok：如果您对使用 Ok 有任何疑问，请参阅本指南。

**Readings:** You might find the following references useful:阅读材料：您可能会发现以下参考资料很有用：

- [Section 1.2第 1.2 节](http://composingprograms.com/pages/12-elements-of-programming.html)
- [Section 1.3第 1.3 节](http://composingprograms.com/pages/13-defining-new-functions.html)
- [Section 1.4第 1.4 节](http://composingprograms.com/pages/14-designing-functions.html)
- [Section 1.5第 1.5 节](http://composingprograms.com/pages/15-control.html)

Note: Some of these readings necessary for the homework questions will not be covered until Monday's lecture on Control.注意：作业问题所需的一些阅读材料要到周一的控制讲座才会涵盖。

**Grading:** Homework is graded based on correctness. Each incorrect problem will decrease the total score by one point. There is a homework recovery policy as stated in the syllabus. **This homework is out of 2 points.**评分：家庭作业根据正确性进行评分。每做错一道题，总分就会减少一分。教学大纲中规定了家庭作业恢复政策。本作业满分2分。

# Required Questions必答问题

### Q1: Syllabus QuizQ1：教学大纲测验

Please fill out our [Syllabus Quiz](https://docs.google.com/forms/d/1GnM3CXAaT63Pu85vg0b3vlJKQobcbo8Idr1exFNMxwg) based off of our policies found on our [syllabus page](https://cs61a.org/articles/about.html).

请根据我们的教学大纲页面上的政策填写我们的教学大纲测验。

### Q2: A Plus Abs B

Fill in the blanks in the following function for adding `a` to the absolute value of `b`, without calling `abs`. You may **not** modify any of the provided code other than the two blanks.填写以下函数中的空白，将 a 与 b 的绝对值相加，而不调用 abs。除了两个空白之外，您不得修改任何提供的代码。

```python
from operator import add, sub

def a_plus_abs_b(a, b):
    """Return a+abs(b), but without calling abs.

    >>> a_plus_abs_b(2, 3)
    5
    >>> a_plus_abs_b(2, -3)
    5
    >>> # a check that you didn't change the return statement!
    >>> import inspect, re
    >>> re.findall(r'^\s*(return .*)', inspect.getsource(a_plus_abs_b), re.M)
    ['return h(a, b)']
    """
    if b >= 0:
        h = _____
    else:
        h = _____
    return h(a, b)
```

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q a_plus_abs_b
```

### Q3: Two of Three Q3：三中之二

Write a function that takes three *positive* numbers and returns the sum of the squares of the two smallest numbers. **Use only a single line for the body of the function.**编写一个函数，接受三个正数并返回两个最小数的平方和。函数体仅使用一行。

```python
def two_of_three(x, y, z):
    """Return a*a + b*b, where a and b are the two smallest members of the
    positive numbers x, y, and z.

    >>> two_of_three(1, 2, 3)
    5
    >>> two_of_three(5, 3, 1)
    10
    >>> two_of_three(10, 2, 8)
    68
    >>> two_of_three(5, 5, 5)
    50
    >>> # check that your code consists of nothing but an expression (this docstring)
    >>> # a return statement
    >>> import inspect, ast
    >>> [type(x).__name__ for x in ast.parse(inspect.getsource(two_of_three)).body[0].body]
    ['Expr', 'Return']
    """
    return _____
```

> **Hint:** Consider using the `max` or `min` function:提示：考虑使用 max 或 min 函数：
>
> ```python
> >>> max(1, 2, 3)
> 3
> >>> min(-1, -2, -3)
> -3
> ```

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q two_of_three
```

### Q4: Largest FactorQ4：最大因素

Write a function that takes an integer `x` that is **greater than 1** and returns the largest integer that is smaller than `x` and evenly divides `x`.编写一个函数，接受大于 1 的整数 x，并返回小于 x 且能整除 x 的最大整数。

```python
def largest_factor(x):
    """Return the largest factor of x that is smaller than x.

    >>> largest_factor(15) # factors are 1, 3, 5
    5
    >>> largest_factor(80) # factors are 1, 2, 4, 5, 8, 10, 16, 20, 40
    40
    >>> largest_factor(13) # factor is 1 since 13 is prime
    1
    """
    "*** YOUR CODE HERE ***"
```

> **Hint:** To check if `b` evenly divides `a`, you can use the expression `a % b == 0`, which can be read as, "the remainder of dividing `a` by `b` is 0."提示：要检查 b 是否整除 a，可以使用表达式 a % b == 0，可以理解为“a 除以 b 的余数为 0”。

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q largest_factor
```

### Q5: If Function vs StatementQ5：If 函数与语句

Let's try to write a function that does the same thing as an `if` statement.让我们尝试编写一个与 if 语句执行相同操作的函数。

```python
def if_function(condition, true_result, false_result):
    """Return true_result if condition is a true value, and
    false_result otherwise.

    >>> if_function(True, 2, 3)
    2
    >>> if_function(False, 2, 3)
    3
    >>> if_function(3==2, 3+2, 3-2)
    1
    >>> if_function(3>2, 3+2, 3-2)
    5
    """
    if condition:
        return true_result
    else:
        return false_result
```

Despite the doctests above, this function actually does *not* do the same thing as an `if` statement in all cases. To prove this fact, write functions `c`, `t`, and `f` such that `with_if_statement` prints the number `6`, but `with_if_function` prints both `5` and `6`.尽管有上面的文档测试，但该函数实际上并不在所有情况下都执行与 if 语句相同的操作。为了证明这一事实，编写函数 c、t 和 f，使 with_if_statement 打印数字 6，但 with_if_function 同时打印 5 和 6。

```python
def with_if_statement():
    """
    >>> result = with_if_statement()
    6
    >>> print(result)
    None
    """
    if c():
        return t()
    else:
        return f()

def with_if_function():
    """
    >>> result = with_if_function()
    5
    6
    >>> print(result)
    None
    """
    return if_function(c(), t(), f())

def c():
    "*** YOUR CODE HERE ***"

def t():
    "*** YOUR CODE HERE ***"

def f():
    "*** YOUR CODE HERE ***"
```

> **Hint**: If you are having a hard time identifying how an `if` statement and `if_function` differ, consider the [rules of evaluation for `if` statements](http://composingprograms.com/pages/15-control.html#conditional-statements) and [call expressions](http://composingprograms.com/pages/12-elements-of-programming.html#call-expressions).提示：如果您很难确定 if 语句和 if_function 有何不同，请考虑 if 语句和调用表达式的求值规则。

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q with_if_statement
python3 ok -q with_if_function
```

### Q6: HailstoneQ6：冰雹

Douglas Hofstadter's Pulitzer-prize-winning book, *Gödel, Escher, Bach*, poses the following mathematical puzzle.道格拉斯·霍夫施塔特 (Douglas Hofstadter) 的普利策奖获奖著作《哥德尔、埃舍尔、巴赫》提出了以下数学难题。

1. Pick a positive integer `x` as the start.选择一个正整数 x 作为开始。
2. If `x` is even, divide it by 2.如果 x 是偶数，则将其除以 2。
3. If `x` is odd, multiply it by 3 and add 1.如果 x 是奇数，则将其乘以 3 加 1。
4. Continue this process until `x` is 1.继续这个过程直到 x 为 1。

The number `x` will travel up and down but eventually end at 1 (at least for all numbers that have ever been tried -- nobody has ever proved that the sequence will terminate). Analogously, a hailstone travels up and down in the atmosphere before eventually landing on earth.数字 x 将上下移动，但最终以 1 结束（至少对于所有尝试过的数字来说——没有人证明该序列会终止）。类似地，冰雹在大气层中上下移动，最终降落在地球上。

> **Breaking News** (or at least the closest thing to that in math). There has been a [recent development](https://www.quantamagazine.org/mathematician-terence-tao-and-the-collatz-conjecture-20191211/) in the hailstone conjecture that shows that almost all numbers will eventually get to 1 if you repeat this process. This isn't a complete proof but a major breakthrough突发新闻（或者至少是数学中最接近的新闻）。冰雹猜想的最新发展表明，如果重复这个过程，几乎所有数字最终都会变成 1。这不是一个完整的证明，而是一个重大突破

This sequence of values of `x` is often called a Hailstone sequence. Write a function that takes a single argument with formal parameter name `x`, prints out the hailstone sequence starting at `x`, and returns the number of steps in the sequence:x 值的这个序列通常称为 Hailstone 序列。编写一个函数，该函数采用形式参数名称为 x 的单个参数，打印出从 x 开始的冰雹序列，并返回序列中的步数：

```python
def hailstone(x):
    """Print the hailstone sequence starting at x and return its
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
    """
    "*** YOUR CODE HERE ***"
```

Hailstone sequences can get quite long! Try 27. What's the longest you can find?冰雹序列可能会变得很长！尝试 27。你能找到最长的长度是多少？

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q hailstone
```

## Submit提交

Make sure to submit this assignment by running:确保通过运行以下命令提交此作业：

```bash
python3 ok --submit
```
