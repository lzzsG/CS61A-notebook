---
layout: page
title: L28 Exception
permalink: /L28
description: "Lecture 28. Exception"
nav_order: 28



---

# Lecture 28. Exception

## Announcements

本周的实验和作业将需要使用 Scheme 编程语言。你可以选择使用 [code.cs61a.org](https://code.cs61a.org) 或者我们为每次 Scheme 作业（包括实验和作业）提供的 Scheme 解释器。这个解释器可以直接从终端运行，从而可以轻松加载并运行 Scheme 文件。

### 实验和作业的安排
- **Lab 10** 的截止日期延长到了周三，以避开选举日的冲突。
- **Homework 6** 将在周四截止，作业包含三个简单的问题，主要是帮助你开始使用 Scheme。

### 相关支持
- 今天会有作业讨论会，时间是晚上 7 点到 9 点，具体的 Zoom 链接请查看 Piazza。
- 周四一些助教会举行概念性辅导时间，预计是下午 1 点到 2 点，具体信息将在 Piazza 上更新。

### 期中考试与投票
- 请查看你们的期中考试成绩，如果有需要重新评分的部分，请在周一之前提交申请。
- 如果你身处美国，请不要忘记去投票。

## 今日课程：Python 的异常处理
今天的课程将重新回到 Python，讨论一个非常重要的主题——**异常处理**。在编写和解释不同编程语言的过程中，了解如何处理程序中的错误至关重要。

### 异常处理的重要性
计算机程序在执行过程中可能会遇到各种各样的错误，例如：
- 函数收到不正确类型的参数。
- 文件资源可能不在预期的位置。
- 网络连接可能中断。

这些都是程序可能会面临的问题。历史上最著名的计算机错误之一出现在 1947 年 Grace Hopper 的工作中，当时她在 Mark II 计算机的继电器中发现了一只飞蛾，导致计算机关闭。这被认为是第一个真正的计算机“bug”案例。

无论是硬件问题还是软件问题，程序需要能够应对这些非标准的情况。不同类型的程序对错误的处理方式不同：
- 对于全球用户的网络服务，程序应尽可能继续运行，确保部分功能即使在故障情况下也能工作。
- 对于 Python 解释器这样的开发工具，当遇到错误时，程序会立即停止，并向开发者提供详细的错误信息，以便调试。

### Python 中的异常机制
Python 的异常机制用于声明错误，并提供处理错误的方式。异常是一种特殊的对象，异常处理允许程序在错误发生时不中止执行，而是根据错误的类型采取适当的处理措施。通常情况下，未经处理的异常会导致程序停止，并输出包含错误堆栈追踪的长错误信息，这样可以帮助程序员找出错误的来源。

从今天开始，你将学习如何处理异常，以便程序可以在遇到错误时继续运行，而不是完全停止。

### 处理异常的关键点
1. **异常是对象**：你已经了解了对象系统，因此异常也有自己的类和构造函数。
2. **异常的作用**：异常允许非本地控制转移。通常，函数的执行顺序是自下而上的返回，但是异常处理可以改变这一规则。
   

## 异常处理机制的两部分：**引发异常** 和 **处理异常**
异常处理有两部分：**引发异常**（raising exceptions）和 **处理异常**（handling exceptions）。首先，我们来讨论如何引发异常。

### 1. 引发异常
最简单的引发异常的方式是使用 `assert` 语句。`assert` 语句用于在程序中进行检查，如果某个条件不成立（即表达式为 `False`），则引发一个 `AssertionError` 异常。例如：
```python
assert 2 + 2 == 5, "Math doesn't work like that!"
```
如果表达式 `2 + 2 == 5` 为 `False`，Python 会引发一个 `AssertionError`，并输出附带的错误信息 `"Math doesn't work like that!"`。

### 关闭 `assert`
`assert` 语句可以在生产环境中关闭以提高效率。通过使用 `-O`（优化）选项运行 Python，所有的 `assert` 语句都会被忽略：
```bash
python3 -O script.py
```

### 2. 使用 `raise` 语句引发异常
除了 `assert`，还可以使用 `raise` 语句手动引发任意类型的异常。`raise` 语句接受一个异常实例或异常类作为参数。例如：
```python
raise TypeError("This is a bad argument.")
```
这会引发一个 `TypeError`，并输出消息 `"This is a bad argument."`。

### 常见的异常类型
- **`TypeError`**：表示函数接收到的参数类型不正确。
- **`NameError`**：表示在当前环境中找不到某个名称。
- **`KeyError`**：表示在字典中找不到指定的键。
- **`RuntimeError`**：表示程序在运行过程中遇到了一般的错误。

例如：
```python
raise KeyError("Key not found in dictionary")
```

### 堆栈追踪（Stack Trace）
当引发异常时，Python 会生成一个堆栈追踪，用于显示错误发生的上下文。例如：
```python
raise TypeError("Bad argument")
```
输出结果会显示引发异常的文件、行号、异常类型和错误信息，帮助开发者定位问题。

## 处理异常：**`try-except` 语句 ** Try Statements

![QQ_1726717774213]({{ site.baseurl }}/docs/assets/QQ_1726717774213.png)

`try-except` 语句用于捕获并处理在 `try` 代码块中引发的异常。它的基本结构如下：

```python
try:
    # 尝试执行的代码
    ...
except SomeException as e:
    # 处理异常的代码
    ...
```
- **`try` 块**：执行可能引发异常的代码。
- **`except` 块**：捕获并处理特定的异常。

### 示例
让我们来看一个实际的示例，处理除零错误：
```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Caught an exception:", e)
```
在这个示例中，`10 / 0` 引发了 `ZeroDivisionError`，程序捕获并输出了该异常，而不是终止运行。

### 多个 `try-except`

你可以在程序中定义多个 `try-except` 块，并且这些块可以嵌套。如果有嵌套的 `try-except` 语句，异常会被最内层的 `try` 块捕获。例如：

```python
try:
    try:
        x = 1 / 0
    except ZeroDivisionError as e:
        print("Inner except caught:", e)
except:
    print("Outer except caught the exception.")
```

这里，`ZeroDivisionError` 会被内部的 `except` 块捕获。

### 捕获多个异常
我们还可以捕获多个异常，处理不同类型的错误：
```python
try:
    some_code()
except (TypeError, ValueError) as e:
    print("Caught a type or value error:", e)
except KeyError as e:
    print("Caught a key error:", e)
```

需要注意的是，异常处理是相对较慢的操作，因此不应该在程序的常规流程中频繁使用。异常处理通常用于处理意外情况，而不是作为程序的主要控制流。

### 处理除零错误的函数示例
让我们重新定义一个函数 `invert(x)` 来计算 `1/x`和一个安全版本 `invert_safe(x)`，用于处理除零错误：
```python
def invert(x):
    return 1 / x

def invert_safe(x):
    try:
        return invert(x)
    except ZeroDivisionError as e:
        print(f"Handling ZeroDivisionError: {e}")
        return 0
```
如果我们调用 `invert_safe(2)`，将会返回 `0.5`。但是，如果我们调用 `invert_safe(0)`，它会捕获 `ZeroDivisionError`，打印错误信息，并返回 `0`：
```python
print(invert_safe(2))  # 输出 0.5
print(invert_safe(0))  # 输出 "Handling ZeroDivisionError: division by zero" 和 0
```

### 处理递归中的异常

异常处理还可以应用于递归函数中。例如，处理递归调用深度超出的情况：

```python
def recursive_function():
    return recursive_function()

try:
    recursive_function()
except RecursionError as e:
    print("Caught recursion error:", e)
```

当递归深度超出 Python 的限制时，Python 会引发 `RecursionError`，该异常可以通过 `try-except` 进行捕获和处理。

## 异常的传播与嵌套 `try-except`

当在函数调用链中某个地方抛出异常时，如果该异常被内部的 `try-except` 块处理，那么该异常不会再向外层传播。让我们来理解以下场景：

```python
def invert(x):
    return 1 / x

def invert_safe(x):
    try:
        return invert(x)
    except ZeroDivisionError as e:
        print("Handled ZeroDivisionError:", e)
        return 0
```

调用 `invert_safe(0)` 时，`invert(0)` 会引发 `ZeroDivisionError`，这个异常会被 `invert_safe` 函数内部的 `try-except` 捕获和处理，输出 "Handled ZeroDivisionError: division by zero" 并返回 `0`。因此，异常不会传播到外层的 `try-except` 块。

### 处理外层异常
如果我们在外层包裹另一个 `try-except` 块：
```python
try:
    invert_safe(0)
except ZeroDivisionError:
    print("Handled in outer block")
```
由于 `ZeroDivisionError` 已经在 `invert_safe` 中被处理，因此外层的 `except` 语句不会执行。

### 错误类型与操作符的优先级
在 Python 中，表达式的操作符在函数调用之前计算。如果表达式在操作符计算时引发错误，那么函数调用甚至不会发生。例如：
```python
invert_safe(1 / 0)
```
在这个例子中，`1 / 0` 会在 `invert_safe` 被调用之前引发 `ZeroDivisionError`。由于函数还没有机会被调用，异常也不会被 `invert_safe` 内部的 `try-except` 捕获。

## 高阶函数中的异常处理：`reduce` 的例子

![QQ_1726717552144]({{ site.baseurl }}/docs/assets/QQ_1726717552144.png)

`reduce` 是一个高阶函数，它接收一个二元函数、一个序列和一个初始值，并将序列中的元素与初始值组合，逐步减少为一个单一的值。例如：
```python
from functools import reduce
import operator

# 使用 reduce 计算乘积
result = reduce(operator.mul, [2, 4, 8], 1)
print(result)  # 输出 64
```
在这个例子中，`reduce` 将初始值 `1` 和序列 `[2, 4, 8]` 中的元素按顺序相乘，结果为 `64`。

### 使用 `reduce` 实现除法

假设我们要编写一个函数 `divide_all`，将一个分子除以一系列分母：
```python
def divide_all(numerator, denominators):
    return reduce(operator.truediv, denominators, numerator)

result = divide_all(1024, [2, 4, 8])
print(result)  # 输出 16.0
```
这里，`reduce` 将 `1024` 依次除以 `2`、`4` 和 `8`，最后的结果为 `16.0`。

### 在 `reduce` 中处理除零错误

如果分母序列中包含 `0`，会引发 `ZeroDivisionError`。为了处理这个错误，我们可以使用异常处理机制，并在遇到除零错误时返回 `inf`（无穷大）：
```python
def divide_all_safe(numerator, denominators):
    try:
        return reduce(operator.truediv, denominators, numerator)
    except ZeroDivisionError:
        return float('inf')

result = divide_all_safe(1024, [2, 0, 8])
print(result)  # 输出 inf
```
在这个例子中，`reduce` 中的某次除法遇到了 `ZeroDivisionError`，异常被捕获，函数返回 `inf`。

### 例子中的分工

通过使用高阶函数和异常处理，我们可以分离关注点：
- `reduce` 专注于递归地组合序列的元素，**并不需要知道具体操作是除法**，也不关心除法的异常。
- `divide_all_safe` 专注于处理除法及可能的异常。通过在其内部调用 `reduce`，它能处理序列中的元素，并捕获可能发生的 `ZeroDivisionError`。

这种方式有效地分离了不同功能模块的责任，使代码更加简洁、灵活。





