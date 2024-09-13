# Lecture 18. Objects

## 公告
- **作业三**：今天截止提交。
- **Hog 项目修改**：可以在明天前修改，找回因组合评分丢失的分数。提交方法为：
  ```bash
  python3 --revise
  ```
  详细说明请参考 Piazza 帖子。
- **学习指南**：课程组为即将到来的期中考试准备了学习指南，期中考试将于三周后的周三进行。指南为你提供如何准备考试的建议。
- **办公时间**：明天（周五）下午 1:00 至 2:30 将有 drop-in 咨询办公时间，加入办公时间队列后，你可以就任何问题进行咨询。

## 面向对象编程引入
今天我们开始学习**面向对象编程（Object-Oriented Programming, OOP）**，这是一种新的编程方法，包含一些新的概念和语法。不过，很多基础概念你已经有所接触，比如**数据抽象**和**数据变异**。此外，还会介绍新的概念，比如**继承**。由于内容较多，建议你多花时间练习实验室中的问题，并为下周发布的与面向对象编程相关的项目分配足够的时间。

在接下来的几次讲座中，我们会详细讨论面向对象编程的内容。今天的部分将涵盖**类（class）**和**对象（object）**的基本概念。

## 类与对象
- **类**：类结合并抽象了**数据**和**功能**。之前我们大多讨论的是功能（如循环结构、条件结构、函数参数等），现在我们将探讨如何将数据和功能结合在一起。类用于定义如何存储信息以及如何操作这些信息。
- **对象**：对象是类的实例。类就像一个蓝图，而对象是根据蓝图创建的实际实例。例如，类可以定义一个房子的设计，而对象则是这个设计下建造的具体房子。

### 类与对象的区别
- 类是一个抽象的定义，定义了数据和功能。
- 对象是类的实例，是我们可以实际操作的东西。

### 类的简单示例
Python 中已经内置了一些类，例如：
- **字符串类（String Class）**：数据是字符串本身（如 `"ardvark"`），功能包括操作字符串的方法（如 `append` 方法）。
- **整数类（Integer Class）**：数据是整数，功能包括运算符（如加法运算）。

我们不仅可以使用 Python 提供的内置类，还可以定义**自己的类**，为数据和功能创建自定义组合。接下来，我们将学习如何定义自己的类并结合功能。



## 定义自己的类与对象

在 Python 中，不仅可以使用内置类，还可以定义**自己的类**，包括自定义的数据和功能。接下来，我们将重点讨论如何定义自己的类，并详细讲解其构造过程。

### 类的构造器（Constructor）

让我们从定义一个类开始，这个类的名称是 `Ball`。这个类将用于存储一个**球**的**位置（position）**和**速度（velocity）**等数据，同时也包含操作这些数据的功能（如移动球、渲染球等）。目前，我们先从概念上理解，后续会详细展示如何编写这个类。

#### 构造器的作用

构造器（Constructor）是创建类实例的关键，它负责以下几个任务：
1. **创建对象**：当调用构造器时，系统会在内存中为对象分配空间。
2. **初始化数据**：构造器根据传递的参数初始化对象的属性。在 `Ball` 类中，球的 `x` 和 `y` 位置，以及 `vx` 和 `vy` 速度会在对象创建时初始化。
3. **返回对象的地址**：构造器返回的是新建对象的内存地址，而不是对象本身。

#### 类似列表的构造过程

这个过程与 Python 中的**列表**非常相似。当创建一个列表时，Python 会在内存中分配空间，存储列表元素，并返回该列表的内存地址。通过这个地址，我们可以引用列表并操作其中的数据。同样，当我们创建 `Ball` 对象时，构造器为该对象分配内存并初始化属性，然后返回该对象的地址。

### 类的实例化

让我们来看 `Ball` 类的实例化过程。假设我们要创建一个 `Ball` 对象，它的构造函数需要 `x` 和 `y` 的位置，以及 `vx` 和 `vy` 的速度：
```python
ball = Ball(10, 15, 0, -5)  # 创建一个 Ball 对象
```
在这个例子中，`Ball` 类的构造器会做以下几件事：
1. 在内存中为 `ball` 对象分配空间。
2. 将 `x=10`、`y=15`、`vx=0`、`vy=-5` 存储为对象的属性。
3. 返回 `ball` 对象的内存地址。

此时，`ball` 对象包含了四个属性：`x`、`y`、`vx` 和 `vy`，并存储在内存中。我们可以通过这个对象引用这些数据，并使用该类所定义的功能。

### 多个对象的实例化

如果我们再创建另一个 `Ball` 对象，例如：
```python
ball2 = Ball(12, 23, 2, 3)
```
构造器会再次执行相同的步骤，为 `ball2` 分配新的内存空间，初始化 `x=12`、`y=23`、`vx=2`、`vy=3`，并返回该对象的内存地址。此时，`ball` 和 `ball2` 是**完全独立的对象**，各自存储着自己的数据，并且拥有相同的操作功能。

### 小结

- **类**是数据和功能的抽象定义。
- **对象**是类的实例，具有独立的数据和功能。
- 构造器负责对象的创建和初始化，并返回对象的内存地址。
- 每个对象都是独立的，拥有自己的数据空间。

通过这种方式，我们可以创建多个 `Ball` 对象，并分别操作它们的数据和功能。在接下来的讲解中，我们将深入探讨如何定义类的具体细节，包括如何定义数据属性和功能方法。





## 对象的数据与功能访问

每个对象都有**自己的数据**和**功能**，我们可以通过**点号表示法**来访问这些数据或调用与该对象相关的功能。这里我们先从概念上理解点号表示法，然后再深入探讨其实现细节。

### 点号表示法访问数据

当我们定义了一个对象（例如 `ball1`），可以通过**点号**来访问对象的属性。例如，`ball1` 是一个球对象，包含 `x` 和 `y` 位置以及 `vx` 和 `vy` 速度。你可以通过点号表示法访问这些属性：
```python
ball1.x  # 访问球的 x 坐标
ball1.vx  # 访问球的 x 方向速度
```
这种点号表示法让我们能够**精确地指定**我们想访问的对象和其对应的数据。与拥有多个对象类似，我们需要明确指定要操作的是哪个对象的数据。

### 点号表示法调用功能

除了访问对象的数据，我们还可以通过点号表示法调用对象的方法（功能）。每个对象都可以有一组与其相关的功能，这些功能可以操作对象的数据。例如，假设 `Ball` 类有一个 `update_position` 方法，用于根据球的速度更新其位置：
```python
ball1.update_position(0.1)  # 更新球的位置，时间步长为 0.1
```
在这个例子中，`ball1.update_position()` 方法会根据球的当前速度和给定的时间步长更新它的 `x` 和 `y` 坐标。

### 点号表示法的使用示例

假设我们有一个球对象，初始位置为 `(5, 4)`，速度为 `(3, 6)`，并且我们想要更新它的位置。可以通过点号表示法访问和操作该对象的数据：
```python
ball1 = Ball(5, 4, 3, 6)  # 创建一个 Ball 对象，初始位置为 (5, 4)，速度为 (3, 6)
print(ball1.x)  # 打印球的 x 坐标，输出 5
ball1.update_position(0.1)  # 更新球的位置
print(ball1.x)  # 打印球的新 x 坐标，输出 5.3（x 坐标更新了 0.3）
```
在这里，`update_position` 方法会根据给定的时间步长（0.1 秒）和球的速度更新它的 `x` 和 `y` 位置。对于 `x` 坐标，由于速度为 3 像素/秒，0.1 秒后 `x` 坐标会增加 `3 * 0.1 = 0.3` 像素，从 `5` 变为 `5.3`。

### 类和对象的功能分配

类不仅可以存储数据，还可以提供对这些数据的操作功能。对于 `Ball` 类，功能可能包括更新位置、渲染球等。例如，当调用 `ball1.update_position()` 时，该方法会操作 `ball1` 的 `x` 和 `y` 数据。这说明，每个对象都有自己的数据，并且功能只能作用于该对象的特定数据。

你可以为每个对象创建独立的功能。例如，如果创建了第二个球对象 `ball2`，它将有自己的位置和速度，并且可以独立于 `ball1` 进行更新：
```python
ball2 = Ball(12, 23, 2, 3)
ball2.update_position(0.1)  # 更新 ball2 的位置
```

### 结论

- 点号表示法用于访问对象的属性或调用对象的方法。
- 每个对象的属性和方法都是独立的，多个对象之间互不影响。
- 类定义了对象的数据和功能，而通过实例化对象，我们可以访问和操作这些数据。

在接下来的课程中，我们将更深入地讲解如何定义类、属性和方法，以及如何在 Python 中构建自己的面向对象程序。





## 面向对象编程引入

我们已经知道，在 Python 中，所有的值都是对象。今天我们将更深入地理解什么是**面向对象编程（Object-Oriented Programming, OOP）**。OOP 是一种组织程序的方法，它强调将数据和与其相关的功能捆绑在一起。

### 模块化和抽象
面向对象编程通过定义独立的模块来组织程序，这意味着我们可以在不关心其他模块细节的情况下定义每个模块。这种方法依赖于**抽象屏障**，即我们将信息和行为绑定在一起，并通过清晰的接口进行交互。

### 分布式状态的比喻
在 OOP 中，每个对象都有自己的**局部状态**，并且知道如何通过调用方法来管理自己的状态。对象之间通过**消息传递**来进行交互，类似于调用方法。每个对象管理自己的状态，因此当我们想了解程序的状态时，必须检查各个对象的状态。对象通过调用方法来更新自身的状态，方法调用可以看作是对象之间传递的消息。

### 类与对象的关系
多个对象可能是相同类的实例，而不同的类之间也可能存在关联。**类**是对象的模板，所有对象都是某个类的实例。Python 提供了许多内置类，例如 `int`、`list` 等，但现在我们将开始定义自己的类。

## 银行账户示例

让我们通过一个银行账户的示例来理解类和对象的概念。假设我们要定义一个**账户类（Account）**，每个账户都具有余额（balance）和账户持有人（account holder）的属性。所有账户共享相同的行为，比如存款和取款。

### 创建账户类
当我们创建一个账户时，会指定账户持有人，并将余额初始设置为 0。代码如下所示：
```python
class Account:
    def __init__(self, holder):
        self.holder = holder
        self.balance = 0
```
- `__init__` 是构造器方法，用于初始化新对象。这里我们初始化了 `holder` 和 `balance` 属性。

### 账户操作方法
每个账户应该具备存款和取款的功能，这可以通过定义方法来实现：
```python
def deposit(self, amount):
    self.balance += amount
    return self.balance

def withdraw(self, amount):
    if self.balance < amount:
        return "Insufficient funds"
    self.balance -= amount
    return self.balance
```
- `deposit` 方法将存款金额加入余额。
- `withdraw` 方法则从余额中扣除指定金额，如果余额不足，则返回“余额不足”的提示。

### 创建账户对象
创建账户对象的示例：
```python
a = Account('Jim')  # 创建一个账户，持有人为 Jim
print(a.holder)     # 输出 'Jim'
print(a.balance)    # 输出 0
```

### 使用账户功能
我们可以通过账户对象调用存款和取款方法：
```python
a.deposit(15)  # Jim 存入 $15，余额为 15
a.withdraw(10)  # Jim 取出 $10，余额为 5
print(a.balance)  # 输出 5
```

### 类共享方法
在 OOP 中，所有账户对象共享相同的 `deposit` 和 `withdraw` 方法。这确保了所有账户的行为一致，而不是每个对象各自定义其方法。通过使用类声明，我们可以在所有实例间共享相同的行为。

## 类的定义语法

在 Python 中，使用 `class` 语句定义类，语法如下：
```python
class ClassName:
    def __init__(self, ...):
        # 初始化代码
    def method(self, ...):
        # 方法代码
```
- 类声明创建了一个新的类，可以作为某些对象的类型，并将该类绑定到当前环境中的名称。
- `__init__` 是构造器，用于初始化新实例。
- 类中的方法通过第一个参数 `self` 访问对象的属性和其他方法。

## 小结

- 面向对象编程强调**将数据和行为捆绑在一起**，对象之间通过方法调用（消息传递）来交互。
- **类**是对象的模板，**对象**是类的实例，每个对象都有自己的数据和行为。
- Python 的 OOP 语法通过 `class` 语句定义类，类中定义构造器 `__init__` 和各种方法。



## 类声明和构造器

### 定义类和属性
通过 **`class`** 语句，我们可以定义任何类型的数据。一个类声明的基本形式如下：
```python
class ClassName:
    # 类的定义
```
类声明会立即执行类中的代码，并在当前环境中将类名绑定到新创建的类对象上。类内部的赋值语句和函数定义（`def` 语句）会创建类的属性。例如，如果我们定义一个名为 `Clown` 的类，并添加属性 `nose` 和方法 `dance`：
```python
class Clown:
    nose = 'big and red'
    
    def dance():
        return "No thanks"
```
此时，我们可以通过 `Clown.nose` 访问 `nose` 属性，并通过 `Clown.dance()` 调用 `dance` 方法。

### 创建类实例
类的主要目的是用于创建其实例（对象）。当调用一个类时，会创建一个新的类实例。类实例一开始是空白的，类中的构造器方法 `__init__` 会被调用，初始化实例的属性。

例如，假设我们有一个 `Account` 类，它为每个账户提供余额和账户持有人。创建 `Account` 类实例的过程如下：
```python
class Account:
    def __init__(self, holder):
        self.holder = holder  # 账户持有人
        self.balance = 0  # 初始余额为 0
```
- `__init__` 方法是类的构造器，它会在类实例创建时自动调用。
- `self` 是对当前对象实例的引用，允许我们对该实例的属性进行操作。

### 创建和使用对象
现在我们可以使用 `Account` 类来创建对象：
```python
a = Account('Jim')  # 创建一个账户，持有人为 Jim
print(a.holder)  # 输出 'Jim'
print(a.balance)  # 输出 0
```
当调用 `Account('Jim')` 时，类的 `__init__` 方法会执行，初始化 `holder` 为 `'Jim'`，`balance` 为 `0`。

### 对象的唯一性
每个类的实例都是独立的，有自己独立的属性。如果创建多个对象，它们会拥有不同的数据：
```python
b = Account('Jack')
print(b.holder)  # 输出 'Jack'
print(b.balance)  # 输出 0
```
即使 `a` 和 `b` 都是 `Account` 类的实例，它们的 `holder` 和 `balance` 属性是互不相关的。

使用**身份运算符** `is` 和 `is not` 可以测试两个变量是否引用同一个对象：
```python
a is a  # 输出 True
a is not b  # 输出 True
```

### 赋值不会创建新对象
如果我们将一个对象赋值给另一个变量，两个变量会指向同一个对象：
```python
c = a
print(c.holder)  # 输出 'Jim'
```
此时，`c` 和 `a` 都指向同一个对象，因此它们的属性是共享的。

## 定义方法

**方法**是对象能够执行的操作，它们在类声明中定义。方法是类的一部分，它们允许我们操作对象的属性。例如，为 `Account` 类添加一个存款方法：
```python
class Account:
    def __init__(self, holder):
        self.holder = holder
        self.balance = 0

    def deposit(self, amount):
        self.balance += amount
        return self.balance
```
- `deposit` 方法将指定的 `amount` 加入当前账户的余额。
- `self` 参数引用当前对象，使得方法可以操作该对象的属性。

### 使用方法
我们可以通过创建的对象调用方法：
```python
a = Account('Jim')
a.deposit(50)  # 向账户存入 50，余额变为 50
print(a.balance)  # 输出 50
```

### 访问属性与调用方法
对象的属性可以通过点号语法直接访问，而方法则需要调用：
```python
print(a.balance)  # 访问属性，输出 50
a.deposit(25)  # 调用方法，存入 25，余额变为 75
```

## 总结
- `class` 语句用于定义类，类是对象的模板。
- 构造器 `__init__` 方法在类实例化时被调用，用于初始化对象属性。
- 对象的每个实例都有独立的属性，并可以通过方法对这些属性进行操作。
- 使用点号语法访问属性和调用方法。





## 方法与 `self` 参数

在 Python 的面向对象编程中，类中的方法可以操作该类的对象属性。每个方法的第一个参数通常命名为 `self`，它代表调用该方法的**当前实例**。当我们调用方法时，Python 会自动将调用该方法的对象作为 `self` 传递给方法，而不需要显式地提供 `self` 作为参数。

### 存款方法（`deposit`）

在 `Account` 类中，`deposit` 方法用来将存入的金额加到账户的余额中。代码如下：
```python
def deposit(self, amount):
    self.balance += amount
    return self.balance
```
- `self` 指向当前的账户对象（即调用方法的实例）。
- `amount` 是存款的金额，作为方法的参数传递。

调用 `deposit` 方法时，Python 会将调用该方法的对象自动作为 `self` 传递进去，因此我们只需提供 `amount` 参数。例如：
```python
a = Account('Jim')  # 创建一个账户对象
a.deposit(50)  # 向账户存入 50
```
这里的 `a.deposit(50)` 等价于 `Account.deposit(a, 50)`，即 `self` 是 `a` 对象，`amount` 是 50。

### 取款方法（`withdraw`）

`withdraw` 方法稍微复杂一些，因为它需要检查账户余额是否足够：
```python
def withdraw(self, amount):
    if self.balance < amount:
        return "Insufficient funds"
    self.balance -= amount
    return self.balance
```
- 如果余额不足，返回“余额不足”的信息。
- 如果余额足够，则从账户中扣除取款金额。

调用方式与 `deposit` 类似：
```python
a.withdraw(30)  # 取出 30
```

### 类中的方法是类的属性

在类定义中，方法作为类的属性被创建和绑定。例如，当定义 `deposit` 和 `withdraw` 方法时，它们成为 `Account` 类的属性。所有 `Account` 类的实例共享这些方法，而每个实例有自己独立的余额属性。

### 点号表示法调用方法

使用点号表示法可以调用对象的属性或方法。例如：
```python
a.deposit(50)  # 向账户存入 50
```
实际上，点号表示法为我们提供了两部分信息：
1. **对象**：即 `a`，表示这是哪个对象。
2. **方法**：即 `deposit`，表示要调用的方法。

### 点号表示法的实现

点号表达式的工作原理是，首先在对象的实例中查找属性，如果找不到，则会在类中查找。例如：
```python
a.deposit(10)
```
该表达式会首先在 `a` 对象中查找 `deposit` 方法，找不到时会在 `Account` 类中查找，最终找到并调用 `Account` 类的 `deposit` 方法。

### 方法的执行

当调用方法时，Python 会将调用方法的对象作为 `self` 传递给方法。例如，调用 `a.deposit(50)` 时，实际上调用的是 `Account.deposit(a, 50)`，其中 `a` 是 `self`，`50` 是 `amount`。

### 类的文档字符串和测试

在定义类时，可以为类添加**文档字符串**，描述类的作用和使用示例。还可以为类添加文档测试，以便通过简单的例子展示如何使用该类：
```python
class Account:
    """
    An Account has a balance and an account holder.
    
    >>> a = Account('Jim')
    >>> a.deposit(100)
    100
    >>> a.withdraw(50)
    50
    """
    def __init__(self, holder):
        self.holder = holder
        self.balance = 0
```

### 示例：账户类的完整实现
```python
class Account:
    def __init__(self, holder):
        self.holder = holder
        self.balance = 0

    def deposit(self, amount):
        self.balance += amount
        return self.balance

    def withdraw(self, amount):
        if self.balance < amount:
            return "Insufficient funds"
        self.balance -= amount
        return self.balance
```
使用该类创建对象并操作余额：
```python
a = Account('Jim')
print(a.deposit(100))  # 输出 100
print(a.withdraw(90))  # 输出 10
print(a.withdraw(90))  # 输出 "Insufficient funds"
```

### 小结
- **`self`** 是对当前对象的引用，允许方法访问和修改该对象的属性。
- 类中的方法是类的属性，所有对象共享这些方法。
- **点号表示法**用于访问对象的属性和方法，Python 会自动将调用方法的对象作为 `self` 传递。





## 类和实例中的属性

在 Python 中，类和实例都有自己的属性，属性可以是数据或方法。通过**点号表示法**可以访问这些属性，也可以通过内置函数 `getattr()` 进行访问。

### 实例属性与类属性

#### 实例属性
实例属性是特定于某个对象的。例如，在 `Account` 类中，每个对象有其独立的 `balance`（余额）和 `holder`（持有人）：
```python
a = Account('John')
b = Account('Jim')

print(a.holder)  # 输出 'John'
print(b.holder)  # 输出 'Jim'
```
每个对象都有自己的属性值。

#### 类属性
类属性是类本身的属性，所有对象共享。例如，设定所有账户的利率为 `0.02`：
```python
class Account:
    interest_rate = 0.02  # 类属性
```
这个 `interest_rate` 是类属性，所有 `Account` 对象都会共享它。访问方式如下：
```python
print(Account.interest_rate)  # 输出 0.02
```
即使通过实例访问类属性，实际查找的仍然是类中的值：
```python
a = Account('John')
print(a.interest_rate)  # 输出 0.02
```
如果类属性 `interest_rate` 发生变化，所有实例都会看到更新后的值：
```python
Account.interest_rate = 0.03
print(a.interest_rate)  # 输出 0.03
```

### 属性查找机制
当通过点号表示法访问属性时，Python 首先会在实例对象中查找。如果找不到对应的属性，Python 会继续在类中查找。例如：
```python
a = Account('John')
print(a.balance)  # 这是实例属性，查找实例中的 balance
print(a.interest_rate)  # 这是类属性，查找类中的 interest_rate
```

### 通过 `getattr()` 和 `hasattr()` 访问属性
除了点号表示法，还可以使用内置函数 `getattr()` 来访问属性：
```python
getattr(a, 'balance')  # 等价于 a.balance
getattr(a, 'interest_rate')  # 等价于 a.interest_rate
```
可以使用 `hasattr()` 检查对象是否拥有某个属性：
```python
hasattr(a, 'balance')  # 返回 True
hasattr(a, 'length')  # 返回 False
```

### 方法和函数的区别

在面向对象编程中，**方法**是绑定到对象的函数。方法的第一个参数是 `self`，它代表调用该方法的对象。Python 会自动将调用方法的对象作为第一个参数传递给方法。

- **函数**：直接定义在类中，未与实例绑定时，它只是一个普通的函数。
- **绑定方法**：当函数通过实例调用时，它会与该实例绑定，成为**绑定方法**。

例如：
```python
class Account:
    def deposit(self, amount):
        self.balance += amount

# 直接访问类中的函数
print(Account.deposit)  # 输出：<function Account.deposit at ...>

# 通过实例调用时，方法与实例绑定
a = Account('John')
print(a.deposit)  # 输出：<bound method Account.deposit of <__main__.Account object at ...>>
```
绑定方法不需要显式传递 `self` 参数，Python 自动传递调用该方法的对象。例如：
```python
a.deposit(100)  # 自动将 `a` 作为第一个参数 self
```

### 类属性与方法的区别
类属性与方法的查找机制相同，Python 先在实例中查找，然后在类中查找。类属性与方法的一个重要区别在于，类属性是共享的，而方法在实例化时会绑定到对象上。因此：
- **类属性**是类本身的特性，所有实例共享它。
- **实例方法**是与实例绑定的函数，方法可以访问和修改该实例的数据。

### 示例：类属性与实例属性
```python
class Account:
    interest_rate = 0.02  # 类属性

    def __init__(self, holder):
        self.holder = holder  # 实例属性
        self.balance = 0  # 实例属性

a = Account('John')
b = Account('Jim')

# 修改类属性
Account.interest_rate = 0.03

# 通过实例访问类属性
print(a.interest_rate)  # 输出 0.03
print(b.interest_rate)  # 输出 0.03

# 修改实例属性
a.balance = 100
print(a.balance)  # 输出 100
print(b.balance)  # 输出 0（b 的余额没有变化）
```

### 小结

- **实例属性**是属于对象的，每个实例都有独立的属性值。
- **类属性**是属于类的，所有实例共享类属性。
- 可以使用 **`getattr()`** 和 **`hasattr()`** 访问和检查属性。
- **方法**是绑定到对象的函数，Python 自动将调用方法的对象作为 `self` 传递给方法。



