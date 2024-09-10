---
layout: page
title: L06 Design
permalink: /L06
description: "Lecture 6. Design"
nav_order: 6








---

# Lecture 6. Design

## Announcements

**期中考试一**将于**周一**举行。如果由于时间冲突或考试时间处于夜间需要调整考试时间，请在**本周四**之前填写**替代时间申请表**。考试期间需要**录制屏幕和头部**，确保你独立完成考试。可选择使用Zoom、Loom或手机录制。请尽早**练习录制2小时视频**，以确保考试当天录制过程顺利。

如果需要**申请免除监考政策**，请在**本周四**之前提交申请。**周五**我们将提供一次**练习考试**，时间为**下午1点到2点**和**晚上7点到8点**，之后48小时内可随时完成练习。练习考试将使用与正式考试相同的软件，建议录制自己参加练习考试的过程，确保一切正常。

你可以创建一张**双面的复习笔记**，也可以使用草稿纸。若选择将笔记电子存储，唯一允许的方式是使用Google Doc，并确保不与他人共享，还需提供编辑权限给 `csixton@berkeley.edu`。不会编辑内容，但需确保我们能查看。

**HKN（Ada Kappa Nu）**学生组织计划在**周六下午1点到4点（太平洋时间）**举办一次复习会议，详情将在Piazza上发布。

根据**第二周的反馈**，所有实验的截止时间调整为**周二**，包括实验二，其截止时间为本周二。**Hog项目**的第一阶段也将于本周二截止，需提交**第5题**，但不包括第6题。提交后将获得**检查点1分**，该分数不高，但仍应完成。提前提交可额外获得1分，建议在**周四**之前完成。

我们将在今天晚上**7点到9点**举办**项目派对**，并有大量**预约时间**可供选择。每天晚上10点会发布次日的新预约时间。如果不想等待排队，建议预约一个确定的时间。此外，你也可以加入**办公室时间队列**，但并非所有时间都开放，具体开放时间可在**办公室时间页面**查看。

最近收到很多**私人Piazza帖子**，由于数量较多，回复可能会有延迟，但我们会确保所有问题都得到解答。

最后，**Hog图形用户界面（GUI）**问题已修复。此前版本不支持同一玩家连续两次行动，这是本学期的新规则。若要使用更新的GUI，请重新下载项目文件，保留旧工作并替换GUI文件。

**讨论二**及相关教程将在**周三**举行，请务必**先参加导向会议**，然后再参加教程，否则教程将难以理解。周五还有一次**考试准备会议**，所有的Zoom链接和讲座问答环节链接已提供。本周没有新内容，因为需要专注于**完成项目**并准备**期中考试**。

本周课程没有新的内容，因为同学们需要花时间**完成项目**并准备期中考试。今天的课程将简要讨论如何设计一个**大型程序**，并通过一个扩展的示例进行讲解。周五的课程主要是复习和考试准备，将涵盖一些**往年考试题目**及其解题思路。

## 抽象概念——函数抽象
**函数抽象**指的是将某个计算过程赋予一个名字，然后在后续使用时只需调用该名字，而无需关心其具体的实现细节。

![image-20240910110019063]({{ site.baseurl }}/docs/assets/image-20240910110019063.png)

### 示例：`square` 和 `sum_squares` 函数
- `square` 函数用于计算数字的平方，`sum_squares` 函数则调用 `square`。
- **关键问题**：`sum_squares` 需要了解 `square` 的哪些信息才能正确调用它？

**回答**：

1. **是否需要知道 `square` 接受一个参数**？  
   是的，否则无法正确调用。
2. **是否需要知道 `square` 的内在名字是 `square`**？  
   不需要，内在名字只为人类检查，任何绑定到当前环境中 `square` 名字的函数都可以被正确调用。
3. **是否需要知道 `square` 的行为，即它计算一个数的平方**？  
   是的，正确使用函数抽象时，必须知道它的行为。
4. **是否需要知道 `square` 是通过 `mull` 函数实现平方计算的**？  
   不需要，它可以通过任何方式计算平方，只要实现结果正确。

我们可以通过内置的 `pow` 函数来计算平方，或者采用其它方法，只要 `sum_squares` 依赖的 `square` 函数行为不变，就不会影响其正确性。

## 选择命名的建议
命名对人类理解代码至关重要，但对程序的**正确性**没有直接影响。好的命名可以显著提升程序的可读性和可维护性。

### 命名规则：
1. **名称应传达其值的意义或用途**，便于理解为何创建该值以及它的用途。
2. **值的类型（如数字、字符串）最好在函数的注释中说明**，而不是体现在变量名中。
3. **函数命名**应反映其**效果**（如打印）、**行为**（如三倍化）或**返回值**（如绝对值）。

![image-20240910110039643]({{ site.baseurl }}/docs/assets/image-20240910110039643.png)

### 命名建议：
- 避免将布尔变量命名为 `trueFalse`，而应根据其意义命名，如 `playerRolledOne`（表示游戏中玩家掷出了1）。
- 避免使用单个字母如 `d`，应使用有意义的名称如 `dice`。
- 函数命名应基于其功能，而不是调用者。举例来说，**不要**将函数命名为 `playHelper`，而应命名为 `takeTurn`，因为该函数的实际作用是模拟一次回合。
- 避免用类型来命名变量，如 `myInt`，应使用更具描述性的名称，如 `numberOfRolls`。

### 不推荐的命名：
- 某些字母如 `l`、`I` 和 `O` 容易与数字 `1` 和 `0` 混淆，建议使用 `k`、`r`、`m` 等字母作为单字符变量。

![image-20240910110406229]({{ site.baseurl }}/docs/assets/image-20240910110406229.png)

### 如何决定值是否需要命名

不是所有中间值都需要命名，但如果同一个复杂的表达式在代码中多次出现，最好赋予它一个名称，这样便于维护。

**示例**：

如果代码中多次计算 `sqrt(square(a) + square(b))`，建议给它命名为 `hypotenuse`(斜边)，这样如果计算逻辑需要修改，只需改动一个地方。

此外，尽量避免编写**过于复杂的表达式**，即便计算机能够处理复杂代码，过于复杂的表达式对人类理解不利。

### 命名技巧

在代码命名方面，有一些额外的建议：
- **长名称**是可以接受的，特别是在帮助解释代码含义时。如果一个赋值语句是用来计算某个学生的平均年龄，并命名为`average_age`，这是一种清晰表达代码意图的好方法。相比之下，使用注释并配以更复杂的表达式，不如直接通过清晰的命名来解释代码更好。
- **短名称**也可以接受，尤其是当它们代表通用量时。例如，表示实数的绝对值、计数器或某些数学操作的参数，甚至是封装某个通用函数的情况。但需要了解一些常见的命名**约定**，这些约定在多种编程语言中都有应用。某些字母常用于表示整数，某些字母表示实数，另一些字母则表示函数。

虽然这些约定并非必须遵守，但它们有助于使代码更具可读性。如果你选择遵循这些约定，其他程序员会更容易理解你的代码。然而，编写程序也是一种创造性行为，关键在于代码对他人具有可读性。

## Function Example: Sounds

## 高阶函数 示例：生成声音文件

学生常常会问，**高阶函数**的意义是什么。例如，`make_adder` 函数很有趣，但为什么不直接加上 `x` 和 `y`，而要构建一个高阶函数呢？为了解释这个问题，我们构建了一个稍长的示例，展示为何在程序的早期定义多个函数，并在程序的最后阶段才处理这些函数，可能会更有利。

![image-20240910110611751]({{ site.baseurl }}/docs/assets/image-20240910110611751.png)

我们将使用Python来生成一个**WAV文件**，这是编码声音的标准格式。虽然WAV文件现在很少使用，因为它占用大量空间，但它的格式非常简单，没有压缩，容易生成。

WAV文件的作用是**直接编码声音波形的样本**。声音是波动的，波形在任意时刻都有振幅，而**采样**的作用是通过记录波形在特定时刻的高度（振幅）来将其数字化。为了生成逼真的声音，我们将在每分钟采集**11000个样本**，以获得足够精确的波形近似。

通常，这些波形是通过**录制真实世界中的声音**产生的，但我们也可以通过**数学函数**生成波形。在电子音乐中，常见的波形有**正弦波**、**方波**、**三角波**和**锯齿波**。在这个例子中，我们选择**三角波**，因为它的音质比其他几种波形更好。

## 生成WAV文件的Python代码

在这个解释中，我们逐步构建一个更复杂的音乐片段，通过结合多个波形并为生成的声音添加节奏。让我们一步步解析，从生成一个简单的三角波开始，逐渐过渡到更复杂的声音组合和节奏。

### 0. **基本配置**

```python
frame_rate = 11025
```

`frame_rate`表示每秒的采样数，决定音频文件的质量。11025是一个常用的低质量音频采样率，常用于简单的音频生成。

### 1. **`encode` 函数**

```python
def encode(x):
    """Encode float x between -1 and 1 as two bytes."""
    i = int(16384 * x)
    return Struct('h').pack(i)
```

该函数将一个范围在`-1`到`1`之间的浮点数`x`编码为16位整数，并打包为两个字节（16位）。`Struct('h')`表示一个16位有符号整数的结构，用于将浮点数转换成WAV文件所需的整数格式。

### 2. **写入 WAV 文件**
`play` 函数将声音写入 `.wav` 文件。我们选择文件名（例如 `song.wav`），并设置声音播放的持续时间（以秒为单位）。`sampler` 函数定义声音的波形，通过在每个时间步生成 `-1` 到 `1` 之间的值，这些值代表波形的振幅。

```python
def play(sampler, name='song.wav', seconds=2):
     """Write the output of a sampler function as a wav file."""
    out = open(name, 'wb')
    out.setnchannels(1)
    out.setsampwidth(2)
    out.setframerate(frame_rate)
    t = 0
    while t < seconds * frame_rate:
        sample = sampler(t)
        out.writeframes(encode(sample))
        t += 1
    out.close()
```

`play` 函数接受一个采样器函数`sampler`作为参数，函数会每次调用 `sampler(t)` 来生成某个时间点 `t` 的波形数据，然后将这些数据编码为 `.wav` 文件中的音频帧。`sampler`是一个随时间变化的函数，负责生成时间点 `t` 对应的波形值。

`setnchannels(1)`表示单声道，`setsampwidth(2)`表示每个样本使用两个字节（16位），`setframerate(frame_rate)`指定音频的采样率。

在主循环中，`sampler(t)`生成第`t`帧的音频样本，`encode(sample)`将该样本编码为两个字节并写入文件。

### 3. **生成三角波**
接下来，我们需要定义一个三角波。三角波是一个周期性波形，我们需要指定它的频率`frequency`（决定音高）和振幅`amplitude`（决定音量）。生成三角波的公式如下：

```python
def tri(frequency, amplitude=0.3):
    """A continuous triangle wave."""
    period = frame_rate // frequency
    def sampler(t):
        saw_wave = t / period - floor(t / period + 0.5)
        tri_wave = 2 * abs(2 * saw_wave) - 1
        return amplitude * tri_wave
    return sampler
```

这个三角波函数 `tri` 会根据频率 `frequency` 和振幅 `amplitude` 生成一个波形。我们用 `saw_wave` 来构建三角波的基础，然后通过数学运算生成 `tri_wave`。`sampler(t)`返回给定时间`t`的波形值。

### 4. **音符函数 `note`**

```python
def note(f, start, end, fade=.01):
    """Play f for a fixed duration."""
    def sampler(t):
        seconds = t / frame_rate
        if seconds < start:
            return 0
        elif seconds > end:
            return 0
        elif seconds < start + fade:
            return (seconds - start) / fade * f(t)
        elif seconds > end - fade:
            return (end - seconds) / fade * f(t)
        else:
            return f(t)
    return sampler
```

`note`函数用来播放一个音符`f`，并在指定的时间段内衰减音量（渐入/渐出效果）。它通过检测当前时间是否在音符的播放时间范围内，控制是否播放音符并应用淡入和淡出效果。

### 5. **组合函数 `both`**

```python
def both(f, g):
    return lambda t: f(t) + g(t)
```

`both`函数将两个采样器`f`和`g`组合成一个新的采样器，这个采样器在每个时间点`t`返回两个采样器输出的和，实现同时播放多个音符的效果。

### 6. **生成单个音符并播放**
我们首先生成并播放单个音符。例如，生成一个 C 音符（频率为 261.63 Hz），并将其播放为四分音符。

```python
c_freq = 261.63  # C 音符频率

# 播放 C 音符，持续时间为 1/4 秒
play(note(tri(c_freq), start=0, end=0.25))
```

在这个例子中，`note` 函数用于指定音符的开始时间和结束时间，而 `play` 函数将音符写入一个 `.wav` 文件并播放。

### 7. **组合音符**
如果我们想播放多个音符，比如在 C 音符之后播放 E 音符（329.63 Hz），我们可以使用 `both` 函数将两个音符组合在一起。

```python
e_freq = 329.63  # E 音符频率

# 播放 C 音符，然后播放 E 音符
play(both(note(tri(c_freq), 0, 0.25), note(tri(e_freq), 0.5, 1)))
```

在这个例子中，C 音符从 0 秒开始播放，持续四分之一秒；E 音符在 0.5 秒开始播放，持续半秒。这种组合让我们能够创建更复杂的旋律。

### 8. **优化音符音质**
为了让音符听起来更加自然，我们可以添加淡入和淡出的效果。通过 `note` 函数中的 `fade` 参数，我们可以控制音符的音量如何逐渐增加和减小，以避免音符开始和结束时产生不自然的“划痕”声。

```python
# 在音符的开始和结束时添加淡入淡出效果
play(note(tri(c_freq), start=0, end=0.25, fade=0.01))
```

在这里，我们将音符的淡入淡出时间设置为 0.01 秒，听起来更加平滑。

### 9. **创建旋律**
我们可以根据这些基本音符组合创建更复杂的旋律，例如模仿经典的 **Mario** 游戏主题曲。每个音符有不同的开始时间和持续时间，并且通过 `both` 函数将音符组合在一起。

```python
def mario(c, e, g, low_g):
    z = 0
    song = note(e, z, z + 0.125)  # 第一个 E 音符
    z += 0.125
    song = both(song, note(e, z, z + 0.125))  # 第二个 E 音符
    z += 0.25
    song = both(song, note(e, z, z + 0.125))  # 第三个 E 音符
    z += 0.25
    song = both(song, note(c, z, z + 0.125))  # C 音符
    z += 0.125
    song = both(song, note(e, z, z + 0.125))  # E 音符
    z += 0.25
    song = both(song, note(g, z, z + 0.25))   # G 音符
    z += 0.5
    song = both(song, note(low_g, z, z + 0.25))  # 低 G 音符
    return song
```

### 10. **不同八度的旋律**
我们可以调整音符的频率来改变旋律的八度。例如，通过将音符的频率乘以 2 可以将旋律提高一个八度，将频率除以 2 则降低一个八度。我们定义了一个 `mario_at` 函数，用于在不同八度下播放 Mario 主题。

```python
def mario_at(octave):
    c = tri(octave * c_freq)
    e = tri(octave * e_freq)
    g = tri(octave * g_freq)
    low_g = tri(octave * g_freq / 2)
    return mario(c, e, g, low_g)

# 播放 Mario 主题曲，不同的八度
play(both(mario_at(1), mario_at(0.5)))
```

这里，我们将原始旋律和降低一个八度的旋律同时播放，创造出和声效果。

### **总结**
这个过程展示了如何通过编程生成音乐，核心思想是将音符表示为数学函数，组合它们以创建旋律和和弦。我们通过使用 `play` 函数将音符写入 `.wav` 文件，生成可以被计算机播放的音频。

---

### 以下是更细致的补充讲解：

```python
from wave import open
from struct import Struct
from math import floor

frame_rate = 11025

def encode(x):
    """Encode float x between -1 and 1 as two bytes.
    (See https://docs.python.org/3/library/struct.html)
    """
    i = int(16384 * x)
    return Struct('h').pack(i)

def play(sampler, name='song.wav', seconds=2):
    """Write the output of a sampler function as a wav file.
    (See https://docs.python.org/3/library/wave.html)
    """
    out = open(name, 'wb')
    out.setnchannels(1)
    out.setsampwidth(2)
    out.setframerate(frame_rate)
    t = 0
    while t < seconds * frame_rate:
        sample = sampler(t)
        out.writeframes(encode(sample))
        t = t + 1
    out.close()

def tri(frequency, amplitude=0.3):
    """A continuous triangle wave."""
    period = frame_rate // frequency
    def sampler(t):
        saw_wave = t / period - floor(t / period + 0.5)
        tri_wave = 2 * abs(2 * saw_wave) - 1
        return amplitude * tri_wave
    return sampler

c_freq, e_freq, g_freq = 261.63, 329.63, 392.00

play(tri(e_freq))

def note(f, start, end, fade=.01):
    """Play f for a fixed duration."""
    def sampler(t):
        seconds = t / frame_rate
        if seconds < start:
            return 0
        elif seconds > end:
            return 0
        elif seconds < start + fade:
            return (seconds - start) / fade * f(t)
        elif seconds > end - fade:
            return (end - seconds) / fade * f(t)
        else:
            return f(t)
    return sampler

play(note(tri(e_freq), 1, 1.5))

def both(f, g):
    return lambda t: f(t) + g(t)

c = tri(c_freq)
e = tri(e_freq)
g = tri(g_freq)
low_g = tri(g_freq / 2)

play(both(note(e, 0, 1/8), note(low_g, 1/8, 3/8)))

play(both(note(c, 0, 1), both(note(e, 0, 1), note(g, 0, 1))))

def mario(c, e, g, low_g):
    z = 0
    song = note(e, z, z + 1/8)
    z += 1/8
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(c, z, z + 1/8))
    z += 1/8
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(g, z, z + 1/4))
    z += 1/2
    song = both(song, note(low_g, z, z + 1/4))
    return song

def mario_at(octave):
    c = tri(octave * c_freq)
    e = tri(octave * e_freq)
    g = tri(octave * g_freq)
    low_g = tri(octave * g_freq / 2)
    return mario(c, e, g, low_g)

play(both(mario_at(1), mario_at(1/2)))
```

## 背景知识

这段代码实现了一个用Python生成并播放简单声音的系统，特别是通过编码音频数据为WAV文件并生成不同的波形和音符。要理解这段代码，我们需要先了解以下几个背景知识：

### 1. 数字音频的基本原理
数字音频是将声音信号的连续波形表示为一系列离散的数字样本。音频信号的波形可以用频率（每秒振动的次数）和振幅（振动的强度）来表示。数字音频通常由一系列样本（每个时刻的音频信号的值）组成，这些样本以固定的采样率记录。

- **采样率**：指每秒钟采集多少个样本点。代码中的`frame_rate = 11025`表示每秒采样11025个样本点，这个值是音频的“帧率”。
- **量化**：将连续信号的振幅离散化为数字形式。为了表示音频样本，每个样本会被编码为一个特定的数据格式（如16位整数）。
  

在这里，代码使用16位的音频格式（每个音频样本用两个字节表示），并生成WAV文件格式保存和播放这些样本。

### 2. WAV文件格式
WAV文件是一种常用的音频文件格式，它记录原始的、未压缩的数字音频。WAV文件中每个音频样本的大小和采样率可以根据需要调整。这个代码使用Python的`wave`库来处理WAV文件的写入：

- `open(name, 'wb')` 打开一个WAV文件准备写入。
- `setnchannels(1)` 设置音频的声道数量（1表示单声道）。
- `setsampwidth(2)` 设置每个样本的字节数，这里每个样本是16位的，所以是2字节。
- `setframerate(frame_rate)` 设置音频的帧率（即采样率）。

在写入音频数据时，代码生成一个浮点数波形（-1到1之间的值），并将其转换为整数形式（通过`encode`函数），然后将这些样本写入WAV文件。

### 3. 波形
声音波形是音频信号的表现形式，可以是正弦波、方波、锯齿波、三角波等不同类型。每种波形都有不同的声音特性。

- **三角波**（Triangle wave）：这是一种连续波形，在上升和下降之间以线性方式切换。三角波的频率决定了音高，振幅决定了声音的强度。在代码中，`tri`函数生成了一个三角波。
- **周期**：波形的周期是它重复的时间间隔，代码通过`period = frame_rate // frequency`来计算波形的周期。

### 4. 频率与音符
频率（Hz，赫兹）决定了音符的音高。代码定义了一些常见的音符频率，例如：
- `c_freq = 261.63`（C音，通常为中音C）
- `e_freq = 329.63`（E音）
- `g_freq = 392.00`（G音）

这些频率用于生成不同音高的音符。

### 5. 函数式编程与采样
代码大量使用了**高阶函数**，即函数返回另一个函数。特别是生成波形的`sampler`函数。这种方法允许动态生成音频采样函数，并且能够基于时间`t`提供每个时刻的波形值。

例如：
- `tri(frequency)` 返回一个生成三角波的采样函数，采样函数根据输入的时间点`t`计算波形值。
- `note`函数可以用来控制音符的播放时间段，设置渐入和渐出效果。

### 6. 组合音符与和弦
`both`函数允许将两个波形（采样器）组合在一起，生成和弦效果。例如：
```python
play(both(note(c, 0, 1), both(note(e, 0, 1), note(g, 0, 1))))
```
这个例子组合了C、E和G音符，形成了一个和弦。

### 7. Mario主题的实现
代码中的`mario`函数生成了一段类似“超级马里奥”的主题音乐片段。它通过组合不同频率的音符，设置音符的开始和结束时间，模拟出这个经典的音乐片段。

## 代码讲解

```python
from wave import open
from struct import Struct
from math import floor

frame_rate = 11025

def encode(x):
    """Encode float x between -1 and 1 as two bytes.
    (See https://docs.python.org/3/library/struct.html)
    """
    i = int(16384 * x)
    return Struct('h').pack(i)

def play(sampler, name='song.wav', seconds=2):
    """Write the output of a sampler function as a wav file.
    (See https://docs.python.org/3/library/wave.html)
    """
    out = open(name, 'wb')
    out.setnchannels(1)
    out.setsampwidth(2)
    out.setframerate(frame_rate)
    t = 0
    while t < seconds * frame_rate:
        sample = sampler(t)
        out.writeframes(encode(sample))
        t = t + 1
    out.close()
```

这部分我们要重点理解几个关键概念：高阶函数、音频采样、音频编码，以及 WAV 文件的生成过程。接下来，我们分模块细致讲解：

### 1. 音频采样率与帧率
```python
frame_rate = 11025
```
- **帧率 (Frame Rate)** 或者 **采样率 (Sampling Rate)** 是音频文件的一个核心属性，它指的是每秒钟采集多少个样本点。这里设定的采样率是 11025 Hz，意味着每秒采集 11025 个音频样本。这种采样率相对较低，通常用于低质量音频文件（CD音频的标准采样率为 44100 Hz），但对于简单的音效或音乐是足够的。

### 2. 高阶函数与采样器
```python
def play(sampler, name='song.wav', seconds=2):
    ...
    sample = sampler(t)
    ...
```
- **高阶函数**：高阶函数是指函数可以作为参数传递给另一个函数，或从函数中返回。这里的 `sampler` 就是一个高阶函数，它接收时间参数 `t`，并返回对应时刻的音频采样值。
  
- **采样器（sampler）**：`sampler(t)` 实际上是一个函数，这个函数会根据时间 `t` 生成一个音频样本值。每当代码需要生成一个新的音频样本时，就会调用 `sampler(t)` 来计算该时刻的音频波形值。这种设计模式允许我们使用不同的函数来生成不同的波形或音频效果。

### 3. 音频编码
```python
def encode(x):
    """Encode float x between -1 and 1 as two bytes."""
    i = int(16384 * x)
    return Struct('h').pack(i)
```
- **音频信号的量化**：音频信号在计算机中以离散的数值来表示，而这段代码的核心功能之一就是将音频信号从浮点数（范围在-1到1之间）转换为整数，并将其编码成字节。

  具体地，`16384` 是一个缩放因子，将浮点数扩展为整型数值范围。将信号从浮点值（-1 到 1）转换为整数范围（-16384 到 16384），这确保音频信号在二进制存储中能够以合适的分辨率表现。

- **结构打包 (Struct)**：`Struct('h')` 创建了一个用于打包数据的结构，`'h'` 表示 16 位有符号整数（short）。`pack(i)` 将整数 `i` 编码为两个字节（16 位），用于存储或传输音频数据。

  这种编码方式是为了符合 WAV 文件格式中对音频数据的要求，即每个音频样本由 2 个字节（16 位）表示。

### 4. 播放与写入 WAV 文件
```python
def play(sampler, name='song.wav', seconds=2):
    out = open(name, 'wb')
    out.setnchannels(1)
    out.setsampwidth(2)
    out.setframerate(frame_rate)
    ...
    t = 0
    while t < seconds * frame_rate:
        sample = sampler(t)
        out.writeframes(encode(sample))
        t = t + 1
    out.close()
```
**文件打开与设置**

- **打开文件**：`open(name, 'wb')` 使用 `wave` 模块打开一个新的 WAV 文件。'wb' 模式表示以二进制写入模式打开，这样可以写入音频数据。
  
- **设置 WAV 文件的属性**：
  - `setnchannels(1)` 设置声道数为 1，表示单声道音频。
  - `setsampwidth(2)` 设置每个音频样本的字节数为 2（16 位），符合 WAV 文件的标准。
  - `setframerate(frame_rate)` 设置帧率，即音频的采样率，定义为 11025 Hz。

**生成音频数据**

- **采样过程**：`while t < seconds * frame_rate:` 这段代码使用一个循环，通过不断调用 `sampler(t)` 来生成音频样本。每个时间点 `t` 都会生成一个音频值，`t` 的递增步长为 1，表示每帧音频的时间点。
  
  例如，对于 2 秒的音频，帧率为 11025，每秒生成 11025 个采样点，2 秒共生成 22050 个采样点。每次调用 `sampler(t)` 生成的音频样本都会通过 `encode()` 函数转换成字节数据。

- **音频写入**：`out.writeframes(encode(sample))` 将编码后的样本数据写入到 WAV 文件中。每个样本都被转换成 16 位的字节格式并逐帧写入文件，直到生成完整的音频文件。

**文件关闭**

- **关闭文件**：`out.close()` 关闭文件，确保数据正确写入并释放文件资源。

### 5. 采样器与声音生成的关系
```python
sample = sampler(t)
```
- `sampler(t)` 函数决定了在时间 `t` 时刻生成的音频值，它通常基于某种波形生成策略（例如三角波、正弦波等）。通过使用不同的 `sampler` 函数，代码可以生成不同的声音效果。

示例：**三角波的生成**

稍后的 `tri` 函数就是一个采样器，它会根据时间 `t` 生成一个三角波。三角波是一种线性上升和下降的波形，这种波形生成的声音会有一种“机械”或“复古”的音色。

```python
def tri(frequency, amplitude=0.3):
    """A continuous triangle wave."""
    period = frame_rate // frequency
    def sampler(t):
        saw_wave = t / period - floor(t / period + 0.5)
        tri_wave = 2 * abs(2 * saw_wave) - 1
        return amplitude * tri_wave
    return sampler

c_freq, e_freq, g_freq = 261.63, 329.63, 392.00

play(tri(e_freq))

def note(f, start, end, fade=.01):
    """Play f for a fixed duration."""
    def sampler(t):
        seconds = t / frame_rate
        if seconds < start:
            return 0
        elif seconds > end:
            return 0
        elif seconds < start + fade:
            return (seconds - start) / fade * f(t)
        elif seconds > end - fade:
            return (end - seconds) / fade * f(t)
        else:
            return f(t)
    return sampler

play(note(tri(e_freq), 1, 1.5))

def both(f, g):
    return lambda t: f(t) + g(t)
```

这一部分代码主要处理了声音的波形生成、音符的控制（包括音符的开始与结束、淡入淡出效果），以及将不同的声音波形组合在一起形成和声。我们将逐步解析每一部分的细节，包括三角波生成、音符控制、以及高阶函数的使用。

### 1. 三角波生成
```python
def tri(frequency, amplitude=0.3):
    """A continuous triangle wave."""
    period = frame_rate // frequency
    def sampler(t):
        saw_wave = t / period - floor(t / period + 0.5)
        tri_wave = 2 * abs(2 * saw_wave) - 1
        return amplitude * tri_wave
    return sampler
```

- **三角波**（Triangle wave）是一种周期性波形，它以线性方式在正负最大值之间来回切换。相比正弦波，三角波听起来更加锐利，具有一种机械感，因为它的振幅是线性变化的，而不是像正弦波那样平滑。

**具体实现**

1. **周期计算**：
   ```python
   period = frame_rate // frequency
   ```
   - `period` 是三角波的周期，表示一个完整的波形所需要的采样点数。通过帧率 `frame_rate` 除以频率 `frequency`，我们可以计算出每个波形的周期长度。
   - 例如，如果帧率是 11025 Hz，频率是 261.63 Hz（对应C音），则周期 `period` = 11025 // 261.63 ≈ 42 个采样点。

2. **生成采样器**：
   ```python
   def sampler(t):
       saw_wave = t / period - floor(t / period + 0.5)
       tri_wave = 2 * abs(2 * saw_wave) - 1
       return amplitude * tri_wave
   ```
   - **saw_wave**：这是生成三角波的第一步，它本质上是一个锯齿波。锯齿波的特点是从 -0.5 到 0.5 线性增长。`saw_wave = t / period - floor(t / period + 0.5)` 会产生一个周期性的锯齿波。
   
   - **tri_wave**：三角波是通过对锯齿波的绝对值变换得到的。`abs(2 * saw_wave)` 将锯齿波变成一个在 0 到 1 之间线性振荡的波形。之后，通过`2 * abs(2 * saw_wave) - 1` 将这个波形变换到 -1 到 1 的范围内，得到三角波。

   - **振幅控制**：`amplitude * tri_wave` 最终会调整三角波的振幅，默认值为0.3，这意味着输出的波形将在 -0.3 和 0.3 之间振荡。

**示例调用**

```python
c_freq, e_freq, g_freq = 261.63, 329.63, 392.00

play(tri(e_freq))
```
这里调用 `tri(e_freq)` 生成了一个以 E 音（329.63 Hz）为频率的三角波，并播放它。

### 2. 控制音符的开始、结束和渐入渐出
```python
def note(f, start, end, fade=.01):
    """Play f for a fixed duration."""
    def sampler(t):
        seconds = t / frame_rate
        if seconds < start:
            return 0
        elif seconds > end:
            return 0
        elif seconds < start + fade:
            return (seconds - start) / fade * f(t)
        elif seconds > end - fade:
            return (end - seconds) / fade * f(t)
        else:
            return f(t)
    return sampler
```

**音符的控制**

`note` 函数允许我们定义一个音符在指定的时间范围内播放，并添加渐入渐出的效果。

1. **音符开始和结束的时间控制**：
   - **start 和 end**：`start` 定义了音符的起始时间，`end` 定义了音符的结束时间。采样器在这段时间内会输出有效的音频样本值，在这段时间之外输出0，这意味着音符在这段时间内才会播放。
   
   - **渐入和渐出**：`fade` 参数控制音符的渐入和渐出效果，默认值是 0.01 秒。音符在播放的最初和结束的短时间内，音量会从 0 逐渐变大（渐入），然后逐渐变小（渐出），使声音更加平滑过渡。

2. **具体逻辑**：
   - 如果当前的 `seconds` 小于 `start` 或者大于 `end`，则返回 0，表示此时音符没有声音。
   - 如果当前时间在 `start` 和 `start + fade` 之间，则音量逐渐从 0 增加到音符的最大值（通过 `f(t)` 来生成音符的实际波形）。
   - 同理，在 `end - fade` 到 `end` 之间，音量逐渐减小。
   - 在这两个区间之外的时间，直接返回 `f(t)`，即按正常振幅播放音符。

**示例调用**

```python
play(note(tri(e_freq), 1, 1.5))
```
这段代码会播放一个 E 音（329.63 Hz）的三角波，起始时间为 1 秒，结束时间为 1.5 秒，并在前后 0.01 秒内加入渐入渐出效果。

### 3. 组合波形
```python
def both(f, g):
    return lambda t: f(t) + g(t)
```

**组合函数**

- `both(f, g)` 允许我们将两个波形组合在一起。它返回一个新的采样器函数，这个采样器会在每个时间 `t` 上，计算 `f(t)` 和 `g(t)` 的值并将它们相加。
  
- **和声效果**：通过将两个不同频率的波形组合，可以产生和声效果。例如，可以同时播放 C 和 E 音符，生成一个简单的和弦。

**示例调用**

```python
c = tri(c_freq)
e = tri(e_freq)
g = tri(g_freq)
play(both(c, e))
```
这里 `both(c, e)` 将 C 和 E 音符组合在一起，并同时播放它们，形成一个和弦。

```python
c = tri(c_freq)
e = tri(e_freq)
g = tri(g_freq)
low_g = tri(g_freq / 2)

play(both(note(e, 0, 1/8), note(low_g, 1/8, 3/8)))

play(both(note(c, 0, 1), both(note(e, 0, 1), note(g, 0, 1))))

def mario(c, e, g, low_g):
    z = 0
    song = note(e, z, z + 1/8)
    z += 1/8
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(c, z, z + 1/8))
    z += 1/8
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(g, z, z + 1/4))
    z += 1/2
    song = both(song, note(low_g, z, z + 1/4))
    return song

def mario_at(octave):
    c = tri(octave * c_freq)
    e = tri(octave * e_freq)
    g = tri(octave * g_freq)
    low_g = tri(octave * g_freq / 2)
    return mario(c, e, g, low_g)

play(both(mario_at(1), mario_at(1/2)))
```

这部分代码进一步展示了如何通过组合不同频率的波形和音符来创建复杂的音乐效果，尤其是经典的“马里奥”音乐片段。以下是详细讲解：

### 1. 简单音符的组合
```python
c = tri(c_freq)
e = tri(e_freq)
g = tri(g_freq)
low_g = tri(g_freq / 2)

play(both(note(e, 0, 1/8), note(low_g, 1/8, 3/8)))
```

**三角波生成**

首先，代码为每个音符创建对应的三角波：
- `c = tri(c_freq)` 生成 C 音符（三角波），频率为 261.63 Hz。
- `e = tri(e_freq)` 生成 E 音符，频率为 329.63 Hz。
- `g = tri(g_freq)` 生成 G 音符，频率为 392.00 Hz。
- `low_g = tri(g_freq / 2)` 生成 G 的低八度音符，频率为 196.00 Hz（G 频率的一半）。

**播放简单的音符组合**

```python
play(both(note(e, 0, 1/8), note(low_g, 1/8, 3/8)))
```
这段代码通过 `both` 函数将两个音符组合在一起：
- `note(e, 0, 1/8)` 播放 E 音符，从第 0 秒到 1/8 秒，时长为 0.125 秒。
- `note(low_g, 1/8, 3/8)` 播放低八度 G 音符，从 1/8 秒到 3/8 秒，时长为 0.25 秒。

`both` 将这两个音符组合并同时播放，使得 E 音符先响起，之后 G 低八度音符开始响起。

### 2. 和弦的组合
```python
play(both(note(c, 0, 1), both(note(e, 0, 1), note(g, 0, 1))))
```

**组合和弦**

这段代码创建了一个和弦，由 C、E 和 G 三个音符同时演奏，时长为 1 秒：
- `note(c, 0, 1)` 播放 C 音符，从 0 秒开始，持续 1 秒。
- `both(note(e, 0, 1), note(g, 0, 1))` 将 E 和 G 音符组合起来，两个音符同时从 0 秒开始，持续 1 秒。
- `both(note(c, 0, 1), ...)` 将 C 音符与 E 和 G 的组合一起播放，形成 C 大三和弦。

这个三和弦的组合展示了如何将不同的音符组合在一起，产生和谐的音乐效果。

### 3. “马里奥”主题音乐
```python
def mario(c, e, g, low_g):
    z = 0
    song = note(e, z, z + 1/8)
    z += 1/8
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(c, z, z + 1/8))
    z += 1/8
    song = both(song, note(e, z, z + 1/8))
    z += 1/4
    song = both(song, note(g, z, z + 1/4))
    z += 1/2
    song = both(song, note(low_g, z, z + 1/4))
    return song
```

**逐步构建音乐**

这段代码逐步构建了一个类似于“马里奥”主题的音乐片段，使用 `note` 函数定义不同音符在不同时间段的播放：

1. `z = 0` 初始化时间计数器 `z`，用于跟踪每个音符的起始时间。
2. 每个 `note` 函数生成一个在特定时间段内播放的音符：
   - `note(e, z, z + 1/8)` 播放 E 音符，从 `z` 秒开始，持续 1/8 秒。
   - `both(song, note(e, z, z + 1/8))` 将之前的 `song` 组合上另一个 E 音符。

3. `z += 1/8` 更新时间计数器，确保下一个音符在正确的时间开始播放。

最终通过不断调用 `both` 函数，将多个音符逐步组合起来，形成了完整的“马里奥”音乐片段。

### 4. 不同八度的马里奥音乐
```python
def mario_at(octave):
    c = tri(octave * c_freq)
    e = tri(octave * e_freq)
    g = tri(octave * g_freq)
    low_g = tri(octave * g_freq / 2)
    return mario(c, e, g, low_g)

play(both(mario_at(1), mario_at(1/2)))
```

**八度变化**

`mario_at` 函数允许我们通过调整音符的频率来生成不同八度的音乐：
- `octave * c_freq` 通过改变 `octave` 参数，调整音符的频率。例如，`octave=1` 生成原本的频率，`octave=1/2` 则生成低八度的频率。

**同时播放两个八度**

`play(both(mario_at(1), mario_at(1/2)))` 将两个不同八度的马里奥主题音乐组合在一起同时播放：
- `mario_at(1)` 生成正常八度的马里奥音乐。
- `mario_at(1/2)` 生成低八度的马里奥音乐。

这样，两个八度的马里奥音乐同时播放，产生丰富的音效。

这一部分的代码展示了如何通过音符、和弦、以及八度变化来创建复杂的音乐效果，特别是通过 `note` 函数控制音符的时间长度和播放顺序，再通过 `both` 函数将多个音符组合在一起。整个代码结构灵活且模块化，通过高阶函数的应用，用户可以轻松生成不同风格的音乐或音效，甚至像“马里奥”这样的经典片段。

## 总结

### 1. **数字音频的基础**

代码通过生成和处理数字音频信号，来模拟声音。它的核心是将连续的声音波形离散化为数字样本，并以固定的采样率进行存储和播放。

- **采样率**：`frame_rate` 设置为 11025 Hz，表示每秒采集 11025 个音频样本，这决定了音频的清晰度。
- **量化**：通过 `encode` 函数，浮点形式的音频信号被转换为 16 位整数，这样可以符合 WAV 文件的要求，并以高分辨率存储音频数据。

### 2. **WAV 文件生成**

代码使用 `wave` 模块生成 WAV 格式音频文件，WAV 是一种常见的无压缩音频格式。

- **文件格式设置**：通过 `setnchannels(1)` 设置单声道，`setsampwidth(2)` 设置样本宽度为 16 位，`setframerate(frame_rate)` 设置帧率（采样率）为 11025 Hz。
- **数据写入**：音频样本被逐帧生成并通过 `writeframes` 写入文件，最终生成 WAV 格式的音频。

### 3. **高阶函数与采样器**

代码大量使用了高阶函数，尤其是在音频采样器的实现中。采样器函数根据时间 `t` 返回每个时间点的音频样本值，并通过高阶函数 `play` 实现不同波形的声音生成。

- **波形生成器**：`tri` 函数生成了一个三角波形，基于时间计算其波形值。这种设计模式使得代码可以灵活定义不同的波形，例如三角波、正弦波等。
- **音符控制**：`note` 函数允许音符在特定时间段内播放，并且支持淡入和淡出效果。通过使用不同的采样器，代码能够精确控制每个音符的时间范围。

### 4. **波形组合与和弦**

- **组合波形**：通过 `both` 函数，代码将两个不同的波形组合在一起，使得多个音符可以同时播放，产生和弦效果。这种组合函数的使用让代码能够轻松实现复杂的和声。
- **和弦播放**：例如，通过组合 C、E、G 音符，代码创建了一个大三和弦。

### 5. **马里奥主题音乐**

- **逐步生成音乐**：代码通过 `note` 函数控制不同音符的开始和结束时间，并通过 `both` 函数组合多个音符，逐步生成类似“马里奥”主题的音乐片段。
- **八度变化**：`mario_at` 函数允许生成不同八度的马里奥音乐，并且通过 `both` 函数将不同八度的音乐组合在一起同时播放，产生丰富的音效。

### 6. **音乐生成与播放**

- **时间控制**：`note` 函数能够精确控制音符的时长和淡入淡出，使得生成的音乐片段更加流畅和自然。
- **多层次音效**：通过组合多个音符和八度变化，代码生成了复杂的音效，展示了如何用简单的波形组合和时间控制，生成具有层次感的音乐。

整个代码展示了从数字音频信号生成、编码、存储、到播放的完整过程，并通过高阶函数、波形生成、和弦组合、音符时间控制等技巧，构建了一个灵活的音频生成框架。这个框架允许你通过简单的函数组合，生成复杂的音效或音乐片段，例如经典的马里奥主题音乐。这段代码展示了音频处理的基础，同时也提供了探索更复杂音效的思路。