# Lecture 28. Exception

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

### 今日课程：Python 的异常处理
今天的课程将重新回到 Python，讨论一个非常重要的主题——**异常处理**。在编写和解释不同编程语言的过程中，了解如何处理程序中的错误至关重要。

#### 异常处理的重要性
计算机程序在执行过程中可能会遇到各种各样的错误，例如：
- 函数收到不正确类型的参数。
- 文件资源可能不在预期的位置。
- 网络连接可能中断。

这些都是程序可能会面临的问题。历史上最著名的计算机错误之一出现在 1947 年 Grace Hopper 的工作中，当时她在 Mark II 计算机的继电器中发现了一只飞蛾，导致计算机关闭。这被认为是第一个真正的计算机“bug”案例。

无论是硬件问题还是软件问题，程序需要能够应对这些非标准的情况。不同类型的程序对错误的处理方式不同：
- 对于全球用户的网络服务，程序应尽可能继续运行，确保部分功能即使在故障情况下也能工作。
- 对于 Python 解释器这样的开发工具，当遇到错误时，程序会立即停止，并向开发者提供详细的错误信息，以便调试。

#### Python 中的异常机制
Python 的异常机制用于声明错误，并提供处理错误的方式。异常是一种特殊的对象，异常处理允许程序在错误发生时不中止执行，而是根据错误的类型采取适当的处理措施。通常情况下，未经处理的异常会导致程序停止，并输出包含错误堆栈追踪的长错误信息，这样可以帮助程序员找出错误的来源。

从今天开始，你将学习如何处理异常，以便程序可以在遇到错误时继续运行，而不是完全停止。

#### 处理异常的关键点
1. **异常是对象**：你已经了解了对象系统，因此异常也有自己的类和构造函数。
2. **异常的作用**：异常允许非本地控制转移。通常，函数的执行顺序是自下而上的返回，但是异常处理可以改变这一规则。
   

通过学习异常处理，你将能够编写更加健壮的程序，使它们在面对非标准情况时能够更好地恢复并继续执行。



在 Python 中，异常处理机制允许程序在发生错误时不终止运行，而是根据特定的异常情况进行处理。这种机制在编写健壮的代码时非常重要，尤其是在可能遇到非标准行为的复杂程序中。

### 异常处理机制的两部分：**引发异常** 和 **处理异常**
异常处理有两部分：**引发异常**（raising exceptions）和 **处理异常**（handling exceptions）。首先，我们来讨论如何引发异常。

#### 1. 引发异常
最简单的引发异常的方式是使用 `assert` 语句。`assert` 语句用于在程序中进行检查，如果某个条件不成立（即表达式为 `False`），则引发一个 `AssertionError` 异常。例如：
```python
assert 2 + 2 == 5, "Math doesn't work like that!"
```
如果表达式 `2 + 2 == 5` 为 `False`，Python 会引发一个 `AssertionError`，并输出附带的错误信息 `"Math doesn't work like that!"`。

##### 关闭 `assert`
`assert` 语句可以在生产环境中关闭以提高效率。通过使用 `-O`（优化）选项运行 Python，所有的 `assert` 语句都会被忽略：
```bash
python3 -O script.py
```

#### 2. 使用 `raise` 语句引发异常
除了 `assert`，还可以使用 `raise` 语句手动引发任意类型的异常。`raise` 语句接受一个异常实例或异常类作为参数。例如：
```python
raise TypeError("This is a bad argument.")
```
这会引发一个 `TypeError`，并输出消息 `"This is a bad argument."`。

##### 常见的异常类型
- **`TypeError`**：表示函数接收到的参数类型不正确。
- **`NameError`**：表示在当前环境中找不到某个名称。
- **`KeyError`**：表示在字典中找不到指定的键。
- **`RuntimeError`**：表示程序在运行过程中遇到了一般的错误。

例如：
```python
raise KeyError("Key not found in dictionary")
```

##### 堆栈追踪（Stack Trace）
当引发异常时，Python 会生成一个堆栈追踪，用于显示错误发生的上下文。例如：
```python
raise TypeError("Bad argument")
```
输出结果会显示引发异常的文件、行号、异常类型和错误信息，帮助开发者定位问题。

### 处理异常：**`try-except` 语句**
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

#### 示例
让我们来看一个实际的示例，处理除零错误：
```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Caught an exception:", e)
```
在这个示例中，`10 / 0` 引发了 `ZeroDivisionError`，程序捕获并输出了该异常，而不是终止运行。

#### 捕获多个异常
我们还可以捕获多个异常，处理不同类型的错误：
```python
try:
    some_code()
except (TypeError, ValueError) as e:
    print("Caught a type or value error:", e)
except KeyError as e:
    print("Caught a key error:", e)
```

### 异常处理的性能考虑
需要注意的是，异常处理是相对较慢的操作，因此不应该在程序的常规流程中频繁使用。异常处理通常用于处理意外情况，而不是作为程序的主要控制流。

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

### 总结
- **引发异常**：通过 `assert` 或 `raise` 语句引发异常，适用于不同的错误类型。
- **处理异常**：使用 `try-except` 语句捕获并处理异常，避免程序因错误而崩溃。
- **堆栈追踪**：当异常引发时，Python 会生成详细的错误信息，帮助开发者定位问题。
- **性能考虑**：异常处理比较慢，因此应该仅在必要时使用。

掌握异常处理机制能够让你的程序更加健壮、容错性更强，适用于处理各种非标准情况。



在 Python 中，`try-except` 语句用于捕获和处理在代码执行过程中可能发生的异常。这个机制让我们能够优雅地处理错误，而不至于让程序崩溃。

### `try-except` 语句的执行规则
1. **`try` 块**：在 `try` 块中放置你想执行的代码。Python 会尝试执行这些语句，如果一切正常（即没有异常），则 `try` 块成功执行，不进入 `except` 块。
2. **`except` 块**：如果在执行 `try` 块时引发了异常，Python 会检查是否有相应的 `except` 语句来处理该异常。如果有匹配的 `except` 块，则转移到 `except` 块执行相应的处理。

#### 异常的类型匹配
当 `try` 块中引发的异常是 `except` 块中指定的异常类型或其子类时，`except` 块将执行。例如，`ZeroDivisionError` 是 `ArithmeticError` 的子类，因此处理 `ArithmeticError` 的 `except` 块也可以捕获 `ZeroDivisionError`。

### 一个简单的 `try-except` 示例
假设我们要处理除零错误，可以使用如下代码：
```python
try:
    x = 1 / 0
except ZeroDivisionError as e:
    print("Handling a", type(e))
    x = 0
```
当 `1 / 0` 引发 `ZeroDivisionError` 时，控制权转移到 `except` 块，程序输出错误信息，并将 `x` 赋值为 0。

#### 多个 `try-except`
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

### 使用 `try-except` 捕获特定错误
我们可以处理特定的错误类型，并针对不同的错误做不同的处理。例如：
```python
try:
    x = int("hello")  # 将字符串转换为整数
except ValueError:
    print("ValueError occurred")
except TypeError:
    print("TypeError occurred")
```
在这个例子中，`int("hello")` 会引发 `ValueError`，因为 `"hello"` 不能被转换为整数。

### 处理除零错误的函数示例
让我们定义一个函数 `invert(x)` 来计算 `1/x`，并且一个安全版本 `invert_safe(x)`，用于处理除零错误：
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

### 处理表达式中的错误
当一个异常在计算函数参数时引发时，函数调用不会发生。例如：
```python
def invert_safe(x):
    try:
        return 1 / x
    except ZeroDivisionError as e:
        print(f"Handling ZeroDivisionError: {e}")
        return 0

print(invert_safe(1 / 0))  # 这将引发 ZeroDivisionError
```
在这个例子中，`invert_safe` 函数甚至没有机会执行，因为 `1 / 0` 在参数计算时已经引发异常，直接导致程序报错。

### 递归调用中的异常
我们可以通过异常处理来控制递归深度过大的情况。例如：
```python
def recursive_function():
    return recursive_function()

try:
    recursive_function()
except RecursionError as e:
    print(f"Recursion error caught: {e}")
```
当递归深度超过 Python 的限制时，`RecursionError` 会被引发，并被 `except` 块捕获。

### `try-except` 的高级用法
我们还可以通过捕获异常来创建更具弹性的程序。在处理异常时，你可以返回默认值、打印调试信息或采取其他补救措施，而不是让程序崩溃。这对于需要稳定性和错误恢复的系统尤其重要。

### 总结
- **`try-except`**：用于捕获和处理异常，防止程序崩溃。
- **匹配异常类型**：通过指定异常类来匹配和处理特定的错误。
- **嵌套异常处理**：`try-except` 块可以嵌套，最内层的 `except` 块优先处理异常。
- **高级使用**：可以通过捕获异常，处理复杂的逻辑并提供替代行为，确保程序的健壮性。

通过掌握这些异常处理技术，你可以编写更加健壮、容错的 Python 程序，在发生错误时能够优雅地恢复和继续执行。





在 Python 中，异常处理不仅可以防止程序在遇到错误时崩溃，还可以帮助我们灵活地处理错误。特别是在某些复杂的场景下，我们可以结合异常处理和高阶函数来实现健壮的程序逻辑。

### 异常的传播与嵌套 `try-except`

当在函数调用链中某个地方抛出异常时，如果该异常被内部的 `try-except` 块处理，那么该异常不会再向外层传播。让我们来理解以下场景：

#### 例子：嵌套的 `try-except` 块
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

#### 处理外层异常
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

### 高阶函数中的异常处理：`reduce` 的例子

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

### 总结
- **嵌套异常处理**：当异常在内部的 `try-except` 块中被处理时，不会传播到外层的 `try-except` 块。
- **表达式的操作符优先级**：操作符优先于函数调用，如果表达式在计算操作符时出错，函数甚至不会被调用。
- **高阶函数中的异常处理**：通过将异常处理与实际的计算逻辑分离，我们可以编写健壮且易维护的代码。例如，`reduce` 专注于序列的递归操作，而 `divide_all_safe` 处理除法及其异常。

这种设计模式提供了清晰的责任分工，便于扩展和维护。



