---
layout: page
title: L06 Design
permalink: /L06
description: "Lecture 6. Design"
nav_order: 6








---

# Lecture 6. Design

### Announcements

**期中考试一**将于**周一**举行。如果由于时间冲突或考试时间处于夜间需要调整考试时间，请在**本周四**之前填写**替代时间申请表**。考试期间需要**录制屏幕和头部**，确保你独立完成考试。可选择使用Zoom、Loom或手机录制。请尽早**练习录制2小时视频**，以确保考试当天录制过程顺利。

如果需要**申请免除监考政策**，请在**本周四**之前提交申请。**周五**我们将提供一次**练习考试**，时间为**下午1点到2点**和**晚上7点到8点**，之后48小时内可随时完成练习。练习考试将使用与正式考试相同的软件，建议录制自己参加练习考试的过程，确保一切正常。

你可以创建一张**双面的复习笔记**，也可以使用草稿纸。若选择将笔记电子存储，唯一允许的方式是使用Google Doc，并确保不与他人共享，还需提供编辑权限给 `csixton@berkeley.edu`。不会编辑内容，但需确保我们能查看。

**HKN（Ada Kappa Nu）**学生组织计划在**周六下午1点到4点（太平洋时间）**举办一次复习会议，详情将在Piazza上发布。

根据**第二周的反馈**，所有实验的截止时间调整为**周二**，包括实验二，其截止时间为本周二。**Hog项目**的第一阶段也将于本周二截止，需提交**第5题**，但不包括第6题。提交后将获得**检查点1分**，该分数不高，但仍应完成。提前提交可额外获得1分，建议在**周四**之前完成。

我们将在今天晚上**7点到9点**举办**项目派对**，并有大量**预约时间**可供选择。每天晚上10点会发布次日的新预约时间。如果不想等待排队，建议预约一个确定的时间。此外，你也可以加入**办公室时间队列**，但并非所有时间都开放，具体开放时间可在**办公室时间页面**查看。

最近收到很多**私人Piazza帖子**，由于数量较多，回复可能会有延迟，但我们会确保所有问题都得到解答。

最后，**Hog图形用户界面（GUI）**问题已修复。此前版本不支持同一玩家连续两次行动，这是本学期的新规则。若要使用更新的GUI，请重新下载项目文件，保留旧工作并替换GUI文件。

**讨论二**及相关教程将在**周三**举行，请务必**先参加导向会议**，然后再参加教程，否则教程将难以理解。周五还有一次**考试准备会议**，所有的Zoom链接和讲座问答环节链接已提供。本周没有新内容，因为需要专注于**完成项目**并准备**期中考试**。





### 1. 导向与教程安排
本周三，务必要参加课程的**导向会议**，然后再参加教程部分。因为如果没有参加导向，教程部分将难以理解。本周五还有一次**考试准备会议**，请注意查看提供的Zoom链接，这些链接也包括了与这次讲座及周五讲座相关的**问答环节**。

### 2. 本周课程安排与学习重点
本周课程没有新的内容，因为同学们需要花时间**完成项目**并准备期中考试。今天的课程将简要讨论如何设计一个**大型程序**，并通过一个扩展的示例进行讲解。周五的课程主要是复习和考试准备，将涵盖一些**往年考试题目**及其解题思路。

### 3. 抽象概念——函数抽象
**函数抽象**指的是将某个计算过程赋予一个名字，然后在后续使用时只需调用该名字，而无需关心其具体的实现细节。

#### 示例：`square` 和 `sum_squares` 函数
- `square` 函数用于计算数字的平方，`sum_squares` 函数则调用 `square`。
- **关键问题**：`sum_squares` 需要了解 `square` 的哪些信息才能正确调用它？

##### 回答：
1. **是否需要知道 `square` 接受一个参数**？  
   是的，否则无法正确调用。
2. **是否需要知道 `square` 的内在名字是 `square`**？  
   不需要，内在名字只为人类检查，任何绑定到当前环境中 `square` 名字的函数都可以被正确调用。
3. **是否需要知道 `square` 的行为，即它计算一个数的平方**？  
   是的，正确使用函数抽象时，必须知道它的行为。
4. **是否需要知道 `square` 是通过 `mull` 函数实现平方计算的**？  
   不需要，它可以通过任何方式计算平方，只要实现结果正确。

我们可以通过内置的 `pow` 函数来计算平方，或者采用其它方法，只要 `sum_squares` 依赖的 `square` 函数行为不变，就不会影响其正确性。

### 4. 选择命名的建议
命名对人类理解代码至关重要，但对程序的**正确性**没有直接影响。好的命名可以显著提升程序的可读性和可维护性。

#### 命名规则：
1. **名称应传达其值的意义或用途**，便于理解为何创建该值以及它的用途。
2. **值的类型（如数字、字符串）最好在函数的注释中说明**，而不是体现在变量名中。
3. **函数命名**应反映其**效果**（如打印）、**行为**（如三倍化）或**返回值**（如绝对值）。

#### 命名建议：
- 避免将布尔变量命名为 `trueFalse`，而应根据其意义命名，如 `playerRolledOne`（表示游戏中玩家掷出了1）。
- 避免使用单个字母如 `d`，应使用有意义的名称如 `dice`。
- 函数命名应基于其功能，而不是调用者。举例来说，**不要**将函数命名为 `playHelper`，而应命名为 `takeTurn`，因为该函数的实际作用是模拟一次回合。
- 避免用类型来命名变量，如 `myInt`，应使用更具描述性的名称，如 `numberOfRolls`。

#### 不推荐的命名：
- 某些字母如 `l`、`I` 和 `O` 容易与数字 `1` 和 `0` 混淆，建议使用 `k`、`r`、`m` 等字母作为单字符变量。

### 5. 如何决定值是否需要命名
不是所有中间值都需要命名，但如果同一个复杂的表达式在代码中多次出现，最好赋予它一个名称，这样便于维护。

#### 示例：
如果代码中多次计算 `sqrt(a^2 + b^2)`，建议给它命名为 `hypotenuse`，这样如果计算逻辑需要修改，只需改动一个地方。

此外，尽量避免编写**过于复杂的表达式**，即便计算机能够处理复杂代码，过于复杂的表达式对人类理解不利。





### 命名技巧

在代码命名方面，有一些额外的建议：
- **长名称**是可以接受的，特别是在帮助解释代码含义时。如果一个赋值语句是用来计算某个学生的平均年龄，并命名为`average_age`，这是一种清晰表达代码意图的好方法。相比之下，使用注释并配以更复杂的表达式，不如直接通过清晰的命名来解释代码更好。
- **短名称**也可以接受，尤其是当它们代表通用量时。例如，表示实数的绝对值、计数器或某些数学操作的参数，甚至是封装某个通用函数的情况。但需要了解一些常见的命名**约定**，这些约定在多种编程语言中都有应用。某些字母常用于表示整数，某些字母表示实数，另一些字母则表示函数。

虽然这些约定并非必须遵守，但它们有助于使代码更具可读性。如果你选择遵循这些约定，其他程序员会更容易理解你的代码。然而，编写程序也是一种创造性行为，关键在于代码对他人具有可读性。

### 高阶函数的作用

学生常常会问，**高阶函数**的意义是什么。例如，`make_adder` 函数很有趣，但为什么不直接加上 `x` 和 `y`，而要构建一个高阶函数呢？为了解释这个问题，我们构建了一个稍长的示例，展示为何在程序的早期定义多个函数，并在程序的最后阶段才处理这些函数，可能会更有利。

### 示例：生成声音文件

我们将使用Python来生成一个**WAV文件**，这是编码声音的标准格式。虽然WAV文件现在很少使用，因为它占用大量空间，但它的格式非常简单，没有压缩，容易生成。

WAV文件的作用是**直接编码声音波形的样本**。声音是波动的，波形在任意时刻都有振幅，而**采样**的作用是通过记录波形在特定时刻的高度（振幅）来将其数字化。为了生成逼真的声音，我们将在每分钟采集**11000个样本**，以获得足够精确的波形近似。

通常，这些波形是通过**录制真实世界中的声音**产生的，但我们也可以通过**数学函数**生成波形。在电子音乐中，常见的波形有**正弦波**、**方波**、**三角波**和**锯齿波**。在这个例子中，我们选择**三角波**，因为它的音质比其他几种波形更好。

### 生成WAV文件的Python代码

我们使用了Python中的一些内置模块来构建WAV文件：
- **wave模块**：处理WAV文件。
- **struct模块**：将整数编码为WAV文件所需的格式。
- **floor函数**：将一个数值向下取整为不大于该值的最大整数。

首先，我们设置一个**帧率**（采样率），即每秒钟我们记录多少个波形的采样值，然后通过采样函数生成波形。接下来，我们将这些采样值写入WAV文件。

代码片段如下：
```python
import wave
import struct
import math

def write_wave_file(filename, length_in_seconds, sampler):
    frame_rate = 22050  # 采样率
    n_frames = int(length_in_seconds * frame_rate)
    
    # 打开WAV文件进行写入
    with wave.open(filename, 'w') as wave_file:
        wave_file.setnchannels(1)  # 单声道
        wave_file.setsampwidth(2)  # 每个样本2字节
        wave_file.setframerate(frame_rate)
        
        # 写入每个帧的采样值
        for i in range(n_frames):
            t = i / frame_rate  # 当前时刻
            sample = sampler(t)  # 采样值（-1到1之间）
            sample_value = int(32767 * sample)  # 将采样值转换为16位整数
            wave_file.writeframesraw(struct.pack('<h', sample_value))  # 写入WAV文件

# 示例：生成1秒长的三角波
def triangle_wave(t):
    period = 1 / 440  # 440Hz的周期
    value = (2 / math.pi) * math.asin(math.sin(2 * math.pi * t / period))
    return value

write_wave_file('triangle_wave.wav', 1, triangle_wave)
```

#### 代码说明：
- **write_wave_file**：生成WAV文件的主函数，接受文件名、音频长度和采样函数作为参数。
- **triangle_wave**：生成一个440Hz的三角波，其值在-1到1之间变化。

在实际操作中，`sampler` 函数就是描述波形的函数，它根据时间 `t` 生成对应的采样值。





在生成声音文件的过程中，我们可以通过调用采样函数 `sampler` 来生成一系列的声音样本。具体来说，我们会在一个采样率下执行多次调用（如22,000次），每次调用时传入不同的时间 `t`，并将生成的样本值写入WAV文件。**采样函数**负责在给定时间 `t` 返回波形的值，这个值通常介于-1到1之间，表示波形在该时刻的振幅。

### 三角波的生成

为了生成一个三角波，我们需要了解两个关键参数：
1. **频率（frequency）**：决定了声音的音高。
2. **振幅（amplitude）**：决定了声音的音量。

有了频率和振幅后，我们可以计算出三角波的周期，即完成一个完整的三角形波形所需的时间步骤数。接着，可以通过构建一个锯齿波的函数，然后进行适当的数学变换，将其转换为三角波。

例如，对于音符C的标准频率是**261.63Hz**，这是乐器在现代调音中的一个基本事实。

### 三角波的实现代码示例

```python
import math

def triangle_wave(t, frequency, amplitude):
    period = 1 / frequency  # 计算周期
    saw_wave = (t / period) % 1  # 生成锯齿波
    triangle_value = 2 * abs(2 * saw_wave - 1) - 1  # 转换为三角波
    return amplitude * triangle_value
```

在这个例子中，`triangle_wave` 函数接受时间 `t`、频率 `frequency` 和振幅 `amplitude` 作为参数。它首先根据频率计算出周期，接着生成一个锯齿波，再通过数学运算将其转换为三角波。

### C音符的示例

接下来，我们通过打印出一系列采样值来展示三角波形的变化。在这里，我们从时间 `t = 0` 开始，不断递增 `t`，并调用 `triangle_wave` 函数来查看不同时间点的振幅值。

```python
t = 0
frequency = 261.63  # C音符的频率
amplitude = 0.3  # 振幅

while t < 100:
    print(triangle_wave(t, frequency, amplitude))
    t += 1
```

### 生成音符C的WAV文件

我们现在可以生成一个C音符的WAV文件，并播放它。首先通过`triangle_wave`函数生成对应的三角波，然后将其写入WAV文件中。

```python
write_wave_file('C_note.wav', 1, lambda t: triangle_wave(t, 261.63, 0.3))
```

这段代码会生成一个C音符的WAV文件，文件中存储了1秒长的C音符三角波形。生成后，可以使用操作系统的音频播放器播放该文件，听到该音符。

### 生成和弦

接下来，我们生成三个不同音符（C、E、G）的频率，并尝试同时播放C和E音符。这意味着我们需要定义一个新的采样函数，该函数会同时调用两个三角波函数（一个针对C音符，一个针对E音符），并将两者的结果相加。

```python
def combine_waves(f1, f2):
    return lambda t: f1(t) + f2(t)

c_wave = lambda t: triangle_wave(t, 261.63, 0.3)  # C音符
e_wave = lambda t: triangle_wave(t, 329.63, 0.3)  # E音符

combined_wave = combine_waves(c_wave, e_wave)

write_wave_file('C_E_chord.wav', 1, combined_wave)
```

通过这个方法，我们生成了一个C和E音符的和弦，听起来会比单个音符更丰富。

### 添加节奏

为了进一步丰富生成的声音，我们可以控制音符的播放时长。例如，通过只在指定的时间区间播放音符，可以为声音添加节奏。为此，我们定义一个函数来确保音符只在给定的时间范围内播放。

```python
def play_with_rhythm(sound, start, end, frame_rate):
    return lambda t: sound(t) if start <= t / frame_rate <= end else 0

# C音符在0秒到0.5秒之间播放
c_note_with_rhythm = play_with_rhythm(c_wave, 0, 0.5, 22050)

write_wave_file('C_with_rhythm.wav', 1, c_note_with_rhythm)
```

这段代码让C音符只在0到0.5秒内播放，形成一个四分音符。通过这种方法，我们可以创建具有节奏的旋律。

### 总结

通过使用Python中的数学函数和WAV文件处理模块，我们能够生成基本的音频文件。使用三角波和其他波形，结合函数的抽象，我们可以生成各种音符、和弦，并为其添加节奏。





在音乐生成的过程中，我们可以通过调整音符的开始时间、持续时间和渐入渐出的效果来使声音听起来更自然。之前的声音听起来有些生硬，我们可以通过为每个音符添加一个**渐入和渐出**效果来解决这个问题。

### 渐入和渐出的实现

为了解决音符开头和结尾听起来突兀的问题，我们可以在音符的开始和结束时加入一个短暂的**渐入（fade-in）**和**渐出（fade-out）**。例如，可以在音符的前0.1秒内逐渐增加音量，并在结束前的0.1秒内逐渐减小音量。

实现代码如下：

```python
def apply_fade(sound, start, end, frame_rate, fade_length=0.1):
    return lambda t: (
        sound(t) * min(1, (t / frame_rate - start) / fade_length) 
        if start <= t / frame_rate <= start + fade_length else
        sound(t) * min(1, (end - t / frame_rate) / fade_length) 
        if end - fade_length <= t / frame_rate <= end else
        sound(t) if start <= t / frame_rate <= end else 0
    )
```

这段代码会根据音符的开始和结束时间，为音符增加渐入和渐出的效果。`fade_length` 指定了渐入和渐出的时长，这里默认为0.1秒。

### 播放多个音符并添加节奏

假设我们要先播放一个C音符，然后在半秒后播放一个E音符，并为每个音符添加渐入和渐出的效果。

```python
c_wave = lambda t: triangle_wave(t, 261.63, 0.3)  # C音符
e_wave = lambda t: triangle_wave(t, 329.63, 0.3)  # E音符

# 为C音符和E音符添加渐入和渐出效果
c_with_fade = apply_fade(c_wave, 0, 0.5, 22050)
e_with_fade = apply_fade(e_wave, 0.5, 1.0, 22050)

# 将两个音符按时间顺序组合在一起
def combine_waves(*waves):
    return lambda t: sum(wave(t) for wave in waves)

song = combine_waves(c_with_fade, e_with_fade)
write_wave_file('C_E_with_fade.wav', 1, song)
```

在这段代码中，我们为C音符和E音符分别设置了0.5秒的播放时长，并通过`apply_fade`函数为它们添加了渐入和渐出的效果。然后使用`combine_waves`函数将两个音符组合在一起并生成WAV文件。

### 增加更多音符和节奏

接下来，我们可以继续为歌曲添加更多音符和节奏。例如，在每个音符之间留出停顿，并将这些音符按特定节奏进行排列。

```python
# 播放C音符作为四分音符，E音符作为八分音符
c_with_rhythm = play_with_rhythm(c_wave, 0, 0.25, 22050)  # 四分音符C
e_with_rhythm = play_with_rhythm(e_wave, 0.5, 0.75, 22050)  # 八分音符E

# 组合节奏
song_with_rhythm = combine_waves(c_with_rhythm, e_with_rhythm)
write_wave_file('song_with_rhythm.wav', 1, song_with_rhythm)
```

### 生成和弦

我们还可以创建和弦，通过同时播放不同频率的音符。例如，可以生成C、E和G的和弦（C大三和弦），并为它们添加渐入和渐出的效果。

```python
g_wave = lambda t: triangle_wave(t, 392.00, 0.3)  # G音符

# 同时播放C、E、G，形成C大三和弦
c_chord = combine_waves(
    apply_fade(c_wave, 0, 0.5, 22050),
    apply_fade(e_wave, 0.5, 1.0, 22050),
    apply_fade(g_wave, 1.0, 1.5, 22050)
)

write_wave_file('C_chord_with_fade.wav', 1.5, c_chord)
```

### 调整音高（八度变化）

我们可以通过改变音符的频率来生成不同的八度。例如，将频率乘以2可以提高一个八度，而将频率减半则可以降低一个八度。

```python
def adjust_octave(wave, factor):
    return lambda t: wave(t * factor)

# C音符在高八度和低八度的版本
c_high_octave = adjust_octave(c_wave, 2)  # 提高一个八度
c_low_octave = adjust_octave(c_wave, 0.5)  # 降低一个八度

# 组合两个八度的音符
song_with_octaves = combine_waves(c_high_octave, c_low_octave)
write_wave_file('C_octaves.wav', 1, song_with_octaves)
```

通过这种方式，我们可以在同一首曲子中同时播放高八度和低八度的C音符，产生丰富的音效。

### 生成完整乐曲

通过将这些函数和音符组合起来，我们可以生成更复杂的乐曲。将音符、和弦和节奏结合起来，通过不同的八度变化可以创造出不同的音乐效果。

例如，我们可以定义一个函数`play_mario_theme`，通过控制不同音符的播放顺序、时长和八度变化，来生成一个简单的“马里奥”主题曲。

```python
def play_mario_theme():
    # 定义马里奥主题曲的音符和节奏
    c = apply_fade(triangle_wave, 0, 0.25, 22050)
    e = apply_fade(triangle_wave, 0.25, 0.5, 22050)
    g = apply_fade(triangle_wave, 0.5, 0.75, 22050)
    
    # 合成乐曲
    song = combine_waves(c, e, g)
    return song

# 播放马里奥主题曲
write_wave_file('mario_theme.wav', 2, play_mario_theme())
```

通过这些方法，我们可以使用编程来生成音乐，不仅能够控制单个音符，还可以实现和弦、节奏和音高的变化，从而创造出丰富的音乐作品。