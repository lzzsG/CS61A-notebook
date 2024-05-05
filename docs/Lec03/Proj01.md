---
layout: page
title: Proj 1. Functions and Control 
permalink: /Proj01/
nav_order: 1
parent: Lecture 3. Control




---

# Proj 1

## Introduction介绍

> **Important submission note:** For full credit:重要提交注意事项： 对于全额学分：
>
> - Submit with Phase 1 complete by **Monday, February 3** (worth 1 pt).在 2 月 3 日星期一之前完成第 1 阶段的提交（价值 1 分）。
> - Submit with Phases 2 and 3 complete by **Thursday, February 6**.请在 2 月 6 日星期四之前完成第 2 阶段和第 3 阶段的提交。
>
> Although the checkpoint date is only a few days from the final due date, you should not put off completing Phase 1. We recommend starting and finishing Phase 1 as soon as possible to give yourself adequate time to complete Phases 2 and 3, which are can be more time consuming.尽管检查点日期距离最终截止日期只有几天，但您不应推迟完成第 1 阶段。我们建议尽快开始和完成第 1 阶段，以便给自己足够的时间来完成第 2 阶段和第 3 阶段，这可以会更耗时。
>
> You do not have to wait until after the checkpoint date to start Phases 2 and 3.您不必等到检查点日期之后才开始第 2 阶段和第 3 阶段。
>
> Phase 1 is individual, Phases 2 and 3 can be completed with a partner.第 1 阶段是个人完成，第 2 阶段和第 3 阶段可以与合作伙伴一起完成。
>
> You can get 1 extra credit point by submitting the entire project one day early on **Wednesday, February 5**.您可以在 2 月 5 日星期三提前一天提交整个项目，获得 1 个额外学分。

In this project, you will develop a simulator and multiple strategies for the dice game Hog. You will need to use *control statements* and *higher-order functions* together, as described in Sections 1.2 through 1.6 of [Composing Programs](http://composingprograms.com/).在这个项目中，您将为骰子游戏 Hog 开发一个模拟器和多种策略。您需要同时使用控制语句和高阶函数，如《组合程序》第 1.2 节到 1.6 节中所述。

### Rules规则

In Hog, two players alternate turns trying to be the first to end a turn with at least 100 total points. On each turn, the current player chooses some number of dice to roll, up to 10. That player's score for the turn is the sum of the dice outcomes. However, a player who rolls too many dice risks:在《Hog》中，两名玩家轮流轮流尝试成为第一个以至少 100 分的总分结束回合的玩家。在每个回合中，当前玩家选择一定数量的骰子进行掷骰，最多 10 个。该玩家在该回合中的得分是骰子结果的总和。然而，掷过多骰子的玩家会面临以下风险：

- **Pig Out**. If any of the dice outcomes is a 1, the current player's score for the turn is 1.猪出来了。如果任一骰子结果为 1，则当前玩家该回合的得分为 1。

Examples例子

- *Example 1*: The current player rolls 7 dice, 5 of which are 1's. They score 1 point for the turn.示例 1：当前玩家掷 7 个骰子，其中 5 个为 1。他们在回合中得 1 分。
- *Example 2*: The current player rolls 4 dice, all of which are 3's. Since Pig Out did not occur, they score 12 points for the turn.例2：当前玩家掷了4个骰子，全部都是3。由于 Pig Out 没有发生，他们在这一回合得到 12 分。

In a normal game of Hog, those are all the rules. To spice up the game, we'll include some special rules:在正常的 Hog 游戏中，这些都是规则。为了让游戏更加有趣，我们将添加一些特殊规则：

- **Free Bacon**. A player who chooses to roll zero dice scores points equal to one more than the absolute alternating difference of the digits of the opponent's score cubed.免费培根。选择掷零骰子的玩家得分等于对手分数的数字的绝对交替差的立方多一。

Examples例子

- *Example 1*: The opponent has 4 points, and the current player chooses to roll zero dice. `4*4*4 = 64`, so the current player gets `1 + |6 - 4| = 3` points.例1：对手有4点，当前玩家选择掷零骰子。 4*4*4 = 64，所以当前玩家得到 1 + |6 - 4| = 3 分。
- *Example 2*: The opponent has 1 points, and the current player chooses to roll zero dice. `1*1*1 = 1`, so the current player gets `1 + |1| = 2` points.例2：对手有1分，当前玩家选择掷零骰子。 1*1*1 = 1，所以当前玩家得到1 + |1| = 2 分。
- *Example 3*: The opponent has 20 points, and the current player chooses to roll zero dice. `20*20*20 = 8000`, so the current player gets `1 + |8 - 0 + 0 - 0| = 9` points.例3：对手有20分，当前玩家选择掷零骰子。 20*20*20 = 8000，所以当前玩家获得 1 + |8 - 0 + 0 - 0| = 9 分。
- *Example 4*: The opponent has 45 points, and the current player chooses to roll zero dice. `45*45*45 = 91125`, so the current player gets `1 + |9 - 1 + 1 - 2 + 5| = 13` points.例4：对手有45分，当前玩家选择掷零骰子。 45*45*45 = 91125，所以当前玩家得到 1 + |9 - 1 + 1 - 2 + 5| = 13 分。

- **Feral Hogs**. If the number of dice you roll is exactly 2 away (absolute difference) from the number of points you scored on the previous turn, you get 3 extra points for the turn. Treat the turn before the first turn as scoring 0 points. Do **not** take into account any previous feral hog bonuses or swine swap (next rule) when calculating the number of points scored the previous turn.野猪。如果您掷出的骰子数量与上一回合的得分相差 2 分（绝对差值），则该回合您将获得 3 分额外积分。将第一个回合之前的回合视为得分 0 分。在计算上一回合的得分时，不要考虑任何以前的野猪奖金或猪交换（下一条规则）。

Examples例子

- *Example 1:示例1：*
  - Both players start out at 0. (0, 0)两名玩家都从 0 开始。(0, 0)
  - Player 0 rolls 3 dice and gets **7** points. (7, 0)玩家 0 掷 3 个骰子并获得 7 分。 (7, 0)
  - Player 1 rolls 1 dice and gets **4** points. (7, 4)玩家 1 掷 1 个骰子并获得 4 分。 (7, 4)
  - Player 0 rolls **5** dice and gets **10** points. **5** is 2 away from **7**, so player 0 gets a bonus of 3. (20, 4)玩家 0 掷 5 个骰子并获得 10 分。 5 距离 7 为 2，因此玩家 0 获得的奖励为 3。 (20, 4)
  - Player 1 rolls **2** dice and gets **8** points. **2** is 2 away from **4**, so player 1 gets a bonus of 3. (20, 15)玩家 1 掷 2 个骰子并获得 8 分。 2 距离 4 为 2，因此玩家 1 获得的奖励为 3。 (20, 15)
  - Player 0 rolls **8** dice and gets 20 points. **8** is 2 away from **10**, so player 0 gets a bonus of 3. (43, 15)玩家 0 掷 8 个骰子并获得 20 分。 8 距离 10 还差 2，因此玩家 0 获得的奖金为 3。 (43, 15)
  - Player 1 rolls **6** dice and gets 1 point. **6** is 2 away from **8**, so player 1 gets a bonus of 3. (43, 19)玩家 1 掷 6 个骰子并获得 1 分。 6 距离 8 为 2，因此玩家 1 获得的奖金为 3。 (43, 19)
- *Example 2:示例2：*
  - Both players start out at 0. (0, 0)两名玩家都从 0 开始。(0, 0)
  - Player 0 rolls 2 dice and gets 3 points. 2 is 2 away from 0, so player 0 gets a bonus of 3. (6, 0)玩家 0 掷 2 个骰子并获得 3 分。 2 距离 0 为 2，因此玩家 0 获得的奖励为 3。 (6, 0)

- **Swine Swap**. Define the *excitement* of the game to be three to the power of the sum of the players' scores. After points for the turn are added to the current player's score, if the excitement's first digit and last digit are the same, the scores should be swapped.猪交换。将游戏的兴奋度定义为玩家得分总和的三次方。当回合的分数与当前玩家的分数相加后，如果兴奋的第一位和最后一位数字相同，则应交换分数。

Examples例子

- *Example 1*: At the end of a turn, the players have scores of 2 and 4; 32 + 4 = 729, and 7 != 9, the scores are not swapped.例1：回合结束时，玩家的分数分别为2和4； 32 + 4 = 729，7 != 9，分数不交换。
- *Example 2*: At the end of a turn, the players have scores of 11 and 1; 311 + 1 = 531441, and 5 != 1, the scores are not swapped.例2：回合结束时，玩家的分数分别为11和1； 311 + 1 = 531441，并且5！= 1，分数不交换。
- *Example 3*: At the end of a turn, the players have scores of 1 and 0; 31 + 0 = 3, and 3 == 3, the scores are swapped.例3：回合结束时，玩家得分为1和0； 31 + 0 = 3，且3 == 3，分数交换。
- *Example 4*: At the end of a turn, the players have scores of 23 and 4; 323 + 4 = 7625597484987, and 7 == 7, the scores are swapped.例4：回合结束时，玩家的分数分别为23和4； 323 + 4 = 7625597484987，7 == 7，分数交换。

## Final Product完成品

Our staff solution to the project can be interacted with at [hog.cs61a.org](https://hog.cs61a.org/) -- if you'd like, try it out now! When you finish the project, you'll have implemented a significant part of this game yourself!我们的项目人员解决方案可以在 hog.cs61a.org 上进行交互——如果您愿意，现在就尝试一下！当您完成该项目时，您将自己实现该游戏的重要部分！

## Download starter files下载入门文件

To get started, download all of the project code as a [zip archive](https://inst.eecs.berkeley.edu/~cs61a/sp20/proj/hog/hog.zip). Below is a list of all the files you will see in the archive. However, you only have to make changes to `hog.py`.首先，将所有项目代码下载为 zip 存档。以下是您将在存档中看到的所有文件的列表。但是，您只需更改 hog.py 即可。

- `hog.py`: A starter implementation of Hoghog.py：Hog 的入门实现
- `dice.py`: Functions for rolling dicedice.py：掷骰子的函数
- `hog_gui.py`: A graphical user interface for Hoghog_gui.py：Hog 的图形用户界面
- `ucb.py`: Utility functions for CS 61Aucb.py：CS 61A 的实用函数
- `ok`: CS 61A autograder好的：CS 61A 自动平地机
- `tests`: A directory of tests used by `ok`测试：ok使用的测试目录
- `gui_files`: A directory of various things used by the web gui.gui_files：Web gui 使用的各种内容的目录。

## Logistics后勤

The project is worth 25 points. 22 points are assigned for correctness, 1 point for submitting Part I by the checkpoint date, and 2 points for the overall [composition](https://cs61a.org//articles/composition.html).该项目得分为25分。正确性得 22 分，在检查点日期之前提交第一部分得 1 分，整体作文得 2 分。

You will turn in the following files:您将上交以下文件：

- `hog.pyhog.py`

You do not need to modify or turn in any other files to complete the project. To submit the project, run the following command:您无需修改或提交任何其他文件即可完成该项目。要提交项目，请运行以下命令：

```python
python3 ok --submit
```

You will be able to view your submissions on the [Ok dashboard](http://ok.cs61a.org/).您将能够在 Ok 仪表板上查看您提交的内容。

For the functions that we ask you to complete, there may be some initial code that we provide. If you would rather not use that code, feel free to delete it and start from scratch. You may also add new function definitions as you see fit.对于我们要求您完成的功能，我们可能会提供一些初始代码。如果您不想使用该代码，请随意删除它并从头开始。您还可以根据需要添加新的函数定义。

However, please do **not** modify any other functions. Doing so may result in your code failing our autograder tests. Also, please do not change any function signatures (names, argument order, or number of arguments).但是，请不要修改任何其他功能。这样做可能会导致您的代码无法通过我们的自动评分器测试。另外，请不要更改任何函数签名（名称、参数顺序或参数数量）。

Throughout this project, you should be testing the correctness of your code. It is good practice to test often, so that it is easy to isolate any problems. However, you should not be testing *too* often, to allow yourself time to think through problems.在整个项目中，您应该测试代码的正确性。经常测试是一个很好的做法，这样就可以轻松隔离任何问题。但是，您不应该过于频繁地进行测试，以便让自己有时间思考问题。

We have provided an **autograder** called `ok` to help you with testing your code and tracking your progress. The first time you run the autograder, you will be asked to **log in with your Ok account using your web browser**. Please do so. Each time you run `ok`, it will back up your work and progress on our servers.我们提供了一个名为 ok 的自动评分器来帮助您测试代码并跟踪进度。第一次运行自动评分器时，系统会要求您使用网络浏览器使用 Ok 帐户登录。请这样做。每次您运行正常时，它都会在我们的服务器上备份您的工作和进度。

The primary purpose of `ok` is to test your implementations.ok 的主要目的是测试您的实现。

We recommend that you submit **after you finish each problem**. Only your last submission will be graded. It is also useful for us to have more backups of your code in case you run into a submission issue.我们建议您在完成每个问题后提交。只有您最后提交的内容才会被评分。如果您遇到提交问题，对您的代码进行更多备份对我们也很有用。

If you do not want us to record a backup of your work or information about your progress, you can run如果您不希望我们记录您的工作备份或有关您的进度的信息，您可以运行

```python
python3 ok --local
```

With this option, no information will be sent to our course servers. If you want to test your code interactively, you can run

使用此选项，不会将任何信息发送到我们的课程服务器。如果你想以交互方式测试你的代码，你可以运行

```python
 python3 ok -q [question number] -i 
```

with the appropriate question number (e.g. `01`) inserted. This will run the tests for that question until the first one you failed, then give you a chance to test the functions you wrote interactively.

插入适当的问题编号（例如 01）。这将运行该问题的测试，直到您的第一个失败，然后让您有机会以交互方式测试您编写的函数。

You can also use the debug printing feature in OK by writing您还可以通过编写以下内容来使用 OK 中的调试打印功能

```python
 print("DEBUG:", x) 
```

which will produce an output in your terminal without causing OK tests to fail with extra output.

这将在您的终端中产生输出，而不会导致 OK 测试因额外输出而失败。

## Graphical User Interface图形用户界面

A **graphical user interface** (GUI, for short) is provided for you. At the moment, it doesn't work because you haven't implemented the game logic. Once you complete the `play` function, you will be able to play a fully interactive version of Hog!为您提供了图形用户界面（简称GUI）。目前，它不起作用，因为你还没有实现游戏逻辑。完成播放功能后，您将可以玩完全互动版的Hog！

Once you've done that, you can run the GUI from your terminal:完成此操作后，您可以从终端运行 GUI：

```python
python3 hog_gui.py
```

## Phase 1: Simulator第一阶段：模拟器

> **Important submission note:** For full credit:重要提交注意事项： 对于全额学分：
>
> - submit with Phase 1 complete by **Monday, February 3** (worth 1 pt).在 2 月 3 日星期一之前完成第一阶段的提交（价值 1 分）。
>
> All Phase 1 tests must pass in order to receive this point.必须通过所有第一阶段测试才能获得该分数。

In the first phase, you will develop a simulator for the game of Hog.在第一阶段，您将为 Hog 游戏开发模拟器。

### Problem 0 (0 pt)问题 0 (0 分)

The `dice.py` file represents dice using non-pure zero-argument functions. These functions are non-pure because they may have different return values each time they are called. The documentation of `dice.py` describes the two different types of dice used in the project:dice.py 文件表示使用非纯零参数函数的骰子。这些函数是非纯函数，因为每次调用它们时可能有不同的返回值。 dice.py 的文档描述了项目中使用的两种不同类型的骰子：

- Dice can be fair, meaning that they produce each possible outcome with equal probability. Example: `six_sided`.骰子可以是公平的，这意味着它们以相同的概率产生每种可能的结果。示例：六边形。
- For testing functions that use dice, deterministic test dice always cycle through a fixed sequence of values that are passed as arguments to the `make_test_dice` function.对于使用骰子的测试函数，确定性测试骰子始终循环遍历作为参数传递给 make_test_dice 函数的固定值序列。

Before writing any code, read over the `dice.py` file and check your understanding by unlocking the following tests.在编写任何代码之前，请阅读 dice.py 文件并通过解锁以下测试来检查您的理解。

```python
python3 ok -q 00 -u
```

This should display a prompt that looks like this:这应该显示如下所示的提示：

```python
=====================================================================
Assignment: Project 1: Hog
Ok, version v1.5.2
=====================================================================

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Unlocking tests

At each "? ", type what you would expect the output to be.
Type exit() to quit

---------------------------------------------------------------------
Question 0 > Suite 1 > Case 1
(cases remaining: 1)

>>> test_dice = make_test_dice(4, 1, 2)
>>> test_dice()
?
```

You should type in what you expect the output to be. To do so, you need to first figure out what `test_dice` will do, based on the description above.您应该输入您期望的输出内容。为此，您需要首先根据上面的描述弄清楚 test_dice 将做什么。

You can exit the unlocker by typing `exit()`. **Typing Ctrl-C on Windows to exit out of the unlocker has been known to cause problems, so avoid doing so.**您可以通过键入 exit() 退出解锁器。已知在 Windows 上键入 Ctrl-C 退出解锁器会导致问题，因此请避免这样做。

### Problem 1 (2 pt)问题 1（2 分）

Implement the `roll_dice` function in `hog.py`. It takes two arguments: a positive integer called `num_rolls` giving the number of dice to roll and a `dice` function. It returns the number of points scored by rolling the dice that number of times in a turn: either the sum of the outcomes or 1 (*Pig Out*).在hog.py中实现roll_dice函数。它有两个参数：一个称为 num_rolls 的正整数，给出要滚动的骰子数量和一个 dice 函数。它返回每轮掷骰子一定次数所获得的分数：结果的总和或 1（Pig Out）。

> The Pig Out rule is reproduced below:Pig Out 规则转载如下：

- **Pig Out**. If any of the dice outcomes is a 1, the current player's score for the turn is 1.猪出来了。如果任一骰子结果为 1，则当前玩家该回合的得分为 1。
  - *Example 1*: The current player rolls 7 dice, 5 of which are 1's. They score 1 point for the turn.示例 1：当前玩家掷 7 个骰子，其中 5 个为 1。他们在回合中得 1 分。
  - *Example 2*: The current player rolls 4 dice, all of which are 3's. Since Pig Out did not occur, they score 12 points for the turn.例2：当前玩家掷了4个骰子，全部都是3。由于 Pig Out 没有发生，他们在这一回合得到 12 分。

To obtain a single outcome of a dice roll, call `dice()`. You should call `dice()` exactly `num_rolls` times in the body of `roll_dice`. Remember to call `dice()` exactly `num_rolls` times even if Pig Out happens in the middle of rolling. In this way, you correctly simulate rolling all the dice together.要获得掷骰子的单个结果，请调用 dice()。您应该在 roll_dice 主体中准确调用 dice() num_rolls 次。请记住，即使 Pig Out 发生在滚动过程中，也要准确调用 dice() num_rolls 次。通过这种方式，您可以正确地模拟将所有骰子掷到一起。

> You can't implement the feral hogs rule in this problem, since `roll_dice` doesn't have the previous number of rolls as an argument. It will be implemented later.在这个问题中你无法实现 feral hogs 规则，因为 roll_dice 没有之前的掷骰数作为参数。稍后将实施。

**Understand the problem**:了解问题：

Before writing any code, unlock the tests to verify your understanding of the question. **Note: you will not be able to test your code using OK until you unlock the test cases for the corresponding question**.在编写任何代码之前，请解锁测试以验证您对问题的理解。注意：在解锁相应问题的测试用例之前，您将无法使用“确定”来测试代码。

```python
python3 ok -q 01 -u
```

**Write code and check your work**:编写代码并检查您的工作：

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 01
```

Debugging Tips调试技巧

If the tests don't pass, it's time to debug. You can observe the behavior of your function using Python directly. First, start the Python interpreter and load the `hog.py` file.如果测试未通过，则需要进行调试。您可以直接使用 Python 观察函数的行为。首先，启动Python解释器并加载hog.py文件。

```python
python3 -i hog.py
```

Then, you can call your `roll_dice` function on any number of dice you want. The `roll_dice` function has a [default argument value](http://composingprograms.com/pages/14-designing-functions.html#default-argument-values) for `dice` that is a random six-sided dice function. Therefore, the following call to `roll_dice` simulates rolling four fair six-sided dice.然后，您可以对任意数量的骰子调用 roll_dice 函数。 roll_dice 函数有一个骰子的默认参数值，它是随机六面骰子函数。因此，以下对 roll_dice 的调用模拟掷出四个公平的六面骰子。

```python
>>> roll_dice(4)
```

You will find that the previous expression may have a different result each time you call it, since it is simulating random dice rolls. You can also use test dice that fix the outcomes of the dice in advance. For example, rolling twice when you know that the dice will come up 3 and 4 should give a total outcome of 7.您会发现前面的表达式每次调用时可能会产生不同的结果，因为它是模拟随机掷骰子。您还可以使用测试骰子来提前确定骰子的结果。例如，当您知道骰子会出现 3 和 4 时，掷两次，总结果应该是 7。

```python
>>> fixed_dice = make_test_dice(3, 4)
>>> roll_dice(2, dice=fixed_dice)
7
```

> On most systems, you can evaluate the same expression again by pressing the up arrow, then pressing enter or return. If you want to get the second last, third last, etc., command you made, press up arrow repeatedly.在大多数系统上，您可以通过按向上箭头，然后按 Enter 或 Return 来再次计算相同的表达式。如果您想获取倒数第二个、倒数第三个等命令，请重复按向上箭头。
>
> If you find a problem, you need to change your `hog.py` file, save it, quit Python, start it again, and then start evaluating expressions. Pressing the up arrow should give you access to your previous expressions, even after restarting Python.如果发现问题，则需要更改 hog.py 文件，保存它，退出 Python，再次启动它，然后开始计算表达式。按向上箭头应该可以访问以前的表达式，即使在重新启动 Python 后也是如此。

Continue debugging your code and running the `ok` tests until they all pass. You should follow this same procedure of understanding the problem, implementing a solution, testing, and debugging for all the problems on this project.继续调试您的代码并运行正确的测试，直到它们全部通过。您应该遵循同样的过程来理解问题、实施解决方案、测试和调试该项目中的所有问题。

> Note: to start the interpreter after the failing test is complete, try running `python3 ok -q 01 -i` instead. This will open an interpreter and then run the test until the first test example that fails.注意：要在失败的测试完成后启动解释器，请尝试运行 python3 ok -q 01 -i。这将打开一个解释器，然后运行测试，直到第一个测试示例失败。

### Problem 2 (1 pt)问题2（1分）

Implement the `free_bacon` helper function that returns the number of points scored by rolling 0 dice, based on the opponent's current `score`. You can assume that `score` is less than 100.实现 free_bacon 辅助函数，该函数根据对手的当前得分返回掷 0 颗骰子所得的分数。您可以假设分数小于 100。

> The Free Bacon rule is reproduced below:免费培根规则转载如下：

- **Free Bacon**. A player who chooses to roll zero dice scores points equal to one more than the absolute alternating difference of the digits of the opponent's score cubed.免费培根。选择掷零骰子的玩家得分等于对手分数的数字的绝对交替差的立方多一。
  - *Example 1*: The opponent has 4 points, and the current player chooses to roll zero dice. `4*4*4 = 64`, so the current player gets `1 + |6 - 4| = 3` points.例1：对手有4点，当前玩家选择掷零骰子。 4*4*4 = 64，所以当前玩家得到 1 + |6 - 4| = 3 分。
  - *Example 2*: The opponent has 1 points, and the current player chooses to roll zero dice. `1*1*1 = 1`, so the current player gets `1 + |1| = 2` points.例2：对手有1分，当前玩家选择掷零骰子。 1*1*1 = 1，所以当前玩家得到1 + |1| = 2 分。
  - *Example 3*: The opponent has 20 points, and the current player chooses to roll zero dice. `20*20*20 = 8000`, so the current player gets `1 + |8 - 0 + 0 - 0| = 9` points.例3：对手有20分，当前玩家选择掷零骰子。 20*20*20 = 8000，所以当前玩家获得 1 + |8 - 0 + 0 - 0| = 9 分。
  - *Example 4*: The opponent has 45 points, and the current player chooses to roll zero dice. `45*45*45 = 91125`, so the current player gets `1 + |9 - 1 + 1 - 2 + 5| = 13` points.例4：对手有45分，当前玩家选择掷零骰子。 45*45*45 = 91125，所以当前玩家得到 1 + |9 - 1 + 1 - 2 + 5| = 13 分。

> The built-in `abs` function returns the absolute value of its argument.内置的abs函数返回其参数的绝对值。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 02 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 02
```

You can also test `free_bacon` interactively by entering `python3 -i hog.py` in the terminal and then calling `free_bacon` with various inputs.您还可以通过在终端中输入 python3 -i hog.py 然后使用各种输入调用 free_bacon 来交互测试 free_bacon 。

### Problem 3 (2 pt)问题 3（2 分）

Implement the `take_turn` function, which returns the number of points scored for a turn by rolling the given `dice` `num_rolls` times.实现 take_turn 函数，该函数返回通过滚动给定骰子 num_rolls 次而获得的分数。

Your implementation of `take_turn` should call both `roll_dice` and `free_bacon` when possible.take_turn 的实现应该尽可能调用 roll_dice 和 free_bacon 。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 03 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 03
```

### Problem 4 (2 pt)问题 4（2 分）

Implement `is_swap`, which returns whether or not the scores should be swapped.实现 is_swap，它返回分数是否应该交换。

> The Swine Swap rule is reproduced below:猪互换规则转载如下：

- **Swine Swap**. Define the *excitement* of the game to be three to the power of the sum of the players' scores. After points for the turn are added to the current player's score, if the excitement's first digit and last digit are the same, the scores should be swapped.猪交换。将游戏的兴奋度定义为玩家得分总和的三次方。当回合的分数与当前玩家的分数相加后，如果兴奋的第一位和最后一位数字相同，则应交换分数。
  - *Example 1*: At the end of a turn, the players have scores of 2 and 4; 32 + 4 = 729, and 7 != 9, the scores are not swapped.例1：回合结束时，玩家的分数分别为2和4； 32 + 4 = 729，7 != 9，分数不交换。
  - *Example 2*: At the end of a turn, the players have scores of 11 and 1; 311 + 1 = 531441, and 5 != 1, the scores are not swapped.例2：回合结束时，玩家的分数分别为11和1； 311 + 1 = 531441，并且5！= 1，分数不交换。
  - *Example 3*: At the end of a turn, the players have scores of 1 and 0; 31 + 0 = 3, and 3 == 3, the scores are swapped.例3：回合结束时，玩家得分为1和0； 31 + 0 = 3，且3 == 3，分数交换。
  - *Example 4*: At the end of a turn, the players have scores of 23 and 4; 323 + 4 = 7625597484987, and 7 == 7, the scores are swapped.例4：回合结束时，玩家的分数分别为23和4； 323 + 4 = 7625597484987，7 == 7，分数交换。

> **IMPORTANT NOTE**: Do not import any external modules to accomplish this task, `python` can handle arbitrarily large numbers automatically. For example,重要提示：不要导入任何外部模块来完成此任务，Python 可以自动处理任意大的数字。例如，
>
> ```
> >>> 2 ** 1000
> 10715086071862673209484250490600018105614048117055336074437503883703510511249361224931983788156958581275946729175531468251871452856923140435984577574698574803934567774824230985421074605062371141877954182153046474983581941267398767559165543946077062914571196477686542167660429831652624386837205668069376
> ```

The `is_swap` function takes two arguments: the players' scores. It returns a boolean value to indicate whether the *Swine Swap* condition is met.is_swap 函数有两个参数：玩家的分数。它返回一个布尔值来指示是否满足 Swine Swap 条件。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 04 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 04
```

### Problem 5a (2 pt)问题 5a（2 分）

Implement the `play` function, which simulates a full game of Hog. Players alternate turns rolling dice until one of the players reaches the `goal` score.实现 play 函数，模拟完整的 Hog 游戏。玩家轮流掷骰子，直到其中一名玩家达到目标分数。

You can ignore the **Feral Hogs** rule and `feral_hogs` argument for now; You'll implement it in Problem 5b.您现在可以忽略 Feral Hogs 规则和 feral_hogs 参数；您将在问题 5b 中实现它。

To determine how much dice are rolled each turn, each player uses their respective strategy (Player 0 uses `strategy0` and Player 1 uses `strategy1`). A *strategy* is a function that, given a player's score and their opponent's score, returns the number of dice that the current player wants to roll in the turn. Each strategy function should be called only once per turn. Don't worry about the details of implementing strategies yet. You will develop them in Phase 3.为了确定每轮掷多少骰子，每个玩家都使用各自的策略（玩家 0 使用策略 0，玩家 1 使用策略 1）。策略是一个函数，给定玩家的分数和对手的分数，返回当前玩家想要在回合中掷骰子的数量。每个策略函数每回合只能调用一次。暂时不用担心实施策略的细节。您将在第三阶段开发它们。

When the game ends, `play` returns the final total scores of both players, with Player 0's score first, and Player 1's score second.当游戏结束时，游戏会返回两个玩家的最终总得分，其中玩家 0 的得分第一，玩家 1 的得分第二。

Here are some hints:以下是一些提示：

- You should use the functions you have already written! You will need to call `take_turn` with all three arguments.您应该使用您已经编写的函数！您需要使用所有三个参数来调用 take_turn。
- Only call `take_turn` once per turn.每回合仅调用 take_turn 一次。
- Enforce all the special rules except for feral hogs.执行除野猪之外的所有特殊规则。
- You can get the number of the other player (either 0 or 1) by calling the provided function `other`.您可以通过调用提供的函数 other 来获取其他玩家的号码（0 或 1）。
- You can ignore the `say` argument to the `play` function for now. You will use it in Phase 2 of the project.您现在可以忽略 play 函数的 say 参数。您将在项目的第二阶段使用它。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 05a -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 05a
```

### Problem 5b (1 pt)问题 5b（1 分）

Now, implement the Feral Hogs rule. When `play` is called **and** its `feral_hogs` argument is `True`, then this rule should be imposed. If `feral_hogs` is `False`, this rule should be ignored. (That way, test cases for 5a will still pass after you solve 5b.)现在，实施野猪规则。当调用 play 且其 feral_hogs 参数为 True 时，应强制执行此规则。如果 feral_hogs 为 False，则应忽略此规则。 （这样，在解决 5b 后，5a 的测试用例仍然会通过。）

> The Feral Hogs rule is reproduced below:野猪规则转载如下：

- **Feral Hogs**. If the number of dice you roll is exactly 2 away (absolute difference) from the number of points you scored on the previous turn, you get 3 extra points for the turn. Treat the turn before the first turn as scoring 0 points. Do **not** take into account any previous feral hog bonuses or swine swap (next rule) when calculating the number of points scored the previous turn.野猪。如果您掷出的骰子数量与上一回合的得分相差 2 分（绝对差值），则该回合您将获得 3 分额外积分。将第一个回合之前的回合视为得分 0 分。在计算上一回合的得分时，不要考虑任何以前的野猪奖金或猪交换（下一条规则）。
  - *Example 1:示例1：*
    - Both players start out at 0. (0, 0)双方玩家均从 0 开始。(0, 0)
    - Player 0 rolls 3 dice and gets **7** points. (7, 0)玩家 0 掷 3 个骰子并获得 7 分。 (7, 0)
    - Player 1 rolls 1 dice and gets **4** points. (7, 4)玩家 1 掷 1 个骰子并获得 4 分。 (7, 4)
    - Player 0 rolls **5** dice and gets **10** points. **5** is 2 away from **7**, so player 0 gets a bonus of 3. (20, 4)玩家 0 掷 5 个骰子并获得 10 分。 5 距离 7 为 2，因此玩家 0 获得的奖励为 3。 (20, 4)
    - Player 1 rolls **2** dice and gets **8** points. **2** is 2 away from **4**, so player 1 gets a bonus of 3. (20, 15)玩家 1 掷 2 个骰子并获得 8 分。 2 距离 4 为 2，因此玩家 1 获得的奖励为 3。 (20, 15)
    - Player 0 rolls **8** dice and gets 20 points. **8** is 2 away from **10**, so player 0 gets a bonus of 3. (43, 15)玩家 0 掷 8 个骰子并获得 20 分。 8 距离 10 还差 2，因此玩家 0 获得的奖金为 3。 (43, 15)
    - Player 1 rolls **6** dice and gets 1 point. **6** is 2 away from **8**, so player 1 gets a bonus of 3. (43, 19)玩家 1 掷 6 个骰子并获得 1 分。 6 距离 8 为 2，因此玩家 1 获得的奖金为 3。 (43, 19)
  - *Example 2:示例2：*
    - Both players start out at 0. (0, 0)两名玩家都从 0 开始。(0, 0)
    - Player 0 rolls 2 dice and gets 3 points. 2 is 2 away from 0, so player 0 gets a bonus of 3. (6, 0)玩家 0 掷 2 个骰子并获得 3 分。 2 距离 0 为 2，因此玩家 0 获得的奖励为 3。 (6, 0)

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 05b -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 05b
```

Also make sure to re-run the checks for 5a. If these don't pass anymore, perhaps you're not using the `feral_hogs` argument correctly.还要确保重新运行 5a 的检查。如果这些不再通过，也许您没有正确使用 feral_hogs 参数。

```python
python3 ok -q 05a
```

> The last test for Question 5b is a *fuzz test*, which checks that your `play` function works for a large number of different inputs. Failing this test means something is wrong, but the issue could be caused by errors in your answers to previous problems.问题 5b 的最后一个测试是模糊测试，它检查您的播放函数是否适用于大量不同的输入。未通过此测试意味着出现问题，但该问题可能是由您对之前问题的答案中的错误引起的。

Once you are finished, you will be able to play a graphical version of the game. We have provided a file called `hog_gui.py` that you can run from the terminal:完成后，您将能够玩游戏的图形版本。我们提供了一个名为 hog_gui.py 的文件，您可以从终端运行它：

```python
python3 hog_gui.py
```

The GUI relies on your implementation, so if you have any bugs in your code, they will be reflected in the GUI. This means you can also use the GUI as a debugging tool; however, it's better to run the tests first.GUI 依赖于您的实现，因此如果您的代码中有任何错误，它们将反映在 GUI 中。这意味着您还可以使用 GUI 作为调试工具；但是，最好先运行测试。

Make sure to submit your work so far before the checkpoint deadline:确保在检查点截止日期之前提交您的作业：

```python
python3 ok --submit
```

Check to make sure that you did all the problems in Phase 1:检查并确保您已完成第一阶段中的所有问题：

```python
python3 ok --score
```

Congratulations! You have finished Phase 1 of this project!恭喜！您已经完成了该项目的第一阶段！

## Phase 2: Commentary第二阶段：评论

> You can work on and submit Phase 2 and 3 with a partner! Make sure one of you submits and then adds the other as a partner on okpy.org.您可以与合作伙伴一起完成并提交第 2 阶段和第 3 阶段！确保其中一人提交，然后将另一人添加为 okpy.org 上的合作伙伴。

In the second phase, you will implement commentary functions that print remarks about the game after each turn, such as, `"22 points! That's the biggest gain yet for Player 1."`在第二阶段，您将实现评论功能，在每个回合后打印有关游戏的评论，例如“22分！这是玩家1迄今为止的最大收获”。

A commentary function takes two arguments, Player 0's current score and Player 1's current score. It can print out commentary based on either or both current scores and any other information in its parent environment. Since commentary can differ from turn to turn depending on the current point situation in the game, a commentary function always returns another commentary function to be called on the next turn. The only side effect of a commentary function should be to print.评论函数有两个参数：玩家 0 的当前得分和玩家 1 的当前得分。它可以根据当前分数及其父环境中的任何其他信息打印评论。由于评论可能会根据游戏中当前的得分情况而有所不同，因此评论函数总是返回另一个评论函数以在下一回合调用。注释功能的唯一副作用应该是打印。

### Commentary examples注释示例

The function `say_scores` in `hog.py` is an example of a commentary function that simply announces both players' scores. Note that `say_scores` returns itself, meaning that the same commentary function will be called each turn.hog.py 中的函数 say_scores 是一个评论函数的示例，它只是宣布两个玩家的分数。请注意，say_scores 返回自身，这意味着每轮都会调用相同的评论函数。

```python
def say_scores(score0, score1):
    """A commentary function that announces the score for each player."""
    print("Player 0 now has", score0, "and Player 1 now has", score1)
    return say_scores
```

The function `announce_lead_changes` is an example of a higher-order function that returns a commentary function that tracks lead changes. A different commentary function will be called each turn.函数announce_lead_changes 是一个高阶函数的示例，它返回跟踪引导更改的注释函数。每回合都会调用不同的评论功能。

```python
def announce_lead_changes(prev_leader=None):
    """Return a commentary function that announces lead changes.

    >>> f0 = announce_lead_changes()
    >>> f1 = f0(5, 0)
    Player 0 takes the lead by 5
    >>> f2 = f1(5, 12)
    Player 1 takes the lead by 7
    >>> f3 = f2(8, 12)
    >>> f4 = f3(8, 13)
    >>> f5 = f4(15, 13)
    Player 0 takes the lead by 2
    """
    def say(score0, score1):
        if score0 > score1:
            leader = 0
        elif score1 > score0:
            leader = 1
        else:
            leader = None
        if leader != None and leader != prev_leader:
            print('Player', leader, 'takes the lead by', abs(score0 - score1))
        return announce_lead_changes(leader)
    return say
```

You should also understand the function `both`, which takes two commentary functions (`f` and `g`) and returns a *new* commentary function. This returned commentary function returns *another* commentary function which calls the functions returned by calling `f` and `g`, in that order.您还应该了解函数 Both，它接受两个注释函数（f 和 g）并返回一个新的注释函数。这个返回的注释函数返回另一个注释函数，该函数按顺序调用通过调用 f 和 g 返回的函数。

```python
def both(f, g):
    """Return a commentary function that says what f says, then what g says.

    NOTE: the following game is not possible under the rules, it's just
    an example for the sake of the doctest

    >>> h0 = both(say_scores, announce_lead_changes())
    >>> h1 = h0(10, 0)
    Player 0 now has 10 and Player 1 now has 0
    Player 0 takes the lead by 10
    >>> h2 = h1(10, 6)
    Player 0 now has 10 and Player 1 now has 6
    >>> h3 = h2(6, 17)
    Player 0 now has 6 and Player 1 now has 17
    Player 1 takes the lead by 11
    """
    def say(score0, score1):
        return both(f(score0, score1), g(score0, score1))
    return say
```

### Problem 6 (2 pt)问题 6 (2 分)

Update your `play` function so that a commentary function is called at the end of each turn. The return value of calling a commentary function gives you the commentary function to call on the next turn.更新您的播放函数，以便在每回合结束时调用评论函数。调用注释函数的返回值会为您提供下一轮要调用的注释函数。

For example, `say(score0, score1)` should be called at the end of the first turn. Its return value (another commentary function) should be called at the end of the second turn. Each consecutive turn, call the function that was returned by the call to the previous turn's commentary function.例如，say(score0, Score1) 应该在第一回合结束时调用。它的返回值（另一个注释函数）应该在第二轮结束时调用。每个连续回合，调用由调用前一回合的注释函数返回的函数。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 06 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 06
```

### Problem 7 (3 pt)问题 7 (3 分)

Implement the `announce_highest` function, which is a higher-order function that returns a commentary function. This commentary function announces whenever a particular player gains more points in a turn than ever before. E.g., `announce_highest(1)` and its return value ignore Player 0 entirely and just print information about Player 1. To compute the gain, it must compare the score from last turn to the score from this turn for the player of interest, which is designated by the `who` argument. This function must also keep track of the highest gain for the player so far.实现announce_highest函数，这是一个返回注释函数的高阶函数。每当特定玩家在回合中获得比以往更多的分数时，此评论功能就会宣布。例如，announce_highest(1) 及其返回值完全忽略玩家 0，只打印有关玩家 1 的信息。为了计算增益，它必须将感兴趣的玩家上一回合的得分与本回合的得分进行比较，该玩家被指定为由谁论证。此函数还必须跟踪玩家迄今为止的最高增益。

The way in which `announce_highest` announces is very specific, and your implementation should match the doctests provided. Don't worry about singular versus plural when announcing point gains; you should simply use "point(s)" for both cases.ounce_highest 宣布的方式非常具体，您的实现应该与提供的文档测试相匹配。在宣布积分增益时，不要担心单数还是复数；对于这两种情况，您应该简单地使用“点”。

> **Hint.** The `announce_lead_changes` function provided to you is an example of how to keep track of information using commentary functions. If you are stuck, first make sure you understand how `announce_lead_changes` works.暗示。提供给您的announce_lead_changes 函数是如何使用注释函数跟踪信息的示例。如果您遇到困难，请首先确保您了解announce_lead_changes 的工作原理。

> **Note:** The doctests for `both`/`announce_highest` in hog.py might describe a game that can't occur according to the rules. This shouldn't be an issue for commentary functions since they don't implement any of the rules of the game.注意：hog.py 中的 Both/announce_highest 的文档测试可能描述了根据规则无法发生的游戏。对于评论功能来说这不应该是问题，因为它们不执行任何游戏规则。

> **Hint.** If you're getting a `local variable [var] reference before assignment` error:暗示。如果您在分配错误之前获得局部变量 [var] 引用：
>
> This happens because in Python, you aren't normally allowed to modify variables defined in parent frames. Instead of reassigning `[var]`, the interpreter thinks you're trying to define a new variable within the current frame. We'll learn about how to work around this in a future lecture, but it is not required for this problem.发生这种情况是因为在 Python 中，通常不允许您修改父框架中定义的变量。解释器认为您正在尝试在当前框架内定义一个新变量，而不是重新分配 [var]。我们将在以后的讲座中了解如何解决这个问题，但这不是这个问题所必需的。
>
> To fix this, you have two options:要解决此问题，您有两种选择：
>
> 1) Rather than reassigning `[var]` to its new value, create a new variable to hold that new value. Use that new variable in future calculations.1) 创建一个新变量来保存该新值，而不是将 [var] 重新分配给它的新值。在以后的计算中使用该新变量。
> 2) For this problem specifically, avoid this issue entirely by not using assignment statements at all. Instead, pass new values in as arguments to a call to `announce_highest`.2）具体针对这个问题，完全不使用赋值语句来完全避免这个问题。相反，将新值作为参数传递给对announce_highest 的调用。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 07 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 07
```

When you are done, you will see commentary in the GUI:完成后，您将在 GUI 中看到注释：

```python
python3 hog_gui.py
```

The commentary in the GUI is generated by passing the following function as the `say` argument to `play`.GUI 中的注释是通过将以下函数作为 say 参数传递给 play 来生成的。

```python
both(announce_highest(0), both(announce_highest(1), announce_lead_changes()))
```

Great work! You just finished Phase 2 of the project!做得好！您刚刚完成了该项目的第二阶段！

## Phase 3: Strategies第三阶段：策略

In the third phase, you will experiment with ways to improve upon the basic strategy of always rolling a fixed number of dice. First, you need to develop some tools to evaluate strategies.在第三阶段，您将尝试改进始终掷固定数量骰子的基本策略的方法。首先，您需要开发一些工具来评估策略。

### Problem 8 (2 pt)问题8（2分）

Implement the `make_averaged` function, which is a higher-order function that takes a function `g` as an argument. It returns another function that takes the same number of arguments as `g` (the function originally passed into `make_averaged`). This returned function differs from the input function in that it returns the average value of repeatedly calling `g` on the same arguments. This function should call `g` a total of `num_samples` times and return the average of the results.实现 make_averaging 函数，它是一个以函数 g 作为参数的高阶函数。它返回另一个函数，该函数采用与 g 相同数量的参数（最初传递给 make_averaging 的函数）。此返回函数与输入函数的不同之处在于，它返回对相同参数重复调用 g 的平均值。该函数应总共调用 g num_samples 次并返回结果的平均值。

To implement this function, you need a new piece of Python syntax! You must write a function that accepts an arbitrary number of arguments, then calls another function using exactly those arguments. Here's how it works.要实现这个功能，你需要一段新的Python语法！您必须编写一个接受任意数量参数的函数，然后使用这些参数调用另一个函数。这是它的工作原理。

Instead of listing formal parameters for a function, you can write `*args`. To call another function using exactly those arguments, you call it again with `*args`. For example,您可以编写 *args，而不是列出函数的形式参数。要完全使用这些参数调用另一个函数，可以使用*args 再次调用它。例如，

```python
>>> def printed(g):
...     def print_and_return(*args):
...         result = g(*args)
...         print('Result:', result)
...         return result
...     return print_and_return
>>> printed_pow = printed(pow)
>>> printed_pow(2, 8)
Result: 256
256
>>> printed_abs = printed(abs)
>>> printed_abs(-10)
Result: 10
10
```

Read the docstring for `make_averaged` carefully to understand how it is meant to work.仔细阅读 make_averaging 的文档字符串以了解它的工作原理。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 08 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 08
```

### Problem 9 (2 pt)问题9（2分）

Implement the `max_scoring_num_rolls` function, which runs an experiment to determine the number of rolls (from 1 to 10) that gives the maximum average score for a turn. Your implementation should use `make_averaged` and `roll_dice`.实现 max_scoring_num_rolls 函数，该函数运行实验来确定给出一轮最大平均得分的掷骰数（从 1 到 10）。您的实现应该使用 make_averaging 和 roll_dice。

If two numbers of rolls are tied for the maximum average score, return the lower number. For example, if both 3 and 6 achieve a maximum average score, return 3.如果两个掷骰数的最大平均分数相同，则返回较低的数字。例如，如果 3 和 6 都达到了最大平均分数，则返回 3。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 09 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 09
```

To run this experiment on randomized dice, call `run_experiments` using the `-r` option:要在随机骰子上运行此实验，请使用 -r 选项调用 run_experiments：

```python
python3 hog.py -r
```

**Running experiments** For the remainder of this project, you can change the implementation of `run_experiments` as you wish. By calling `average_win_rate`, you can evaluate various Hog strategies. For example, change the first `if False:` to `if True:` in order to evaluate `always_roll(8)` against the baseline strategy of `always_roll(6)`.运行实验 对于本项目的其余部分，您可以根据需要更改 run_experiments 的实现。通过调用average_win_rate，您可以评估各种Hog策略。例如，将第一个 if False: 更改为 if True: 以便根据always_roll(6) 的基线策略评估always_roll(8)。

Some of the experiments may take up to a minute to run. You can always reduce the number of samples in your call to `make_averaged` to speed up experiments.有些实验可能需要一分钟才能运行。您始终可以减少调用 make_averaging 时的样本数量以加快实验速度。

### Problem 10 (1 pt)问题10（1分）

A strategy can try to take advantage of the *Free Bacon* rule by rolling 0 when it is most beneficial to do so. Implement `bacon_strategy`, which returns 0 whenever rolling 0 would give **at least** `margin` points and returns `num_rolls` otherwise.策略可以尝试利用免费培根规则，在最有利的时候掷 0。实现 bacon_strategy，只要滚动 0 至少给出保证金点，它就返回 0，否则返回 num_rolls。

> Note it is impossible for strategies to know what number of points the current player earned on the previous turn, and thus we cannot predict feral hogs. For strategies, we do not take into account bonuses from feral hogs to calculate bonuses against the margin or whether a swap will occur请注意，策略不可能知道当前玩家在上一回合中获得了多少积分，因此我们无法预测野猪。对于策略，我们不考虑野猪的奖金来计算保证金奖金或是否会发生掉期

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 10 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 10
```

Once you have implemented this strategy, change `run_experiments` to evaluate your new strategy against the baseline. Is it better than just rolling 4?实施此策略后，更改 run_experiments 以根据基线评估新策略。是不是比直接滚4更好？

### Problem 11 (2 pt)问题11（2分）

A strategy can also take advantage of the *Swine Swap* rule. The swap strategy always rolls 0 if doing so triggers a beneficial swap and always avoids rolling 0 if doing so triggers a detrimental swap. In other cases, it rolls 0 if rolling 0 would give **at least** `margin` points. Otherwise, the strategy rolls `num_rolls`.策略还可以利用猪互换规则。如果这样做会触发有益的交换，则交换策略始终滚动 0；如果这样做会触发有害的交换，则始终避免滚动 0。在其他情况下，如果滚动 0 至少给出边缘点，则滚动 0。否则，该策略将滚动 num_rolls。

> Note it is impossible for strategies to know what number of points the current player earned on the previous turn, and thus we cannot predict feral hogs. For strategies, we do not take into account bonuses from feral hogs to calculate bonuses against the margin or whether a swap will occur请注意，策略不可能知道当前玩家在上一回合中获得了多少积分，因此我们无法预测野猪。对于策略，我们不考虑野猪的奖金来计算保证金奖金或是否会发生掉期
>
> Hint: a tie is technically a "swap" (e.g., 43 being swapped with 43), but is considered neither detrimental nor beneficial for the purposes of this problem.提示：从技术上讲，平局是一种“交换”（例如，43 与 43 交换），但对于此问题的目的而言，被认为既无害也无益。

Before writing any code, unlock the tests to verify your understanding of the question.在编写任何代码之前，请解锁测试以验证您对问题的理解。

```python
python3 ok -q 11 -u
```

Once you are done unlocking, begin implementing your solution. You can check your correctness with:完成解锁后，开始实施您的解决方案。您可以通过以下方式检查您的正确性：

```python
python3 ok -q 11
```

Once you have implemented this strategy, update `run_experiments` to evaluate your new strategy against the baseline. You should find that it gives a significant edge over `always_roll(4)`.实施此策略后，请更新 run_experiments 以根据基线评估您的新策略。您应该发现它比always_roll(4) 具有显着的优势。

### Optional: Problem 12 (0 pt)可选：问题 12（0 分）

Implement `final_strategy`, which combines these ideas and any other ideas you have to achieve a high win rate against the `always_roll(4)` strategy. Some suggestions:实施final_strategy，它结合了这些想法和任何其他想法，以实现针对always_roll(4) 策略的高胜率。一些建议：

- `swap_strategy` is a good default strategy to start with.swap_strategy 是一个很好的默认策略。
- There's no point in scoring more than 100. Check whether you can win by rolling 0, 1 or 2 dice. If you are in the lead, you might take fewer risks.得分超过 100 就没有意义。看看您是否可以通过掷 0、1 或 2 个骰子获胜。如果你处于领先地位，你可能会承担更少的风险。
- Try to force a beneficial swap rolling more than 0 dice.尝试强制进行有益的交换，掷骰子数超过 0。
- Choose the `num_rolls` and `margin` arguments carefully.仔细选择 num_rolls 和 margin 参数。
- Take the action that is most likely to win the game.采取最有可能赢得比赛的行动。

You can check that your final strategy is valid by running Ok.您可以通过运行“确定”来检查您的最终策略是否有效。

```python
python3 ok -q 12
```

You can also check your exact final win rate by running您还可以通过运行来检查您确切的最终获胜率

```python
python3 calc.py
```

This should pop up a window asking for you to confirm your identity, and then it will print out a win rate for your final strategy. If it doesn't and instead hangs, please download a fresh calc.py from [here](https://inst.eecs.berkeley.edu/~cs61a/sp20/proj/hog/calc.py) and put it in your `hog` folder.这应该会弹出一个窗口，要求您确认您的身份，然后它将打印出您最终策略的胜率。如果没有出现并且挂起，请从此处下载新的 calc.py 并将其放入您的 hog 文件夹中。

The old `calc.py` technically worked but took over an hour to give a solution, this version just sends your strategy to our server where we use a super-fast implementation of hog to calculate your win rate.旧的 calc.py 在技术上可以工作，但需要一个多小时才能给出解决方案，这个版本只是将您的策略发送到我们的服务器，我们使用 hog 的超快速实现来计算您的获胜率。

At this point, run the entire autograder to see if there are any tests that don't pass.此时，运行整个自动评分器以查看是否有任何测试未通过。

```python
python3 ok
```

Once you are satisfied, submit to Ok to complete the project.一旦您满意，请提交“确定”以完成项目。

```python
python3 ok --submit
```

If you have a partner, make sure to add them to the submission on okpy.org.如果您有合作伙伴，请确保将他们添加到 okpy.org 上的提交内容中。

Check to make sure that you did all the problems by running检查以确保您通过运行解决了所有问题

```python
python3 ok --score
```

You can also play against your final strategy with the graphical user interface:您还可以使用图形用户界面来对抗您的最终策略：

```python
python3 hog_gui.py
```

The GUI will alternate which player is controlled by you.GUI 将交替由您控制哪个玩家。

Congratulations, you have reached the end of your first CS 61A project! If you haven't already, relax and enjoy a few games of Hog with a friend.恭喜，您的第一个 CS 61A 项目已结束！如果您还没有准备好，请放松一下，与朋友一起玩几场 Hog 游戏。
