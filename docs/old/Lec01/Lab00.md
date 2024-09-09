---
layout: page
title: Lab 0. Workflow and Python Basics
permalink: /Lab00/
nav_order: 0
parent: Lecture 1. Computer Science


---

# Lab 0. Workflow and Python Basics



> 安装配置也可参考文档 [1]([https://github.com/SFUMECJF/cs61b-study-guide/blob/main/A%20Guide%20For%20CS%2061A_%20Structure%20and%20Interpretatiof%20Computer%20Programs.pdf) / [2](https://docs.google.com/document/d/1pceaNK3_1mcFOPtK47YKqDl45u8kWCzayuVxP9mrWZg/edit#heading=h.jyajdx9seiwa)

> 官网测试代码后加```--local```进行本地测试。

> [关于 ok ](#使用-ok-测试)

---

## 开始
下载 `lab00.zip`，解压后会发现实验的起始文件和一个 `Ok` 自动评分程序。

## 简介
本实验将指导你如何在自己的电脑上完成 CS 61A 的作业，并介绍 Python 的基础知识。本实验虽然看起来很长，但主要是设置和学习使用本课程的基本工具。可能现在有点难，但随着课程深入会逐渐习惯。

## 设置
**安装终端**
无论你使用何种操作系统（Windows、macOS、Linux），终端都是 CS 61A 的必备工具。

**macOS/Linux**
如果你使用 Mac 或某种 Linux 发行版（如 Ubuntu），系统已经自带了终端程序，打开它即可。

**Windows**
可以跳过这步，直接使用预装的 PowerShell。以后课程可能会用到 Bash，如果你想提前熟悉，可以安装 Git-Bash。

### 安装 Python 3
Python 3 是本课程主要使用的编程语言。

**Linux**
运行 `sudo apt install python3`（Ubuntu），或根据你的发行版使用相应命令。

**macOS**
下载并安装 Python 3（64-bit）。安装后，关闭并重新打开终端。

> ### 使用Homebrew安装Python3
>
> #### 安装Homebrew
> 如果你的Mac上还没有安装Homebrew，可以先通过以下命令安装Homebrew。Homebrew是macOS上的包管理器，可以方便地安装和管理软件包。
>
> ```sh
> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
> ```
>
> #### 安装Python3
> 安装Homebrew后，打开终端并输入以下命令来安装Python3：
>
> ```sh
> brew install python
> ```
>
> 这个命令将安装最新版本的Python3，并包括pip（Python的包管理工具）。
>

**Windows**
官网安装，确保选中“ads Python 3.x to PATH”框。 https://www.python.org/

![Windows PATH at setup](./assets/python-windows-install-path-1800377.png)

### 安装文本编辑器
需要一个文本编辑器来编写 Python 代码。Visual Studio Code 是推荐的选择，但你可以使用任何你喜欢的编辑器。

### 使用终端
**检查安装**
打开终端，输入以下命令检查 Python 3 是否安装成功：

```sh
python3
```

看到 `>>>` 提示符，说明安装成功。可以输入 `exit()` 或 `Ctrl-D` 退出。

> ### 测试Python3是否安装成功
>
> #### 检查Python3版本
>
> 安装完成后，可以通过以下命令检查Python3的版本，确认安装是否成功：
>
> ```sh
> python3 --version
> ```
>
> 你应该会看到类似以下的输出，显示当前安装的Python3版本号：
>
> ```sh
> Python 3.x.x
> ```
>
> #### 检查pip3版本
>
> 还可以检查pip3的版本，确认pip3是否安装成功：
>
> ```sh
> pip3 --version
> ```
>
> 你应该会看到类似以下的输出，显示当前安装的pip3版本号：
>
> ```sh
> pip 21.x.x from /usr/local/lib/python3.x/site-packages/pip (python 3.x)
> ```
>
> ### 测试Python3运行环境
>
> #### 运行Python3解释器
>
> 在终端中输入以下命令启动Python3解释器：
>
> ```sh
> python3
> ```
>
> 你应该会看到类似以下的交互式解释器提示符：
>
> ```sh
> Python 3.x.x (default, Month Day Year, HH:MM:SS)
> [Clang 12.0.0 (clang-1200.0.32.29)] on darwin
> Type "help", "copyright", "credits" or "license" for more information.
> >>>
> ```
>
> #### 运行一个简单的Python3程序
>
> 在Python3解释器中，输入以下命令来运行一个简单的程序：
>
> ```python
> print("Hello, World!")
> ```
>
> 你应该会看到以下输出：
>
> ```sh
> Hello, World!
> ```
>
> 输入以下命令退出Python3解释器：
>
> ```
> exit()
> ```

## **组织文件**（或自行组织）

使用 `ls` 列出当前目录内容，使用 `cd` 进入目录，使用 `mkdir` 创建新目录。例如：

```sh
cd ~/Desktop
mkdir cs61a
cd cs61a
mkdir projects labs
```

### **下载并解压作业文件**

下载 `lab00.zip`，使用以下命令解压（或者任意方法）：

```sh
cd ~/Downloads
unzip lab00.zip
```

解压后会看到一个名为 `lab00` 的新文件夹，包含以下文件：

- `lab00.py`：模板文件
- `ok`：用于测试和提交作业的程序
- `lab00.ok`：`ok` 的配置文件
- 什么文件夹，无所谓别管它

### 移动文件
将实验文件移动到之前创建的 `lab` 文件夹：

```sh
mv ~/Downloads/lab00 ~/Desktop/cs61a/lab
```

使用 `mv` 命令将 `~/Downloads/lab00` 文件夹移动到 `~/Desktop/cs61a/lab` 文件夹中。

接下来，进入刚刚移动的 `lab00` 文件夹。你可以尝试自己用 `cd` 导航，如果遇到问题，可以使用以下命令：

```sh
cd ~/Desktop/cs61a/lab/lab00
```

### 命令总结
以下是刚刚用到的命令：

- `ls`: 列出当前目录中的所有文件
- `cd <目录路径>`: 切换到指定目录
- `mkdir <目录名>`: 创建一个新目录
- `mv <源路径> <目标路径>`: 移动文件或文件夹

## Python 基础
### 表达式和语句
程序由表达式和语句组成。表达式计算并返回一个值，而语句执行操作。

打开 Python 解释器：

```sh
python3
```

如果使用 Windows，试试 `python` 或 `py` 命令。

### 基本表达式
基本表达式只需一步即可计算，例如数字和布尔值：

```python
>>> 3
3
>>> True
True
```

### 算术表达式
使用数学运算符可以组合数字形成复合表达式：

```python
>>> 7 / 4
1.75
>>> 7 // 4
1
>>> 7 % 4
3
```

### 赋值语句
赋值语句将表达式的值绑定到一个名称：

```python
>>> a = (100 + 50) // 2
>>> a
75
```

## 做实验
### 解锁测试
在终端中输入以下命令开始测试：

```sh
python3 ok -q python-basics -u --local
```

根据提示输入输出结果。

### 理解问题
打开 `lab00.py` 文件，根据描述完成代码。

### 编写代码
理解问题后，开始编写代码。例如：

```python
def twenty_twenty():
    return 2020
```

保存文件。

### 运行测试
在终端中运行以下命令测试代码：

```sh
python3 ok --local
```



通过以上步骤，你就可以完成并测试 CS 61A 的实验。如果有任何问题，随时寻求帮助！

---

### 如果需要 Anaconda 
Anaconda 是一个广泛使用的 Python 发行版，特别适用于数据科学、机器学习和大数据处理。它包含了 Python、conda 包管理器以及许多常用的数据科学库和工具（如 NumPy、Pandas、SciPy、Jupyter Notebook 等），简化了环境配置和依赖管理。

### 安装 Anaconda 的步骤
根据你的操作系统，[选择适当的 Anaconda 版本进行安装](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/?C=M&O=A%EF%BC%89)。以下是各个平台的安装步骤：

#### macOS
1. **选择版本**：
   
   - **Intel 架构（x86_64）**：
     - 下载 `Anaconda3-xxxx-MacOSX-x86_64.pkg` 或 `Anaconda3-xxxx-MacOSX-x86_64.sh`。
   - **Apple Silicon 架构（arm64）**：
     - 下载 `Anaconda3-xxxx-MacOSX-arm64.pkg` 或 `Anaconda3-xxxx-MacOSX-arm64.sh`。
   
2. **安装**：
   - 使用 `.pkg` 文件：
     - 双击下载的 `.pkg` 文件，按照屏幕上的提示进行安装。
   - 使用 `.sh` 文件：
     - 打开终端，导航到下载目录，并运行以下命令：
       ```sh
       bash Anaconda3-xxxx-MacOSX-x86_64.sh
       ```
       或
       ```sh
       bash Anaconda3-xxxx-MacOSX-arm64.sh
       ```

3. **初始化 Anaconda**：
   - 安装完成后，初始化 Anaconda：
     ```sh
     source ~/.bashrc
     ```
     如果你使用的是 Zsh：
     ```sh
     source ~/.zshrc
     ```

#### Windows
1. **选择版本**：
   - 下载 `Anaconda3-xxxx-Windows-x86_64.exe`。

2. **安装**：
   - 双击下载的 `.exe` 文件，按照屏幕上的提示进行安装。

3. **初始化 Anaconda**：
   - 安装完成后，打开 Anaconda Prompt（通过开始菜单搜索“Anaconda Prompt”），可以在其中使用 conda 命令。

#### Linux
1. **选择版本**：
   - **Intel 架构（x86_64）**：
     - 下载 `Anaconda3-xxxx-Linux-x86_64.sh`。
   - **s390x 架构**：
     - 下载 `Anaconda3-xxxx-Linux-s390x.sh`。

2. **安装**：
   - 打开终端，导航到下载目录，并运行以下命令：
     ```sh
     bash Anaconda3-xxxx-Linux-x86_64.sh
     ```
     或
     ```sh
     bash Anaconda3-xxxx-Linux-s390x.sh
     ```

3. **初始化 Anaconda**：
   - 安装完成后，初始化 Anaconda：
     ```sh
     source ~/.bashrc
     ```
     如果你使用的是 Zsh：
     ```sh
     source ~/.zshrc
     ```

### 配置 Anaconda 环境
1. **创建并激活环境**：
   ```sh
   conda create -n cs61a_env python=3.8
   conda activate cs61a_env
   ```

2. **安装依赖**：
   
   ```sh
   conda install 需要的依赖
   ```
   
3. **运行 Python**：
   ```sh
   python
   ```

> 新建终端测试前需要激活环境```conda activate cs61a_env```。

通过以上步骤，你就可以在不同平台上安装和配置 Anaconda。根据你的操作系统选择适当的版本进行安装，配置完成后可以方便地管理和运行 Python 项目。如果有任何问题，随时寻求帮助！



---



# 使用 Ok

CS 61A 使用名为 `ok` 的程序来测试和提交作业、实验和项目。

每个编程作业将包含一个 `.zip` 压缩包，内含以下内容：

- 起始代码
- 一份 `ok` 副本

在解压压缩包内容后，你可以开始你的作业。

## 使用 Ok 测试

编写一些代码后，你可以通过 `ok` 以多种方式测试你的代码。

> 后加```--local```进行本地测试。

### 测试特定问题

要测试特定问题，请使用带有问题名称的 `-q` 选项：

```
python3 ok -q 问题名称
```

### 测试所有问题

你可以使用以下命令运行所有测试：

```
python3 ok
```

### 显示所有测试

默认情况下，只有**失败**的测试会显示。如果你想查看所有测试的结果，可以使用 `-v` 选项：

```
python3 ok -v
```

### 本地测试

如果你不想将进度发送到服务器，或在登录时遇到问题，**请添加 `--local` 标志以阻止所有通信**：

```
python3 ok --local
```

### 添加你自己的测试

你可以编写自己的测试并使用 `ok` 运行它们。默认情况下，测试文件名为 `mytests.rst`。你可以使用不同的名称，但在运行测试时需要指定它。

### 运行你自己的测试

要运行 `mytests.rst` 中所有测试并显示详细结果：

```
python3 ok -t -v
```

如果你将测试放在不同文件或将测试分成多个文件：

```
python3 ok -t 你的新文件名.rst
```

要仅运行 `mytests.rst` 中的第1套第1个案例的测试：

```
python3 ok -t --suite 1 --case 1
```

你可能已经注意到，测试的“覆盖率”百分比（请注意，仅在运行所有测试时才会返回覆盖率统计数据）。这是你测试的[代码覆盖率](https://en.wikipedia.org/wiki/Code_coverage)的度量。

要获取增加覆盖率的指导意见：

```
python3 ok -t -cov
```

代码覆盖率不包括 `ok` 测试，因此覆盖率百分比实际上可能更高。

虽然代码覆盖率是一个有用的工具，但你不应过分关注这个数字。编写有助于完成问题并让生活更轻松的测试比达到更高的覆盖率更好。

