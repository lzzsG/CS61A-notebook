---
layout: page
title: Lab 0. Workflow and Python Basics
permalink: /Lab00/
nav_order: 0
parent: Lecture 1. Computer Science


---

# Lab 0. Workflow and Python Basics

## Starter Files入门文件

Download [lab00.zip](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/lab00.zip). Inside the archive, you will find starter files for the questions in this lab, along with a copy of the [Ok](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/ok) autograder.下载 lab00.zip。在存档中，您将找到本实验中问题的入门文件，以及 Ok 自动评分器的副本。

## Submission提交

By the end of this lab, you should have submitted the lab with `python3 ok --submit`. You may submit more than once before the deadline; only the final submission will be graded. Check that you have successfully submitted your code on [okpy.org](https://okpy.org/).在本实验结束时，您应该已经使用 python3 ok --submit 提交了实验。您可以在截止日期前多次提交；仅对最终提交的作品进行评分。检查您是否已在 okpy.org 上成功提交代码。

## Introduction介绍

This lab explains how to use your own computer to complete assignments for CS 61A, as well as introduce some of the basics of Python. If you are using a lab computer, most of the instructions are the same, except you won't have to install anything.本实验介绍了如何使用自己的计算机完成 CS 61A 作业，并介绍了一些 Python 基础知识。如果您使用的是实验室计算机，大多数说明都是相同的，只是您无需安装任何东西。

If you need any help at any time through the lab, please feel free to come to [office hours](https://cs61a.org/office-hours.html) or post on piazza.如果您在实验室任何时候需要任何帮助，请随时来到办公时间或在广场上发帖。

This lab looks really long, but it's mostly setup and learning how to use essential tools for this class; these may seem a bit difficult now, but quickly become second nature as we move further into the course.这个实验看起来很长，但主要是设置和学习如何使用本课程的基本工具；这些现在看起来可能有点困难，但随着我们进一步学习课程，它们很快就会成为第二天性。

## Setup设置

### Register for an account注册一个帐户

> These accounts allow you to use instructional machines in the CS department, which can be useful if you do not have regular access to a computer. They are **not required if you do not plan on using the lab computers or printers**.这些帐户允许您使用计算机科学部门的教学机器，如果您无法定期访问计算机，这可能会很有用。如果您不打算使用实验室计算机或打印机，则不需要它们。

Signing up for a class account注册班级帐户
Logging into your class account登录您的班级帐户
Changing your password更改您的密码
Registering your account注册您的帐户
Logging Out注销

### Install a terminal安装终端

The terminal is a program that allows you to interact with your computer by entering commands. No matter what operating system you use (Windows, macOS, Linux), the terminal will be an essential tool for CS 61A.终端是一个程序，允许您通过输入命令与计算机进行交互。无论您使用什么操作系统（Windows、macOS、Linux），终端都将是 CS 61A 的必备工具。

### macOS/LinuxmacOS/Linux

If you're on a Mac or are using a form of Linux (such as Ubuntu), you already have a program called `Terminal` or something similar on your computer. Open that up and you should be good to go.如果您使用的是 Mac 或使用某种形式的 Linux（例如 Ubuntu），则您的计算机上已经有一个名为“终端”或类似程序的程序。打开它，你就可以开始了。

### Windows视窗

For Windows users, we recommend a terminal called Git-Bash. You can try either method below:对于 Windows 用户，我们推荐一个名为 Git-Bash 的终端。您可以尝试以下任一方法：

- **Easy (automatic) method:** Download and run our [automatic installer](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/assets/Install-Python-on-Windows.jse), and follow the displayed instructions.简单（自动）方法：下载并运行我们的自动安装程序，然后按照显示的说明进行操作。
  (*Advanced users:* If double-clicking doesn't work, you can try `cscript "Install-Python-on-Windows.jse"` from the Command Prompt.)（高级用户：如果双击不起作用，您可以在命令提示符下尝试 cscript“Install-Python-on-Windows.jse”。）
  If this method **succeeds**, you can move on and [install a text editor](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/#install-a-text-editor); you now run Python inside Git-Bash. (In fact, *only* inside Git-Bash. So this *won't* let you run `.py` files by double-clicking them. But you shouldn't need to do that for this course.)如果此方法成功，您可以继续安装文本编辑器；现在，您可以在 Git-Bash 中运行 Python。 （事实上​​，仅在 Git-Bash 中。所以这不会让您通过双击 .py 文件来运行它们。但在本课程中您不需要这样做。）
  If this method **fails**, try the alternate method below.如果此方法失败，请尝试下面的替代方法。

  > *Anti-virus note:* Some anti-viruses mistakenly flag our installer as a virus. We're aware of this, but there's little we can do to prevent it.防病毒说明：某些防病毒软件错误地将我们的安装程序标记为病毒。我们知道这一点，但我们无能为力来阻止它。
  > In the case of Windows Defender, some students have reported success by clicking "See Details", letting it scan the file, and then rebooting.就 Windows Defender 而言，一些学生报告说，通过单击“查看详细信息”，让它扫描文件，然后重新启动，成功了。
  > Otherwise, you can try to exclude/whitelist the file from scanning.否则，您可以尝试从扫描中排除/白名单文件。
  > If neither of these work for you or you aren't comfortable messing with your anti-virus software, you can just use the manual installation method below.如果这两种方法都不适合您，或者您不喜欢使用防病毒软件，则可以使用下面的手动安装方法。

  

- **Alternate (manual) method:替代（手动）方法：**
  First, if you already tried the automatic installer above, make sure it's fully cleaned up:首先，如果您已经尝试过上面的自动安装程序，请确保它已完全清理：

  1. Look for *Git* as an installed program in "Add/Remove Programs", and, if it exists, uninstall it.在“添加/删除程序”中查找已安装的 Git 程序，如果存在，请将其卸载。
  2. Once Git is no longer installed, if a `C:\Program Files\Git` folder still exists, delete that too.不再安装 Git 后，如果 C:\Program Files\Git 文件夹仍然存在，请将其也删除。

  Now download and install [Git Bash](https://git-scm.com/download/win). You can use the default options, **with one exception**:现在下载并安装 Git Bash。您可以使用默认选项，但有一个例外：
  Select ***Use Windows' default console window\*** in the *Configuring the terminal emulator to use with Git Bash* step.在配置终端模拟器以与 Git Bash 一起使用步骤中选择使用 Windows 的默认控制台窗口。
  **This is very important! If you do not select this option, your terminal won't work with Python!这个非常重要！如果您不选择此选项，您的终端将无法使用 Python！**
  ![Git Bash configuration options]({{ site.baseurl }}/docs/Lec01/assets/git-bash-options.png)

> *If you're already using Git-Bash from outside this course and reinstalling it isn't an option:如果您已经在本课程之外使用 Git-Bash，并且无法重新安装它：*
> Depending on whether you selected the MinTTY option when installing Git, it's possible that typing a command like `python` won't display anything on the screen. You can fix this by typing `winpty python` instead (or `winpty python3`, etc. as described below), but it will be painful, as you will have to remember to do this *every time* for the rest of the course! Hence we recommend that you go back and reinstall Git-Bash with the recommended options if at all possible.根据您在安装 Git 时是否选择了 MinTTY 选项，输入像 python 这样的命令可能不会在屏幕上显示任何内容。您可以通过输入 winpty python（或 winpty python3 等，如下所述）来解决此问题，但这会很痛苦，因为您必须记住在课程的其余部分中每次都执行此操作！因此，如果可能的话，我们建议您返回并使用推荐的选项重新安装 Git-Bash。

If everything succeeded, you are now able to launch a terminal on Windows by running Git-Bash.如果一切成功，您现在可以通过运行 Git-Bash 在 Windows 上启动终端。

> *SSL/TLS errors:* If you ran into connection security errors, you may need to update your system and/or enable TLS 1.2 (e.g. see [here](https://support.microsoft.com/en-us/help/3140245) for Windows 7). You can check your TLS version by installing Python first, and running the following in `python3`:SSL/TLS 错误：如果您遇到连接安全错误，您可能需要更新系统和/或启用 TLS 1.2（例如，对于 Windows 7，请参阅此处）。您可以通过先安装 Python 并在 python3 中运行以下命令来检查 TLS 版本：
>
> ```
> from json import loads; from urllib.request import urlopen;
> loads(urlopen('https://www.howsmyssl.com/a/check').read().decode('UTF-8'))['tls_version']
> ```
>
> 
>
> If you don't see TLS 1.2 or later, that may be why you are encountering problems.如果您没有看到 TLS 1.2 或更高版本，这可能就是您遇到问题的原因。
> If you're on Windows 10, though, the problem may be something else, and you may need to search/ask for help.但是，如果您使用的是 Windows 10，问题可能是其他问题，您可能需要搜索/寻求帮助。

### Install Python 3安装Python 3

Python 3 is the primary programming language used in this course. Use the instructions below to install the Python 3 interpreter.Python 3 是本课程使用的主要编程语言。使用以下说明安装 Python 3 解释器。
(The instructions may feature older versions of Python 3, but the steps are similar.)（这些说明可能使用旧版本的 Python 3，但步骤类似。）

### LinuxLinux

Run `sudo apt install python3` (Ubuntu), `sudo pacman -S python3` (Arch), or the command for your distro.运行 sudo apt install python3 (Ubuntu)、sudo pacman -S python3 (Arch) 或适用于您的发行版的命令。

### macOS苹果系统

Download and install Python: for Windows [click here](https://www.python.org/ftp/python/3.8.1/python-3.8.1-amd64.exe), for Mac or Linux [click here](https://www.python.org/downloads/).下载并安装 Python：对于 Windows，请单击此处；对于 Mac 或 Linux，请单击此处。
Refer to this [video](https://www.youtube.com/watch?v=smHuBHxJdK8) for additional help on setting up Python.请参阅此视频以获取有关设置 Python 的其他帮助。

You may need to right-click the download icon and select "Open". After installing please close and open your Terminal.您可能需要右键单击下载图标并选择“打开”。安装后，请关闭并打开您的终端。

### Windows视窗

If you used our automated installer successfully, skip to the next section—you should already have Python.如果您成功使用了我们的自动安装程序，请跳到下一部分 - 您应该已经拥有 Python。

Otherwise, if you're installing manually, download [Python](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/) and **make sure to check the "Add Python 3.x to PATH" box**, which will allow you to execute the `python` command from your terminal.否则，如果您手动安装，请下载 Python 并确保选中“将 Python 3.x 添加到 PATH”框，这将允许您从终端执行 python 命令。

After installing please close and open your Terminal.安装后，请关闭并打开您的终端。

![Windows PATH at setup]({{ site.baseurl }}/docs/Lec01/assets/python-windows-install-path.png)

### Other其他

[Download Python from the download page](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/).从下载页面下载 Python。

### Install a text editor安装文本编辑器

The **Python interpreter** that you just installed allows you to *run* Python code. You will also need a **text editor**, where you will *write* Python code.您刚刚安装的 Python 解释器允许您运行 Python 代码。您还需要一个文本编辑器，您可以在其中编写 Python 代码。

There are many editors out there, each with its own set of features. We find that [Atom](https://atom.io/) and [Sublime Text 3](http://www.sublimetext.com/3) are popular choices among students, but you are free to use other text editors.那里有很多编辑器，每个编辑器都有自己的一组功能。我们发现 Atom 和 Sublime Text 3 是学生中最受欢迎的选择，但您可以自由使用其他文本编辑器。

> **Note**: Please, please, *please* do not use word processors such as Microsoft Word to edit programs.注意：请、请、请不要使用 Microsoft Word 等文字处理程序来编辑程序。

For your reference, we've also written some guides on using popular text editors. After you're done with lab, you can take a look if you're interested:为了供您参考，我们还编写了一些有关使用流行文本编辑器的指南。完成实验后，如果您感兴趣，可以看一下：

- [Atom原子](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/atom.html)
- [Sublime Text 3崇高文本3](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/sublime.html)
- [EmacsEmacs](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/emacs.html)
- [Vim维姆](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/vim.html)

## Using the terminal使用终端

Let's check if everything was installed properly!让我们检查一切是否安装正确！

First, open a terminal window. (If you're on Windows, launch *Git-Bash* from the Start menu.)首先，打开一个终端窗口。 （如果您使用的是 Windows，请从“开始”菜单启动 Git-Bash。）

**Important:** You should see a `$` sign, waiting for you to type commands.重要提示：您应该看到一个 $ 符号，等待您输入命令。

> If you see a `>` sign (such as `C:\Users\Oski>`), you are **not** running Bash; you are in the Windows Command Prompt! Do *not* use that! Close it, and launch Git-Bash instead. (Do *not* launch Git-CMD.)如果您看到 > 符号（例如 C:\Users\Oski>），则表明您没有运行 Bash；您正处于 Windows 命令提示符中！不要使用那个！关闭它，然后启动 Git-Bash。 （不要启动 Git-CMD。）

![starting the terminal]({{ site.baseurl }}/docs/Lec01/assets/terminal.png)

When you first open your terminal, you will start in the home directory. The **home directory** is represented by the `~` symbol.当您第一次打开终端时，您将从主目录开始。主目录由 ~ 符号表示。

> Don't worry if your terminal window doesn't look exactly the same; the important part is that the text on the left-hand side of the `$` has a `~` (tilde). That text might also have the name of your computer.如果您的终端窗口看起来不完全相同，请不要担心；重要的部分是 $ 左侧的文本有一个 ~（波形符）。该文本可能还包含您的计算机的名称。
> **If you see your home directory instead of `~`:如果您看到的是主目录而不是 ~：**Try running `echo ~`. If it displays the same path, that's also fine.尝试运行 echo ~。如果它显示相同的路径，那也没关系。

### Python InterpreterPython解释器

We can use the terminal to check if your Python 3 interpreter was installed correctly. Try the following command:我们可以使用终端来检查你的Python 3解释器是否安装正确。尝试以下命令：

```
python3
```

If the installation worked, you should see some text printed out about the interpreter followed by `>>>` on its own line. This is where you can type in Python code. Try typing some expressions you saw in lecture, or just play around to see what happens! You can type `exit()` or `Ctrl-D` to return to your command line.如果安装成功，您应该会看到打印出一些有关解释器的文本，后跟 >>> 独占一行。您可以在此处输入 Python 代码。尝试输入您在讲座中看到的一些表达方式，或者只是玩一下，看看会发生什么！您可以键入 exit() 或 Ctrl-D 返回命令行。

> Windows troubleshooting:Windows 故障排除：
>
> - If the `python3` command doesn't run *at all*:如果 python3 命令根本不运行：
>   Try `python`, `py`, or `py -3` instead.请尝试使用 python、py 或 py -3。
> - If Python freezes (doesn't display anything at all):如果 Python 冻结（根本不显示任何内容）：
>   You probably didn't select the **"Use Windows' default console window"** option when installing Git-Bash manually. Try `winpty python`, or just uninstall Git-Bash and reinstall it with the correct options.手动安装 Git-Bash 时，您可能没有选择“使用 Windows 的默认控制台窗口”选项。尝试 winpty python，或者只是卸载 Git-Bash 并使用正确的选项重新安装。
> - If you see an error like `WindowsApps/python: Permission denied`:如果您看到类似 WindowsApps/python: 权限被拒绝的错误：
>   Either (a) go to the `WindowsApps` folder whose path is shown and just delete `python.exe` and `python3.exe` in that folder, or alternatively, (b) follow [these steps](https://superuser.com/a/1461471). Then try again.(a) 转到显示路径的 WindowsApps 文件夹，然后删除该文件夹中的 python.exe 和 python3.exe，或者 (b) 按照以下步骤操作。然后再试一次。
> - If Python doesn't run *at all*, and you used our automated installer:如果 Python 根本不运行，并且您使用了我们的自动安装程序：
>   Go back and try installing using the manual method.返回并尝试使用手动方法安装。
> - If Python doesn't run *at all*, and you installed manually:如果 Python 根本不运行，并且您手动安装：
>   Make sure you set up your "PATH" correctly as shown above.确保您正确设置“路径”，如上所示。
> - If you mixed multiple versions of Python (e.g. 32-bit and 64-bit, or 3.6 and 3.8, etc.):如果您混合使用多个版本的 Python（例如 32 位和 64 位，或 3.6 和 3.8 等）：
>   They may conflict. Occasionally, this becomes extremely difficult to fix—even for instructors.他们可能会发生冲突。有时，即使对于教师来说，这个问题也变得极其难以解决。
>   Uninstall them one-by-one (the most recent one *first*), then reinstall only the latest 64-bit version.逐一卸载它们（首先卸载最新的），然后仅重新安装最新的 64 位版本。
>
> 
>
> Ask for help if you get stuck!如果您遇到困难，请寻求帮助！

## Organizing your files整理您的文件

In this section, you will learn how to manage files using terminal commands.在本节中，您将学习如何使用终端命令管理文件。

> Make sure your prompt contains a `$` somewhere in it and does not begin with `>>>`. If it begins with `>>>` you are still in a Python shell, and you need to exit. See above for how.确保您的提示符中包含 $ 并且不以 >>> 开头。如果它以 >>> 开头，那么您仍然处于 Python shell 中，需要退出。请参阅上文了解具体方法。

### Directories目录

The first command you'll use is `ls`. Try typing it in the terminal:您将使用的第一个命令是 ls。尝试在终端中输入：

```
ls
```

The `ls` command **l**i**s**ts all the files and folders in the current directory. A **directory** is another name for a folder (such as the `Documents` folder). Since you're in the home directory right now, you should see the contents of your home directory.ls 命令列出当前目录中的所有文件和文件夹。目录是文件夹（例如“文档”文件夹）的另一个名称。由于您现在位于主目录中，因此您应该会看到主目录的内容。

> If `ls` doesn't work, but `dir` does: **stop**! You've mistakenly opened the Windows Command Prompt!如果 ls 不起作用，但 dir 起作用：停止！您错误地打开了 Windows 命令提示符！
> Exit it, and run *Git-Bash* instead.退出它，然后运行 ​​Git-Bash。

### Changing directories更改目录

To move into another directory, use the `cd` command. Let's try moving into your Desktop directory. First, make sure you're in your home directory (check for the `~` on your command line) and use `ls` to see if the `Desktop` directory is present. Try typing the following command into your terminal, which should move you into that directory:要移动到另一个目录，请使用 cd 命令。让我们尝试进入您的桌面目录。首先，确保您位于主目录中（检查命令行上的 ~）并使用 ls 查看 Desktop 目录是否存在。尝试在终端中输入以下命令，这会将您移至该目录：

```
cd Desktop
```

Although, on some Windows accounts, your actual Desktop folder might actually be inside OneDrive:尽管在某些 Windows 帐户上，您的实际桌面文件夹实际上可能位于 OneDrive 内：

```
cd OneDrive/Desktop
```

If you still can't find your Desktop directory, ask a TA or a lab assistant for help.如果您仍然找不到桌面目录，请向助教或实验室助理寻求帮助。

There are a few ways to return to the home directory:返回主目录有以下几种方法：

- `cd ..` (two dots). The `..` means "the parent directory". In this case, the parent directory of `cs61a` is your home directory, so you can use `cd ..` to go up one directory.cd ..（两个点）。 .. 表示“父目录”。在这种情况下，cs61a 的父目录是您的主目录，因此您可以使用 cd .. 上一级目录。
- `cd ~` (the tilde). Remember that `~` means home directory, so this command will always change to your home directory.cd ~（波浪号）。请记住，〜表示主目录，因此此命令将始终更改为您的主目录。
- `cd` (`cd` on its own). Typing just `cd` is a shortcut for typing `cd ~`.cd（单独的 cd）。仅键入 cd 是键入 cd ~ 的快捷方式。

> You do not have to keep your files on your Desktop if you prefer otherwise. Where you keep your files locally will not affect your grade. Do whatever is easiest and most convenient for you!如果您愿意，则不必将文件保留在桌面上。您在本地保存文件的位置不会影响您的成绩。做对你来说最简单、最方便的事情！

### Making new directories制作新目录

The next command is called `mkdir`, which **m**a**k**es new **dir**ectories. Let's make a directory called `cs61a` on your Desktop to store all of the assignments for this class:下一个命令称为 mkdir，它创建新目录。让我们在桌面上创建一个名为 cs61a 的目录来存储此类的所有作业：

```
mkdir cs61a
```

A folder named `cs61a` will appear on your Desktop. You can verify this by using the `ls` command again or by simply checking your Desktop.名为 cs61a 的文件夹将出现在您的桌面上。您可以通过再次使用 ls 命令或简单地检查桌面来验证这一点。

At this point, let's create some more directories. First, make sure you are in the `~/Desktop/cs61a` directory. Then, create folders called `projects` and `lab` inside of your `cs61a` folder:此时，让我们创建更多目录。首先，确保您位于 ~/Desktop/cs61a 目录中。然后，在 cs61a 文件夹中创建名为项目和实验室的文件夹：

```
cd ~/Desktop/cs61a
mkdir projects
mkdir lab
```

Now if you list the contents of the directory (using `ls`), you'll see two folders, `projects` and `lab`.现在，如果您列出目录的内容（使用 ls），您将看到两个文件夹：projects 和 lab。

![cs61a directory]({{ site.baseurl }}/docs/Lec01/assets/terminal_commands.png)

### Downloading the assignment下载作业

If you haven't already, download the zip archive, [lab00.zip](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/lab00.zip), which contains all the files that you'll need for this lab. Once you've done that, let's find the downloaded file. On most computers, `lab00.zip` is probably located in a directory called `Downloads` in your home directory. Use the `ls` command to check:如果您还没有下载 zip 存档 lab00.zip，请下载它，其中包含本实验所需的所有文件。完成后，让我们找到下载的文件。在大多数计算机上，lab00.zip 可能位于主目录中名为 Downloads 的目录中。使用ls命令查看：

```
ls ~/Downloads
```

If you don't see `lab00.zip`, ask a TA or lab assistant for help.如果您没有看到 lab00.zip，请向助教或实验室助理寻求帮助。

### Extracting starter files提取启动文件

You must expand the zip archive before you can work on the lab files. Different operating systems and different browsers have different ways of unzipping. If you don't know how, you can search online.您必须先展开 zip 存档，然后才能处理实验室文件。不同的操作系统和不同的浏览器有不同的解压方式。如果你不知道怎么做，你可以上网搜索。

> Using a terminal, you can unzip the zip file from the command line. First, `cd` into the directory that contains the zip file:使用终端，您可以从命令行解压缩 zip 文件。首先，cd 进入包含 zip 文件的目录：
>
> ```
> cd ~/Downloads
> ```
>
> Now, run the `unzip` command with the name of the zip file:现在，使用 zip 文件的名称运行 unzip 命令：
>
> ```
> unzip lab00.zip
> ```
>
> You might also be able to unzip files without using the terminal by double clicking them in your OS's file explorer.您还可以通过在操作系统的文件资源管理器中双击文件来解压缩文件，而无需使用终端。

Once you unzip `lab00.zip`, you'll have a new folder called `lab00` which contains the following files (check it out with `cd` and `ls`):解压 lab00.zip 后，您将得到一个名为 lab00 的新文件夹，其中包含以下文件（使用 cd 和 ls 查看）：

- `lab00.py`: The template file you'll be adding your code tolab00.py：您将添加代码的模板文件
- `ok`: A program used to test and submit assignmentsok：用于测试和提交作业的程序
- `lab00.ok`: A configuration file for `ok`lab00.ok：ok的配置文件

### Moving files移动文件

Move the lab files to the lab folder you created earlier:将实验文件移动到您之前创建的实验文件夹中：

```
mv ~/Downloads/lab00 ~/Desktop/cs61a/lab
```

The `mv` command will **m**o**v**e the `~/Downloads/lab00` folder into the `~/Desktop/cs61a/lab` folder.mv 命令会将 ~/Downloads/lab00 文件夹移动到 ~/Desktop/cs61a/lab 文件夹中。

Now, go to the `lab00` folder that you just moved. Try using `cd` to navigate your own way! If you get stuck, you can use the following command:现在，转到您刚刚移动的 lab00 文件夹。尝试使用 cd 来导航！如果你遇到困难，可以使用以下命令：

```
cd ~/Desktop/cs61a/lab/lab00
```

### Summary概括

Here is a summary of the commands we just went over for your reference:以下是我们刚刚浏览过的命令摘要，供您参考：

- `ls`: **l**i**s**ts all files in the current directoryls：列出当前目录下的所有文件
- `cd <path to directory>`: **c**hange into the specified **d**irectorycd <目录路径>：进入指定目录
- `mkdir <directory name>`: **m**a**k**e a new **dir**ectory with the given namemkdir <目录名称>：使用给定名称创建一个新目录
- `mv <source path> <destination path>`: **m**o**v**e the file at the given source to the given destinationmv <源路径> <目标路径>：将给定源处的文件移动到给定目标

Finally, you're ready to start editing the lab files! Don't worry if this seems complicated -- it will get much easier over time. Just keep practicing! You can also take a look at our [UNIX tutorial](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/unix.html) for a more detailed explanation of terminal commands.最后，您可以开始编辑实验室文件了！如果这看起来很复杂，请不要担心——随着时间的推移，它会变得容易得多。继续练习吧！您还可以查看我们的 UNIX 教程，了解终端命令的更详细说明。

## Python BasicsPython 基础知识

### Expressions and statements表达式和陈述

Programs are made up of expressions and statements. In very simple terms, an *expression* is a piece of code that evaluates to some value and a *statement* is one or more lines of code that make something happen in a program.程序由表达式和语句组成。简而言之，表达式是计算结果为某个值的一段代码，而语句是使程序中发生某些事情的一行或多行代码。

When you type a Python expression into the Python interpreter, its value will be printed out. As you read through the following examples, try out some similar expressions in your own Python shell, which you can start up by typing this in your terminal:当你在 Python 解释器中输入 Python 表达式时，它的值将被打印出来。当您阅读以下示例时，请在您自己的 Python shell 中尝试一些类似的表达式，您可以通过在终端中键入以下内容来启动这些表达式：

```
python3
```

> Remember, if you are using Windows and the `python3` command doesn't work, try using `python` or `py`. See the [install Python 3](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/#install-python-3) section for more info and ask for help if you get stuck!请记住，如果您使用的是 Windows 并且 python3 命令不起作用，请尝试使用 python 或 py。请参阅安装 Python 3 部分以获取更多信息，如果遇到困难，请寻求帮助！

You'll be learning various types of expressions and statements in this course. For now, let's take a look at the ones you'll need to complete today's lab.您将在本课程中学习各种类型的表达式和陈述。现在，让我们看一下完成今天的实验所需的内容。

### Primitive expressions原始表达式

Primitive expressions only take one step to evaluate. These include numbers and booleans, which just evaluate to themselves.原始表达式只需要一步来求值。其中包括数字和布尔值，它们只是对自身求值。

```
>>> 3
3
>>> 12.5
12.5
>>> True
True
```

Names are also primitive expressions. Names evaluate to the value that they are bound to in the current environment. One way to bind a name to a value is with an assignment statement.名称也是原始的表达方式。名称的计算结果是它们在当前环境中绑定的值。将名称绑定到值的一种方法是使用赋值语句。

### Arithmetic expressions算术表达式

Numbers may be combined with mathematical operators to form compound expressions. In addition to `+` operator (addition), the `-` operator (subtraction), the `*` operator (multiplication) and the `**` operator (exponentiation), there are three division-like operators to remember:数字可以与数学运算符组合以形成复合表达式。除了 + 运算符（加法）、- 运算符（减法）、* 运算符（乘法）和 ** 运算符（求幂）之外，还有三个类似除法的运算符需要记住：

- Floating point division (`/`): divides the first number number by the second, evaluating to a number with a decimal point *even if the numbers divide evenly*浮点除法 (/)：将第一个数字除以第二个数字，即使数字被整除，也会得出带小数点的数字
- Floor division (`//`): divides the first number by the second and then rounds down, evaluating to an integer下限除法 (//)：将第一个数字除以第二个数字，然后向下舍入，计算结果为整数
- Modulo (`%`): evaluates to the positive remainder left over from division模 (%)：计算除法留下的正余数

Parentheses may be used to group subexpressions together; the entire expression is evaluated in PEMDAS order.括号可用于将子表达式分组在一起；整个表达式按照 PEMDAS 顺序进行计算。

```
>>> 7 / 4
1.75
>>> (2 + 6) / 4
2.0
>>> 7 // 4        # Floor division (rounding down)
1
>>> 7 % 4         # Modulus (remainder of 7 // 4)
3
```

### Assignment statements赋值语句

An assignment statement consists of a name and an expression. It changes the state of the program by evaluating the expression and *binding* its value to the name in the current frame.赋值语句由名称和表达式组成。它通过计算表达式并将其值绑定到当前帧中的名称来更改程序的状态。

```
>>> a = (100 + 50) // 2
```

Note that the statement itself doesn't evaluate to anything, because it's a statement and not an expression. Now, if we ask for `a`'s value, the interpreter will look it up in the current environment and output its value.请注意，语句本身不会计算任何内容，因为它是语句而不是表达式。现在，如果我们询问 a 的值，解释器将在当前环境中查找它并输出它的值。

```
>>> a
75
```

Note that the name `a` is bound to the *value* 75, *not* the expression `(100 + 50) // 2`. **Names are bound to values, not expressions.**请注意，名称 a 绑定到值 75，而不是表达式 (100 + 50) // 2. 名称绑定到值，而不是表达式。

## Doing the assignment做作业

### Unlocking tests解锁测试

One component of lab assignments is *unlocking* tests. Their purpose is to test your understanding and make sure you have a good enough grasp on the topic to make progress on the assignment.实验室任务的组成部分之一是解锁测试。他们的目的是测试您的理解程度，并确保您对主题有足够的掌握，以便在作业上取得进展。

> Enter the following in your terminal to begin this section:在终端中输入以下内容以开始本部分：
>
> ```
> python3 ok -q python-basics -u
> ```
>
> You will be prompted to enter the output of various statements/expressions. You must enter them correctly to move on, but there is no penalty for incorrect answers.系统将提示您输入各种语句/表达式的输出。您必须正确输入它们才能继续，但错误答案不会受到处罚。
>
> The first time you run Ok, you will be prompted for your bCourses email. Please follow [these directions](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/using-ok.html#signing-in-with-ok). We use this information to associate your code with you when grading.第一次运行“确定”时，系统将提示您输入 bCourses 电子邮件。请遵循这些指示。评分时，我们使用此信息将您的代码与您关联起来。

```
>>> 10 + 2
______
>>> 7 / 2
______
>>> 7 // 2
______
>>> 7 % 2		  # 7 modulo 2, equivalent to the remainder of 7 // 2
______
>>> x = 20
>>> x + 2
______
>>> x
______
>>> y = 5
>>> y += 3			# Equivalent to y = y + 3
>>> y * 2
______
>>> y //= 4			# Equivalent to y = y // 4			
>>> y + x
______
```

### Understanding problems了解问题

Labs will also consist of function writing problems. Open up `lab00.py` in your text editor. You can type `open .` on MacOS or `start .` on Windows to open the current directory in your Finder/File Explorer. Then double click or right click to open the file in your text editor. You should see something like this:实验室还将包括函数编写问题。在文本编辑器中打开 lab00.py。您可以输入 open 。在 MacOS 上或启动 .在 Windows 上打开 Finder/文件资源管理器中的当前目录。然后双击或右键单击以在文本编辑器中打开该文件。你应该看到这样的东西：

```
def twenty_twenty():
    """Come up with the most creative expression that evaluates to 2020,
    using only numbers and the +, *, and - operators.

    >>> twenty_twenty()
    2020
    """
    return ______
```



The lines in the triple-quotes `"""` are called a **docstring**, which is a description of what the function is supposed to do. When writing code in 61A, you should always read the docstring!三引号“””中的行称为文档字符串，它是对函数应该执行的操作的描述。在 61A 中编写代码时，您应该始终阅读文档字符串！

The lines that begin with `>>>` are called **doctests**. Recall that when using the Python interpreter, you write Python expressions next to `>>>` and the output is printed below that line. Doctests explain what the function does by showing actual Python code: "if we input this Python code, what should the expected output be?"以 >>> 开头的行称为 doctest。回想一下，使用 Python 解释器时，您可以在 >>> 旁边编写 Python 表达式，并且输出会打印在该行下方。文档测试通过显示实际的 Python 代码来解释该函数的功能：“如果我们输入这个 Python 代码，预期的输出应该是什么？”

In `twenty_twenty`,二二十岁时，

- The docstring tells you to "come up with the most creative expression that evaluates to 2020," but that you can only use numbers and arithmetic operators `+` (add), `*` (multiply), and `-` (subtract).文档字符串告诉您“想出最有创意的表达式，计算结果为 2020 年”，但您只能使用数字和算术运算符 +（加）、*（乘）和 -（减）。
- The doctest checks that the function call `twenty_twenty()` should return the number 2020.doctest 检查函数调用二十二十（）是否应返回数字 2020。

> You should not modify the docstring, unless you want to add your own tests! The only part of your assignments that you'll need to edit is the code.您不应该修改文档字符串，除非您想添加自己的测试！您的作业中唯一需要编辑的部分是代码。

### Writing code编写代码

Once you understand what the question is asking, you're ready to start writing code! You should replace the underscores in `return ______` with an expression that evaluates to 2020. What's the most creative expression you can come up with?一旦您理解了问题的含义，您就可以开始编写代码了！您应该将返回 ______ 中的下划线替换为计算结果为 2020 的表达式。您能想出的最有创意的表达式是什么？

> Don't forget to save your assignment after you edit it! In most text editors, you can save by navigating to File > Save or by pressing Command-S on MacOS or Ctrl-S on Windows.编辑作业后，不要忘记保存它！在大多数文本编辑器中，您可以通过导航到“文件”>“保存”或在 MacOS 上按 Command-S 或在 Windows 上按 Ctrl-S 来保存。

### Running tests运行测试

In CS 61A, we will use a program called `ok` to test our code. `ok` will be included in every assignment in this class.在 CS 61A 中，我们将使用一个名为 ok 的程序来测试我们的代码。 ok 将包含在本课程的每项作业中。

Back to the terminal! Make sure you are in the `lab00` directory we created earlier (remember, the `cd` command lets you [change directories](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/#changing-directories)).返回航站楼！确保您位于我们之前创建的 lab00 目录中（记住，cd 命令允许您更改目录）。

In that directory, you can type `ls` to verify that there are the following three files:在该目录中，您可以键入 ls 来验证是否存在以下三个文件：

- `lab00.py`: the starter file you just editedlab00.py：您刚刚编辑的起始文件
- `ok`: our testing program好的：我们的测试程序
- `lab00.ok`: a configuration file for Oklab00.ok：Ok的配置文件

Now, let's test our code to make sure it works. You can run `ok` with this command:现在，让我们测试我们的代码以确保它有效。您可以使用此命令运行确定：

```
python3 ok
```

> Remember, if you are using Windows and the `python3` command doesn't work, try using just `python` or `py`. See the the [install Python 3](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/#install-python-3) section for more info and ask for help if you get stuck!请记住，如果您使用的是 Windows 并且 python3 命令不起作用，请尝试仅使用 python 或 py。请参阅安装 Python 3 部分以获取更多信息，如果遇到困难，请寻求帮助！

If you wrote your code correctly, you should see a successful test:如果您正确编写了代码，您应该会看到成功的测试：

```
=====================================================================
Assignment: Lab 0
Ok, version v1.11.1
=====================================================================

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Running tests

---------------------------------------------------------------------
Test summary
    1 test cases passed! No cases failed.
```

If you didn't pass the tests, `ok` will instead show you something like this:如果您没有通过测试，ok 会显示如下内容：

```
---------------------------------------------------------------------
Doctests for twenty_twenty

>>> from lab00 import *
>>> twenty_twenty()
2013

# Error: expected
#     2020
# but got
#     2013

---------------------------------------------------------------------
Test summary
    0 test cases passed before encountering first failed test case
```

Fix your code in your text editor until the test passes.在文本编辑器中修复代码，直到测试通过。

> Every time you run Ok, Ok will try to back up your work. Don't worry if it says that the "Connection timed out." We won't use your backups for grading.每次运行 Ok 时，Ok 都会尝试备份您的工作。如果它显示“连接超时”，请不要担心。我们不会使用您的备份进行评分。
>
> While `ok` is the primary assignment "autograder" in CS 61A, you may find it useful at times to write some of your own tests in the form of [doctests](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/#understand-the-question). Then, you can try them out using the `-m doctest` [option for Python](https://inst.eecs.berkeley.edu/~cs61a/sp20/lab/lab00/#appendix-useful-python-command-line-options)).虽然 ok 是 CS 61A 中的主要作业“自动评分器”，但有时您可能会发现以文档测试的形式编写一些自己的测试很有用。然后，您可以使用 Python 的 -m doctest 选项来尝试它们。

## Submitting the assignment提交作业

Now that you have completed your first CS 61A assignment, it's time to turn it in. Note that it is **not** sufficient to receive credit for an assignment simply by running the autograder per the last section. You must follow these steps to submit and get points!现在您已经完成了第一个 CS 61A 作业，是时候将其上交了。请注意，仅通过按照最后一部分运行自动评分器来获得作业学分是不够的。您必须按照以下步骤提交并获得积分！

### Step 1: Submit with `ok`第1步：确定提交

In your terminal, make sure you are in the directory that contains `ok`. If you aren't there yet, you can use this command:在您的终端中，确保您位于包含 ok 的目录中。如果您还没有，可以使用以下命令：

```
cd ~/Desktop/cs61a/lab/lab00
```

Next, use `ok` with the `--submit` option:接下来，将 ok 与 --submit 选项一起使用：

```
python3 ok --submit
```

This will prompt you for an email address if you haven't run Ok before. Please follow [these directions](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/using-ok.html#signing-in-with-ok), and refer to the troubleshooting steps on that page if you encounter issues. After that, Ok will print out a message like the following:如果您之前没有运行过“确定”，这将提示您输入电子邮件地址。请按照这些说明进行操作，如果遇到问题，请参阅该页面上的故障排除步骤。之后，Ok 将打印出如下消息：

```
Submitting... 100% complete
Backup successful for user: ...
URL: https://okpy.org/...
```

### Step 2: Verify your submission第 2 步：验证您的提交

You can follow the link that Ok printed out to see your final submission, or you can go to [okpy.org](https://okpy.org/). You will be able to view your submission after you log in.您可以点击 Ok 打印出来的链接查看您的最终提交内容，也可以访问 okpy.org。登录后您就可以查看您提交的内容。

> Make sure you log in with the same email you provided when running `ok` from your terminal!确保您使用从终端正常运行时提供的同一电子邮件登录！

You should see a successful submission for Lab 0.您应该看到实验室 0 已成功提交。

**Congratulations**, you just submitted your first CS 61A assignment!恭喜，您刚刚提交了第一份 CS 61A 作业！

> More information on Ok is available [here](https://inst.eecs.berkeley.edu/~cs61a/sp20/articles/using-ok.html). You can also use the `--help` flag:有关 Ok 的更多信息请参见此处。您还可以使用 --help 标志：
>
> ```
> python3 ok --help
> ```
>
> This flag works just like it does for UNIX commands we used earlier.该标志的工作方式与我们之前使用的 UNIX 命令类似。

## Appendix: Useful Python command line options附录：有用的 Python 命令行选项

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

  ```
   python3 -m doctest 
  ```