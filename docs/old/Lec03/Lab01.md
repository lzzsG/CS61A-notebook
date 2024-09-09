---
layout: page
title: Lab 1. Functions and Control 
permalink: /Lab01/
nav_order: 1
parent: Lecture 3. Control



---

# Lab 1. Functions and Control 

## Starter Files入门文件

Download [lab01.zip](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab01/lab01.zip). Inside the archive, you will find starter files for the questions in this lab, along with a copy of the [Ok](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab01/ok) autograder.下载 lab01.zip。在存档中，您将找到本实验中问题的入门文件，以及 Ok 自动评分器的副本。

## Submission提交

By the end of this lab, you should have submitted the lab with `python3 ok --submit`. You may submit more than once before the deadline; only the final submission will be graded. Check that you have successfully submitted your code on [okpy.org](https://okpy.org/).在本实验结束时，您应该已经使用 python3 ok --submit 提交了实验。您可以在截止日期前多次提交；仅对最终提交的作品进行评分。检查您是否已在 okpy.org 上成功提交代码。

Additionally, please fill out [this survey](https://forms.gle/rbuv3eKpYKY4tepw7) with any issues you might have faced in Lab 0 Python installation or if you used the Windows automated installer.此外，请填写此调查，说明您在 Lab 0 Python 安装中或使用 Windows 自动安装程序时可能遇到的任何问题。

# Quick Logistics Review快速物流审核

## Using Python

## Using Python使用Python

When running a Python file, you can use options on the command line to inspect your code further. Here are a few that will come in handy. If you want to learn more about other Python command-line options, take a look at the [documentation](https://docs.python.org/3.4/using/cmdline.html).运行 Python 文件时，您可以使用命令行上的选项来进一步检查代码。这里有一些会派上用场的。如果您想了解有关其他 Python 命令行选项的更多信息，请查看文档。

- Using no command-line options will run the code in the file you provide and return you to the command line.不使用命令行选项将运行您提供的文件中的代码并返回到命令行。

  ```
  python3 
  ```

- **`-i`**: The `-i` option runs your Python script, then opens an interactive session. In an interactive session, you run Python code line by line and get immediate feedback instead of running an entire file all at once. To exit, type `exit()` into the interpreter prompt. You can also use the keyboard shortcut `Ctrl-D` on Linux/Mac machines or `Ctrl-Z Enter` on Windows.-i：-i 选项运行 Python 脚本，然后打开交互式会话。在交互式会话中，您可以逐行运行 Python 代码并获得即时反馈，而不是一次运行整个文件。要退出，请在解释器提示符中键入 exit()。您还可以在 Linux/Mac 计算机上使用键盘快捷键 Ctrl-D 或在 Windows 上使用 Ctrl-Z Enter。

  If you edit the Python file while running it interactively, you will need to exit and restart the interpreter in order for those changes to take effect.如果您在交互运行 Python 文件时对其进行编辑，则需要退出并重新启动解释器才能使这些更改生效。

  ```
  python3 -i 
  ```

- **`-m doctest`**: Runs doctests in a particular file. Doctests are surrounded by triple quotes (`"""`) within functions.-m doctest：在特定文件中运行 doctest。文档测试在函数内用三引号 (""") 括起来。

  Each test in the file consists of `>>>` followed by some Python code and the expected output (though the `>>>` are not seen in the output of the doctest command).文件中的每个测试都由 >>> 组成，后跟一些 Python 代码和预期输出（尽管在 doctest 命令的输出中看不到 >>>）。

  ```bash
   python3 -m doctest 
  ```

## Using OK

## Using OK使用确定

In 61A, we use a program called Ok for autograding labs, homeworks, and projects. You should have Ok in the starter files downloaded at the start of this lab. For more information on using Ok commands, learn more [here](http://cs61a.org/articles/using-ok.html). To use Ok to run doctests for a specified function, run the following command:在 61A 中，我们使用一个名为 Ok 的程序来自动评分实验室、作业和项目。在本实验开始时下载的入门文件中应该显示“Ok”。有关使用 Ok 命令的更多信息，请在此处了解更多信息。要使用 Ok 为指定函数运行 doctest，请运行以下命令：

```bash
python3 ok -q <specified function>
```

By default, only tests that did not pass will show up. You can use the `-v` option to show all tests, including tests you have passed:默认情况下，仅显示未通过的测试。您可以使用 -v 选项显示所有测试，包括您已通过的测试：

```bash
python3 ok -v
```

You can also use the debug printing feature in OK by writing您还可以通过编写以下内容来使用 OK 中的调试打印功能

```bash
print("DEBUG:", x)
```

Finally, when you have finished all the questions in [lab01.py](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab01/lab01.py), you must submit the assignment using the `--submit` option:最后，当您完成 lab01.py 中的所有问题后，您必须使用 --submit 选项提交作业：

```bash
python3 ok --submit
```

For more Ok commands, visit [here](https://cal-cs-61a-staff.github.io/ok-help/).有关更多 Ok 命令，请访问此处。

# Topics主题

Consult this section if you need a refresher on the material for this lab. It's okay to skip directly to [the questions](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab01/#required-questions) and refer back here should you get stuck.如果您需要复习本实验的材料，请参阅本部分。如果您遇到困难，可以直接跳到问题并返回此处参考。

## Division分配

Let's compare the different division-related operators in Python:让我们比较一下 Python 中不同的除法相关运算符：

| True Division: `/`真除法： / (decimal division)（十进制除法） | Floor Division: `//`楼层划分：// (integer division)（整数除法） | Modulo: `%`模：% (remainder)（余）                           |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `>>> 1 / 5 0.2 >>> 25 / 4 6.25 >>> 4 / 2 2.0 >>> 5 / 0 ZeroDivisionError ` | `>>> 1 // 5 0 >>> 25 // 4 6 >>> 4 // 2 2 >>> 5 // 0 ZeroDivisionError ` | `>>> 1 % 5 1 >>> 25 % 4 1 >>> 4 % 2 0 >>> 5 % 0 ZeroDivisionError ` |

Notice that Python outputs `ZeroDivisionError` for certain cases. We will go over this later in this lab under [Error Messages](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab01/#error-messages).请注意，Python 在某些情况下会输出 ZeroDivisionError。我们稍后将在本实验室的“错误消息”下讨论这一点。

One useful technique involving the `%` operator is to check whether a number `x` is divisible by another number `y`:涉及 % 运算符的一种有用技术是检查数字 x 是否可以被另一个数字 y 整除：

```python
x % y == 0
```

For example, in order to check if `x` is an even number:例如，为了检查 x 是否为偶数：

```python
x % 2 == 0
```

## Functions功能

If we want to execute a series of statements over and over, we can abstract them away into a function to avoid repeating code.如果我们想要一遍又一遍地执行一系列语句，我们可以将它们抽象成一个函数以避免重复代码。

For example, let's say we want to know the results of multiplying the numbers 1-3 by 3 and then adding 2 to it. Here's one way to do it:例如，假设我们想知道数字 1-3 乘以 3，然后加上 2 的结果。这是一种方法：

```python
>>> 1 * 3 + 2
5
>>> 2 * 3 + 2
8
>>> 3 * 3 + 2
11
```

If we wanted to do this with a larger set of numbers, that'd be a lot of repeated code! Let's write a function to capture this operation given any input number.如果我们想用更大的数字集来做到这一点，那就需要很多重复的代码！让我们编写一个函数来捕获给定任何输入数字的此操作。

```python
def foo(x):
    return x * 3 + 2
```

This function, called `foo`, takes in a single **argument** and will **return** the result of multiplying that argument by 3 and adding 2.这个函数称为 foo，接受一个参数，并返回该参数乘以 3 再加上 2 的结果。

Now we can **call** this function whenever we want this operation to be done:现在，只要我们想要完成此操作，就可以调用此函数：

```python
>>> foo(1)
5
>>> foo(2)
8
>>> foo(1000)
3002
```

Applying a function to some arguments is done with a **call expression**.将函数应用于某些参数是通过调用表达式完成的。

### Call expressions调用表达式

A call expression applies a function, which may or may not accept arguments. The call expression evaluates to the function's return value.调用表达式应用一个函数，该函数可能接受也可能不接受参数。调用表达式的计算结果为函数的返回值。

The syntax of a function call:函数调用的语法：

```python
  add   (    2   ,    3   )
   |         |        |
operator  operand  operand
```

Every call expression requires a set of parentheses delimiting its comma-separated operands.每个调用表达式都需要一组括号来分隔其逗号分隔的操作数。

To evaluate a function call:要评估函数调用：

1. Evaluate the operator, and then the operands (from left to right).先评估运算符，然后评估操作数（从左到右）。
2. Apply the operator to the operands (the values of the operands).将运算符应用于操作数（操作数的值）。

If an operand is a nested call expression, then these two steps are applied to that inner operand first in order to evaluate the outer operand.如果操作数是嵌套调用表达式，则首先将这两个步骤应用于该内部操作数，以便计算外部操作数。

### `return` and `print`返回并打印

Most functions that you define will contain a `return` statement. The `return` statement will give the result of some computation back to the caller of the function and exit the function. For example, the function `square` below takes in a number `x` and returns its square.您定义的大多数函数都将包含 return 语句。 return 语句将一些计算的结果返回给函数的调用者并退出函数。例如，下面的函数 square 接受数字 x 并返回其平方。

```python
def square(x):
    """
    >>> square(4)
    16
    """
    return x * x
```

When Python executes a `return` statement, the function terminates immediately. If Python reaches the end of the function body without executing a `return` statement, it will automatically return `None`.当Python执行return语句时，函数立即终止。如果Python到达函数体末尾而没有执行return语句，它将自动返回None。

In contrast, the `print` function is used to display values in the Terminal. This can lead to some confusion between `print` and `return` because calling a function in the Python interpreter will print out the function's return value.相反，打印功能用于在终端中显示值。这可能会导致 print 和 return 之间出现一些混淆，因为在 Python 解释器中调用函数会打印出函数的返回值。

However, unlike a `return` statement, when Python evaluates a `print` expression, the function does *not* terminate immediately.但是，与 return 语句不同，当 Python 计算 print 表达式时，该函数不会立即终止。

```python
def what_prints():
    print('Hello World!')
    return 'Exiting this function.'
    print('61A is awesome!')

>>> what_prints()
Hello World!
'Exiting this function.'
```

> Notice also that `print` will display text **without the quotes**, but `return` will preserve the quotes.另请注意， print 将显示不带引号的文本，但 return 将保留引号。

## Control控制

### Boolean Operators布尔运算符

Python supports three boolean operators: `and`, `or`, and `not`:Python 支持三种布尔运算符：and、or 和 not：

```python
>>> a = 4
>>> a < 2 and a > 0
False
>>> a < 2 or a > 0
True
>>> not (a > 0)
False
```

- `and` evaluates to `True` only if both operands evaluate to `True`. If at least one operand is `False`, then `and` evaluates to `False`.仅当两个操作数的计算结果均为 True 时，计算结果才为 True。如果至少有一个操作数为 False，则 和 的计算结果为 False。
- `or` evaluates to `True` if at least one operand evaluates to `True`. If both operands are `False`, then `or` evaluates to `False`.如果至少一个操作数计算结果为 True，则 or 计算结果为 True。如果两个操作数均为 False，则 or 的计算结果为 False。
- `not` evaluates to `True` if its operand evaluates to `False`. It evaluates to `False` if its operand evalutes to `True`.如果其操作数计算结果为 False，则 not 计算结果为 True。如果其操作数计算结果为 True，则计算结果为 False。

What do you think the following expression evaluates to? Try it out in the Python interpreter.您认为以下表达式的计算结果是什么？在 Python 解释器中尝试一下。

```python
>>> True and not False or not True and False
```

It is difficult to read complex expressions, like the one above, and understand how a program will behave. Using parentheses can make your code easier to understand. Python interprets that expression in the following way:阅读复杂的表达式（如上面的表达式）并理解程序的行为方式是很困难的。使用括号可以使您的代码更易于理解。 Python 按以下方式解释该表达式：

```python
>>> (True and (not False)) or ((not True) and False)
```

This is because boolean operators, like arithmetic operators, have an order of operation:这是因为布尔运算符与算术运算符一样，也有一个运算顺序：

- `not` has the highest priority没有最高优先级
- `and和`
- `or` has the lowest priority或者具有最低优先级

It turns out `and` and `or` work on more than just booleans (`True`, `False`). Python values such as `0`, `None`, `''` (the empty string), and `[]` (the empty list) are considered false values. *All* other values are considered true values.事实证明 and 和 or 不仅仅适用于布尔值（True、False）。 Python 值（例如 0、None、''（空字符串）和 []（空列表））被视为假值。所有其他值均被视为真实值。

#### Short Circuiting短路

What do you think will happen if we type the following into Python?如果我们在 Python 中输入以下内容，你认为会发生什么？

```python
1 / 0
```

Try it out in Python! You should see a `ZeroDivisionError`. But what about this expression?在 Python 中尝试一下！您应该看到 ZeroDivisionError。但这个表情又如何呢？

```python
True or 1 / 0
```

It evaluates to `True` because Python's `and` and `or` operators *short-circuit*. That is, they don't necessarily evaluate every operand.它的计算结果为 True，因为 Python 的 and 和 or 运算符短路了。也就是说，它们不一定评估每个操作数。

| Operator操作员 | Checks if:检查是否：                          | Evaluates from left to right up to:从左到右评估： | Example例子                                                  |
| :------------- | :-------------------------------------------- | :------------------------------------------------ | :----------------------------------------------------------- |
| AND和          | All values are true所有值均为真               | The first false value第一个假值                   | `False and 1 / 0` evaluates to `False`False 且 1 / 0 计算结果为 False |
| OR或者         | At least one value is true至少有一个值是 true | The first true value第一个真实值                  | `True or 1 / 0` evaluates to `True`True 或 1 / 0 计算结果为 True |

Short-circuiting happens when the operator reaches an operand that allows them to make a conclusion about the expression. For example, `and` will short-circuit as soon as it reaches the first false value because it then knows that not all the values are true.当运算符到达允许他们对表达式做出结论的操作数时，就会发生短路。例如， 和 一旦达到第一个假值就会短路，因为它知道并非所有值都是真的。

If `and` and `or` do not *short-circuit*, they just return the last value; another way to remember this is that `and` and `or` always return the last thing they evaluate, whether they short circuit or not. Keep in mind that `and` and `or` don't always return booleans when using values other than `True` and `False`.如果 and 和 or 不短路，则只返回最后一个值；记住这一点的另一种方法是 and 和 or 总是返回它们评估的最后一个东西，无论它们是否短路。请记住，当使用 True 和 False 以外的值时，and 和 or 并不总是返回布尔值。

### If Statements如果语句

You can review the syntax of `if` statements in [Section 1.5.4](http://composingprograms.com/pages/15-control.html#conditional-statements) of Composing Programs.您可以在《编写程序》的 1.5.4 节中查看 if 语句的语法。

> *Tip*: We sometimes see code that looks like this:提示：我们有时会看到如下所示的代码：
>
> ```python
> if x > 3:
>     return True
> else:
>     return False
> ```
>
> This can be written more concisely as `return x > 3`. If your code looks like the code above, see if you can rewrite it more clearly!可以更简洁地写为 return x > 3。如果您的代码类似于上面的代码，看看是否可以重写得更清楚！

### While LoopsWhile 循环

You can review the syntax of `while` loops in [Section 1.5.5](http://composingprograms.com/pages/15-control.html#iteration) of Composing Programs.您可以在《编写程序》的 1.5.5 节中查看 while 循环的语法。

## Error Messages错误信息

By now, you've probably seen a couple of error messages. They might look intimidating, but error messages are very helpful for debugging code. The following are some common types of errors:到目前为止，您可能已经看到了一些错误消息。它们可能看起来很吓人，但错误消息对于调试代码非常有帮助。以下是一些常见的错误类型：

| Error Types错误类型         | Descriptions说明                                             |
| :-------------------------- | :----------------------------------------------------------- |
| SyntaxError语法错误         | Contained improper syntax (e.g. missing a colon after an `if` statement or forgetting to close parentheses/quotes)包含不正确的语法（例如，if 语句后缺少冒号或忘记关闭括号/引号） |
| IndentationError缩进错误    | Contained improper indentation (e.g. inconsistent indentation of a function body)包含不正确的缩进（例如函数体的缩进不一致） |
| TypeError类型错误           | Attempted operation on incompatible types (e.g. trying to add a function and a number) or called function with the wrong number of arguments尝试对不兼容的类型进行操作（例如尝试添加函数和数字）或使用错误数量的参数调用函数 |
| ZeroDivisionError零除法错误 | Attempted division by zero尝试除以零                         |

Using these descriptions of error messages, you should be able to get a better idea of what went wrong with your code. **If you run into error messages, try to identify the problem before asking for help.** You can often Google unfamiliar error messages to see if others have made similar mistakes to help you debug.使用这些错误消息的描述，您应该能够更好地了解代码出了什么问题。如果您遇到错误消息，请在寻求帮助之前尝试找出问题。你经常可以Google一下不熟悉的错误信息，看看其他人是否也犯过类似的错误，以帮助你调试。

For example:例如：

```python
>>> square(3, 3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: square() takes 1 positional argument but 2 were given
```

Note:笔记：

- The last line of an error message tells us the type of the error. In the example above, we have a `TypeError`.错误消息的最后一行告诉我们错误的类型。在上面的例子中，我们有一个类型错误。
- The error message tells us what we did wrong -- we gave `square` 2 arguments when it can only take in 1 argument. In general, the last line is the most helpful.错误消息告诉我们做错了什么——当它只能接受 1 个参数时，我们给出了 2 个参数。一般来说，最后一行是最有帮助的。
- The second to last line of the error message tells us on which line the error occurred. This helps us track down the error. In the example above, `TypeError` occurred at `line 1`.错误消息的倒数第二行告诉我们错误发生在哪一行。这有助于我们追踪错误。在上面的示例中，TypeError 发生在第 1 行。



# Required Questions必答问题

## What Would Python Display? (Part 1)Python 会显示什么？ （第1部分）

### Q1: WWPD: ControlQ1：WWPD：控制

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:使用 Ok 通过以下“Python 将显示什么？”来测试您的知识。问题：
>
> ```bash
> python3 ok -q control -u
> ```

```python
>>> def xk(c, d):
...     if c == 4:
...         return 6
...     elif d >= 4:
...         return 6 + 7 + c
...     else:
...         return 25
>>> xk(10, 10)
______
>>> xk(10, 6)
______
>>> xk(4, 6)
______
>>> xk(0, 0)
______
>>> def how_big(x):
...     if x > 10:
...         print('huge')
...     elif x > 5:
...         return 'big'
...     elif x > 0:
...         print('small')
...     else:
...         print("nothin'")
>>> how_big(7)
______
>>> how_big(12)
______
>>> how_big(1)
______
>>> how_big(-1)
______
>>> n = 3
>>> while n >= 0:
...     n -= 1
...     print(n)
______
```

> *Hint*: Make sure your `while` loop conditions eventually evaluate to a false value, or they'll never stop! Typing `Ctrl-C` will stop infinite loops in the interpreter.提示：确保您的 while 循环条件最终计算结果为假值，否则它们将永远不会停止！输入 Ctrl-C 将停止解释器中的无限循环。

```python
>>> positive = 28
>>> while positive:
...    print("positive?")
...    positive -= 3
______
>>> positive = -9
>>> negative = -12
>>> while negative:
...    if positive:
...        print(negative)
...    positive += 3
...    negative += 3
______
```

### Q2: WWPD: VeritasinessQ2：WWPD：真实性

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:使用 Ok 通过以下“Python 将显示什么？”来测试您的知识。问题：
>
> ```bash
> python3 ok -q short-circuit -u
> ```

```python
>>> True and 13
______
>>> False or 0
______
>>> not 10
______
>>> not None
______
>>> True and 1 / 0 and False
______
>>> True or 1 / 0 or False
______
>>> True and 0
______
>>> False or 1
______
>>> 1 and 3 and 6 and 10 and 15
______
>>> 0 or False or 2 or 1 / 0
______
>>> not 0
______
>>> (1 + 1) and 1
______
>>> 1/0 or True
______
>>> (True or False) and False
______
```

### Q3: Debugging Quiz!Q3：调试测验！

The following is a quick quiz on different debugging techniques you should use in this class. You should refer to [this document](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/debugging.html) to answer the questions!以下是关于您应该在本课程中使用的不同调试技术的快速测验。您应该参考此文档来回答问题！

Run the following to run the quiz.运行以下命令来运行测验。

```bash
python3 ok -q debugging-quiz -u
```

## Coding Practice编码练习

### Q4: Fix the BugQ4：修复Bug

The following snippet of code doesn't work! Figure out what is wrong and fix the bugs.下面的代码片段不起作用！找出问题所在并修复错误。

```python
def both_positive(a, b):
    """Returns True if both a and b are positive.

    >>> both_positive(-1, 1)
    False
    >>> both_positive(1, 1)
    True
    """
    return a and b > 0 # You can replace this line!
```

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q both_positive
```

### Q5: Sum DigitsQ5：数字求和

Write a function that takes in a nonnegative integer and sums its digits. (Using floor division and modulo might be helpful here!)编写一个函数，它接受一个非负整数并对它的数字求和。 （在这里使用除法和取模可能会有所帮助！）

```python
def sum_digits(x):
    """Sum all the digits of x.

    >>> sum_digits(10) # 1 + 0 = 1
    1
    >>> sum_digits(4224) # 4 + 2 + 2 + 4 = 12
    12
    >>> sum_digits(1234567890)
    45
    >>> a = sum_digits(123) # make sure that you are using return rather than print
    >>> a
    6
    """
    "*** YOUR CODE HERE ***"
```

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q sum_digits
```

## Submit提交

Make sure to submit this assignment by running:确保通过运行以下命令提交此作业：

```bash
python3 ok --submit
```

# Optional Questions可选问题

## What Would Python Display? (Part 2)Python 会显示什么？ （第2部分）

### Q6: WWPD: What If?问题 6：WWPD：如果怎么办？

> Use Ok to test your knowledge with the following "What Would Python Display?" questions:使用 Ok 通过以下“Python 将显示什么？”来测试您的知识。问题：
>
> ```bash
> python3 ok -q if-statements -u
> ```
>
> **Hint**: `print` (unlike `return`) does *not* cause the function to exit!提示：print（与 return 不同）不会导致函数退出！

```python
>>> def ab(c, d):
...     if c > 5:
...         print(c)
...     elif c > 7:
...         print(d)
...     print('foo')
>>> ab(10, 20)
______
>>> def bake(cake, make):
...     if cake == 0:
...         cake = cake + 1
...         print(cake)
...     if cake == 1:
...         print(make)
...     else:
...         return cake
...     return make
>>> bake(0, 29)
______
>>> bake(1, "mashed potatoes")
______
```

## More Coding Practice更多编码练习

### Q7: Falling FactorialQ7：阶乘下降

Let's write a function `falling`, which is a "falling" factorial that takes two arguments, `n` and `k`, and returns the product of `k` consecutive numbers, starting from `n` and working downwards.让我们编写一个函数 Falling，它是一个“下降”阶乘，它接受两个参数 n 和 k，并返回从 n 开始向下计算的 k 个连续数字的乘积。

```python
def falling(n, k):
    """Compute the falling factorial of n to depth k.

    >>> falling(6, 3)  # 6 * 5 * 4
    120
    >>> falling(4, 3)  # 4 * 3 * 2
    24
    >>> falling(4, 1)  # 4
    4
    >>> falling(4, 0)
    1
    """
    "*** YOUR CODE HERE ***"
```

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q falling
```

### Q8: Double EightsQ8：双八

Write a function that takes in a number and determines if the digits contain two adjacent 8s.编写一个函数，该函数接收一个数字并确定这些数字是否包含两个相邻的 8。

```python
def double_eights(n):
    """Return true if n has two eights in a row.
    >>> double_eights(8)
    False
    >>> double_eights(88)
    True
    >>> double_eights(2882)
    True
    >>> double_eights(880088)
    True
    >>> double_eights(12345)
    False
    >>> double_eights(80808080)
    False
    """
    "*** YOUR CODE HERE ***"
```

Use Ok to test your code:使用“确定”来测试您的代码：

```bash
python3 ok -q double_eights
```