---
layout: page
title: L19 Inheritance
permalink: /L19
description: "Lecture 19. Inheritance"
nav_order: 19




---

# Lecture 19. Inheritance

## Announcements

- **实验七**：截止时间为**周二**。
- **作业四**：截止时间为**周四**。
- **Ants 项目**：项目将在下周发布，截止时间为**下周五**。你需要在**下周二**前开始项目，以获取中途检查点（checkpoint）。提前在**下周四**前提交整个项目可以获得额外的加分。项目中还有额外的加分问题，完成后可以获得更多额外学分。

该项目基于一款名为**植物大战僵尸（Plants vs. Zombies）**的游戏，重写版名为**Ants vs. Some Bees**。你将实现游戏中的角色逻辑，这非常适合使用**面向对象编程**和**继承**。项目比以往的要短，但仍然是本学期你要完成的最大的程序之一，因此请留出足够的时间完成。

- **学术建议讨论会**：本周四将举办一个建议讨论会，讨论行业、研究生课程、班级等问题。我们还会继续提供**一对一咨询时间**，每周五下午 1:00 到 2:30 为开放时间。

- **匿名调查**：请在**周一前**完成一份简短的匿名调查，帮助我们了解你对课程的看法和建议。

- **期中考试二**：考试将于两周后的**周三**进行，考试范围涵盖本周内容。下周将不会有新内容发布，你可以专注于 Ants 项目。期中考试的形式将与期中考试一类似，如果你有不满，可以通过匿名调查反馈。

## 本节内容：面向对象编程与继承

## Attributes

### 继承的概述

**继承**是面向对象编程中的一个重要但需要谨慎使用的概念。继承允许我们创建一个类，该类可以**继承**另一个类的属性和方法，从而避免重复代码。尽管继承是一种强大的工具，但它不应该被滥用，建议只在合理的场景下应用。

### 属性回顾
对象拥有**属性**，它们是**名称-值对**。属性分为**实例属性**和**类属性**：
- **实例属性**：属于某个对象实例的属性。
- **类属性**：属于类本身的属性，所有实例共享。

当访问属性时，Python 首先在实例中查找，如果找不到则继续在类中查找。

## 继承的应用
继承可以帮助我们创建层次结构，其中一个类继承另一个类的功能。例如，假设我们有一个 `Animal` 类，包含通用的属性和方法，而 `Dog` 类可以继承 `Animal` 类，并增加或修改某些功能。这避免了在每个子类中重复定义通用功能。

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "I can make a sound."

class Dog(Animal):
    def speak(self):
        return "Woof!"

dog = Dog("Rex")
print(dog.speak())  # 输出 "Woof!"
```
在这个例子中，`Dog` 类继承了 `Animal` 类，并重写了 `speak` 方法。



## 类与实例的属性管理

在 Python 中，**类**和**实例**都有各自的属性。属性可以是实例特有的，也可以是类共享的。理解属性的查找和修改规则对使用面向对象编程（OOP）至关重要。

### 类属性和实例属性

- **类属性**：由类本身定义，所有类的实例共享该属性。
- **实例属性**：由实例单独拥有，实例之间互不影响。

例如，假设我们有一个 `Account` 类，其包含利率 (`interest`) 作为类属性，而账户持有人 (`holder`) 和余额 (`balance`) 作为实例属性：

```python
class Account:
    interest = 0.02  # 类属性

    def __init__(self, holder):
        self.holder = holder  # 实例属性
        self.balance = 0  # 实例属性
```

在这个例子中，`interest` 是所有 `Account` 实例共享的类属性，而 `holder` 和 `balance` 是每个实例单独持有的属性。

### 属性查找机制

当使用点号表示法（如 `obj.attr`）访问属性时，Python 会按照以下顺序查找：
1. 首先在实例的属性中查找。如果找到，则返回该属性值。
2. 如果实例中没有该属性，则继续在类的属性中查找。如果类中存在该属性，则返回类属性。
3. 如果类中也没有找到，则引发 `AttributeError`。

```python
a = Account('Jim')
print(a.holder)  # 输出 'Jim'，这是实例属性
print(a.interest)  # 输出 0.02，这是类属性
```

## 类属性与实例属性的修改

### 修改类属性

类属性的修改影响所有实例，因为类属性是共享的。例如：
```python
Account.interest = 0.03  # 修改类属性
print(a.interest)  # 输出 0.03，反映了类属性的变化
```
所有实例在访问 `interest` 时都会看到更新后的值，因为类属性是共享的。

### 修改实例属性

如果在实例上对属性进行赋值操作，Python 会在该实例上创建或修改该属性，而不会影响类属性或其他实例。例如：
```python
a.interest = 0.08  # 为实例 'a' 创建或修改 interest 属性
print(a.interest)  # 输出 0.08（实例属性）
print(Account.interest)  # 输出 0.03（类属性未改变）
```
此时，`a` 实例的 `interest` 属性已经变成了 0.08，而类属性 `interest` 仍然是 0.03。其他实例仍然使用类属性的值。

### 类属性和实例属性的查找顺序

1. **实例属性优先**：当访问实例属性时，Python 会优先查找实例本身的属性。
2. **类属性作为默认值**：如果实例中没有定义该属性，Python 会在类中查找该属性。

```python
b = Account('Tom')
print(b.interest)  # 输出 0.03，因为没有定义实例属性，查找类属性
```

### 绑定方法与函数

**方法**是绑定到对象的函数，调用时会自动将调用对象作为 `self` 参数传递。例如：

```python
def deposit(self, amount):
    self.balance += amount
```

当通过实例调用方法时，Python 会将实例作为 `self` 传递：
```python
a.deposit(100)  # 实际上是调用 Account.deposit(a, 100)
```

### 属性赋值

当我们对属性进行赋值操作时，Python 会根据点号左侧对象是实例还是类来决定是设置**实例属性**还是**类属性**：
- **实例属性赋值**：如果点号左侧是实例，则设置或修改该实例的属性。
- **类属性赋值**：如果点号左侧是类，则设置或修改类属性。

### 实例属性赋值
```python
a.interest = 0.08  # 为实例 'a' 设置或修改 interest 属性
print(a.interest)  # 输出 0.08
```

### 类属性赋值
```python
Account.interest = 0.04  # 修改类属性
print(a.interest)  # 输出 0.08（实例属性）
print(b.interest)  # 输出 0.04（类属性）
```



## 继承（Inheritance）

**继承**是面向对象编程的重要特性，允许我们通过继承现有类的属性和方法来创建新类。子类可以继承父类的所有属性和方法，同时可以**重写**或**扩展**父类的功能。

### 继承的语法
在 Python 中，通过在类定义的括号中指定一个**父类**来实现继承：
```python
class CheckingAccount(Account):
    withdraw_fee = 1  # 子类的属性
    interest = 0.01  # 重写父类的属性
```
在这个例子中，`CheckingAccount` 类继承了 `Account` 类，具有与普通账户类似的行为，但利率较低，并且每次提款都会收取手续费。

## 子类的特殊化
继承允许我们在子类中只定义与父类不同的部分，其余的功能可以继承。例如，`CheckingAccount` 类中，大部分功能与 `Account` 类相同，不需要重新定义。只有需要修改的部分（如利率和提款功能）需要重写。

### 子类中的方法重写
在 `CheckingAccount` 类中，提款操作需要收取额外的手续费。因此，我们重写了 `withdraw` 方法：
```python
def withdraw(self, amount):
    return super().withdraw(amount + self.withdraw_fee)
```
这里我们使用 `super()` 来调用父类的 `withdraw` 方法，并在提款金额中加入手续费。

### 属性查找机制
继承中的属性查找遵循以下规则：
1. **在子类中查找**：首先检查子类是否定义了该属性或方法。
2. **在父类中查找**：如果子类中没有定义，则继续在父类中查找。
3. **递归查找**：如果父类本身也继承自另一个类，则继续向上查找，直到找到属性或引发 `AttributeError`。

### 示例：CheckingAccount 类
```python
class CheckingAccount(Account):
    withdraw_fee = 1  # 提款手续费
    interest = 0.01  # 利率较低

    def withdraw(self, amount):
        # 提款时收取手续费
        return super().withdraw(amount + self.withdraw_fee)
```
在这个例子中，`CheckingAccount` 继承了 `Account` 类，重写了 `withdraw` 方法，但保留了其他未修改的功能（如存款功能）。

### 示例运行
```python
ch = CheckingAccount('Tom')
print(ch.interest)  # 输出 0.01
ch.deposit(100)  # 使用继承自父类的存款方法
ch.withdraw(20)  # 提款时会扣除手续费
```





## 属性查找与继承

在 Python 的继承体系中，属性查找的机制遵循以下步骤：
1. **实例属性查找**：首先查找实例本身是否有该属性。
2. **类属性查找**：如果实例没有该属性，则在类中查找。
3. **基类查找**：如果类也没有定义该属性，则在基类中递归查找。

当我们创建一个子类（如 `CheckingAccount`）的实例时，Python 会遵循上述步骤来查找并调用合适的属性和方法。

### 创建子类 `CheckingAccount`
当我们创建 `CheckingAccount` 的实例时，假设传入了 `Tom` 作为账户持有人。如果子类 `CheckingAccount` 没有定义 `__init__` 方法，Python 会在父类 `Account` 中查找，并调用父类的 `__init__` 来初始化实例：
```python
ch = CheckingAccount('Tom')
```
即使 `CheckingAccount` 没有自己的 `__init__`，它会继承 `Account` 的 `__init__`，为 `Tom` 设置初始余额为 0。

## 方法的查找与调用

### 存款方法 `deposit`
在 `CheckingAccount` 中，没有定义 `deposit` 方法，因此当调用 `deposit` 时，Python 会在父类 `Account` 中查找：
```python
ch.deposit(20)  # 在父类 Account 中找到 deposit 方法并执行
```
此时，`deposit` 方法会被绑定到 `CheckingAccount` 实例 `ch`，即 `self` 作为第一个参数传递给 `deposit`，实现将 $20 存入账户。

### 重写的提款方法 `withdraw`
在 `CheckingAccount` 类中，我们重写了父类的 `withdraw` 方法，添加了提款手续费。调用时，Python 会优先在子类中查找方法：
```python
ch.withdraw(10)  # 在 CheckingAccount 类中找到重写的 withdraw 方法
```
此方法会调用 `super().withdraw()`，即父类的 `withdraw` 方法，并在提款金额中加入手续费。调用结果会显示提款 $10 后再扣除 $1 手续费。

### 属性查找与重写
在继承体系中，子类可以重写父类的属性。例如，`CheckingAccount` 类重写了 `interest` 属性，将其设为 `0.01`：
```python
class CheckingAccount(Account):
    interest = 0.01  # 重写父类的 interest 属性
    withdraw_fee = 1  # 提款手续费
```
当访问 `CheckingAccount` 实例的 `interest` 属性时，Python 会在 `CheckingAccount` 类中找到重写的值 `0.01`。

### 使用父类方法与避免代码重复
继承的一个重要原则是避免代码重复。通过继承，我们可以重用父类的实现，而不必重复编写相同的代码。例如，在 `CheckingAccount` 的 `withdraw` 方法中，我们通过 `super()` 调用父类的 `withdraw` 方法，而不是重新实现所有的提款逻辑：
```python
def withdraw(self, amount):
    return super().withdraw(amount + self.withdraw_fee)  # 调用父类 withdraw 并添加手续费
```

![QQ_1726463366426]({{ site.baseurl }}/docs/assets/QQ_1726463366426.png)

### 属性查找顺序的动态性

属性查找是动态的，即使在实例创建之后，类的属性发生了变化，实例的属性查找仍然会反映最新的类属性值。例如，如果修改 `Account` 类的 `interest` 属性，所有未定义 `interest` 实例属性的实例都会反映这一变化：
```python
Account.interest = 0.05
print(ch.interest)  # 输出 0.01，因为 CheckingAccount 重写了 interest 属性
```

如果在 `Account` 类上修改 `interest` 属性，所有没有重写 `interest` 的实例都会反映新的值。

### 设计建议
1. **避免代码重复**：通过继承，使用父类的方法和属性，减少重复代码。
2. **实例优先**：在实例中优先查找属性，保证子类和实例的灵活性。
3. **使用 `super()`**：在子类中重用父类方法时，使用 `super()` 来调用父类的实现，保证继承结构的可维护性。



## 继承与组合的设计决策

在面向对象编程中，**继承（Inheritance）**和**组合（Composition）**是两种重要的设计模式。它们分别用于不同的场景。

### 继承（Inheritance）
继承用于表示**“是一个”（is-a）**的关系。例如：
- `CheckingAccount` 是 `Account` 的一种，因此它可以从 `Account` 继承。
- `CheckingAccount` 拥有 `Account` 类的所有属性和方法，但可以增加或重写某些行为。

在 `CheckingAccount` 的例子中，我们继承了 `Account` 的 `deposit` 方法，但重写了 `withdraw` 方法来添加提款手续费。这种设计使得 `CheckingAccount` 保留了 `Account` 的大部分功能，同时又可以增加特定的行为。

### 组合（Composition）
组合用于表示**“有一个”（has-a）**的关系。在这种模式下，一个对象作为另一个对象的属性。例如，一个**银行（Bank）**拥有多个账户（`Account`）：
- 银行不会从 `Account` 类继承，而是将 `Account` 作为银行的一个属性。

在组合中，一个类持有另一个类的实例。例如，银行拥有账户，但银行不是账户的一种：
```python
class Bank:
    def __init__(self):
        self.accounts = []

    def open_account(self, holder, amount, account_type=Account):
        account = account_type(holder)
        account.deposit(amount)
        self.accounts.append(account)
        return account
```
在这里，`Bank` 类通过组合持有 `Account` 的实例，并且通过 `open_account` 方法来为不同持有者创建账户。

## 设计银行类的功能
让我们实现一个简单的银行系统，允许创建账户并支付利息。银行使用组合模式来管理账户，并提供相关操作。

### 银行的操作
- **开户**：银行可以为持有人创建不同类型的账户（如普通账户或支票账户），并存入初始金额。
- **支付利息**：银行可以为所有账户支付利息。

### 示例实现
```python
class Bank:
    def __init__(self):
        self.accounts = []  # 组合：银行管理多个账户

    def open_account(self, holder, amount, account_type=Account):
        account = account_type(holder)  # 创建账户（普通账户或支票账户）
        account.deposit(amount)  # 存入初始金额
        self.accounts.append(account)  # 将账户添加到银行的账户列表中
        return account

    def pay_interest(self):
        for account in self.accounts:
            interest = account.balance * account.interest  # 利率计算
            account.deposit(interest)  # 存入利息
```

### 使用银行类
通过银行类，我们可以创建多个账户，并为每个账户支付利息：
```python
bank = Bank()
john_account = bank.open_account('John', 10)  # 创建普通账户
jack_account = bank.open_account('Jack', 5, CheckingAccount)  # 创建支票账户

bank.pay_interest()  # 支付利息
print(john_account.balance)  # 输出 John 的账户余额，增加了 2% 的利息
print(jack_account.balance)  # 输出 Jack 的账户余额，增加了 1% 的利息
```
在此示例中，`john_account` 是普通账户，利率为 2%，而 `jack_account` 是支票账户，利率为 1%。

### 组合与继承的使用建议
- **继承**：用于表示**“是一个”**的关系，如 `CheckingAccount` 是 `Account` 的一种。因此，`CheckingAccount` 继承自 `Account`，并重写了一些方法。
- **组合**：用于表示**“有一个”**的关系，如银行管理账户，银行拥有多个账户，但银行本身不是账户的一种。因此，银行使用组合模式，而不是继承。

## Attributes Lookup Practice

## 分析类声明

![QQ_1726463382383]({{ site.baseurl }}/docs/assets/QQ_1726463382383.png)

假设我们有三个类 `A`、`B` 和 `C`，其中 `B` 继承自 `A`，而 `C` 继承自 `B`。每个类定义了自己的属性和方法，某些属性和方法被子类重写。

```python
class A:
    z = -1
    def f(self, x):
        return B(x-1)

class B(A):
    n = 4
    def __init__(self, y):
        if y:
            self.z = self.f(y)
        else:
            self.z = C(y+1)

class C(B):
    def f(self, x):
        return x

```

1. **类A**：定义了一个类属性 `z = -1`，并且有一个方法 `f(self, x)`，该方法返回一个新的 `B` 类实例，传入参数 `x-1`。
   
2. **类B**继承了类A：定义了一个类属性 `n = 4`，并且有自己的构造函数 `__init__`，该函数根据传入的 `y` 值决定如何为 `self.z` 赋值。如果 `y` 是True（非零），则调用 `self.f(y)`，否则使用 `C(y+1)`。
3. **类C**继承了类B：重写了 `f(self, x)` 方法，简单地返回 `x`。

## 对象实例化与属性查找：

```python
a = A()
b = B(1)
b.n = 5
```

你提出的修正思路是正确的，我们可以更详细地解释 `a = A()` 和 `b = B(1)` 的具体过程。以下是详细的说明和修正后的解释：

### 1. **`a = A()`**：
- 创建了 `A` 类的一个实例 `a`。由于 `A` 类没有定义 `__init__` 方法，因此实例 `a` 并不会有任何实例属性。此时，`a` 只会继承 `A` 类的类属性 `z = -1`，并且可以调用 `A` 类的方法 `f`。

### 2. **`b = B(1)`**：
- 调用了 `B` 类的 `__init__` 方法，传递 `1` 作为 `y` 参数，进入 `B` 类的构造函数 `__init__`。具体过程如下：
  1. 因为 `y = 1` 是 `True`，所以进入 `if y:` 分支，执行 `self.z = self.f(y)`。
  2. 调用 `self.f(1)`，此时 `self.f` 是类 `A` 的方法 `f`（因为类 `B` 没有重写 `f` 方法，而继承自 `A`）。因此，`A.f` 方法会被调用，`self.f(1)` 相当于 `A.f(self, 1)`。
  3. `A.f` 方法返回一个 `B(x-1)`，其中 `x = 1`，所以实际调用的是 `B(0)`。
  
### 3. **`B(0)`** 的处理：
- 当递归调用 `B(0)` 时，再次进入 `B` 类的构造函数 `__init__`，但这次 `y = 0`，进入 `else` 分支，执行 `self.z = C(y+1)`，即 `self.z = C(1)`。
- `C(1)` 创建了一个 `C` 类的实例。`C` 继承自 `B`，而 `C` 重写了 `f` 方法，因此接下来 `C(1)` 的 `self.z` 值由 `C` 类的 `f` 方法决定。
  1. `C(1)` 调用 `C` 类的 `f(1)`，该方法直接返回 `x`，即 `1`。因此，`self.z = 1`。

### 4. **`b.z` 的最终值**：
- 递归回到 `B(1)` 的构造函数中，此时 `self.z` 被赋值为 `B(0)` 返回的结果，而 `B(0)` 调用了 `C(1)` 并将 `self.z` 设置为 `1`。因此，`b.z` 的最终值为 `1`。

### 5. `b.n = 5` 

- `b.n` 继承自类 `B`，初始值为 `4`，后被赋值为 `5`。

## 属性查找流程

在Python中，属性的查找遵循**从实例到类**的顺序。也就是说，Python首先会在实例本身查找属性，如果找不到，再去类中查找。如果在类中也找不到，还会继续沿着继承链往上查找，直到找到属性或终止。

### 1. **`C(2).n` 的属性查找过程：**

- `C(2)` 创建了一个 `C` 类的实例。
- 类 `C` 继承了 `B` 的类属性 `n = 4`。
- 因为实例 `C(2)` 没有自己的 `n` 属性，Python 会沿着继承链向上查找，在类 `C` 中没有找到 `n`，继续在类 `B` 中找到了 `n`，值为 `4`。
- 因此，**`C(2).n`** 的结果为 `4`。

### 2. **`a.z == C.z` 的属性查找过程：**

- **`a.z`**：
  - `a` 是 `A` 类的实例。`A` 没有定义 `__init__` 方法，也没有设置实例属性 `z`，因此 `a` 没有实例属性 `z`。
  - Python接着在类 `A` 中查找，找到了类属性 `z = -1`。
  - 因此，`a.z` 的值为 `-1`。
  
- **`C.z`**：
  - `C` 是 `B` 的子类，`B` 又是 `A` 的子类。类 `C` 没有定义 `z` 属性，因此Python会沿着继承链向上查找。
  - 类 `B` 也没有 `z` 属性，继续在类 `A` 中找到了类属性 `z = -1`。
  - 因此，`C.z` 的值也是 `-1`。

- 由于 **`a.z` 和 `C.z`** 都是从类 `A` 继承的类属性，值相同，**`a.z == C.z`** 的结果为 **`True`**。

### 3. **`a.z == b.z` 的属性查找过程：**

- **`a.z`**：
  - 如前所述，`a` 是 `A` 类的实例，`a.z` 查找到类 `A` 的类属性 `z = -1`，因此 `a.z = -1`。

- **`b.z`**：
  - `b` 是 `B(1)` 的实例。前面提到递归调用后`b.z` 被赋值为了 `1`。
  
- **比较**：
  - `a.z = -1`，`b.z = 1`，二者不相等。
  - 因此，**`a.z == b.z`** 的结果为 **`False`**。

## 多重继承与方法解析顺序

在 Python 中，多重继承允许一个类从多个父类继承属性和方法。虽然这是一个强大的功能，但也会增加代码的复杂性，特别是在处理方法解析顺序（MRO，Method Resolution Order）时。下面我们通过一个具体的例子来解释如何处理多重继承。

### 多重继承的实际例子

我们来设计一个新的银行账户类型，称为 **AsSeenOnTVAccount**。该账户结合了 **CheckingAccount** 和 **SavingsAccount** 的特性，具备一些特别的功能，例如有提款和存款手续费，同时开户时还会有免费一美元的奖励。

```python
class CheckingAccount(Account):
    withdraw_fee = 1  # 提款手续费
    interest = 0.01  # 利率为1%

    def withdraw(self, amount):
        return super().withdraw(amount + self.withdraw_fee)

class SavingsAccount(Account):
    deposit_fee = 2  # 存款手续费
    interest = 0.02  # 利率为2%

    def deposit(self, amount):
        return super().deposit(amount - self.deposit_fee)

class AsSeenOnTVAccount(CheckingAccount, SavingsAccount):
    def __init__(self, holder):
        super().__init__(holder)
        self.balance += 1  # 开户时赠送1美元
```

### 方法解析顺序（MRO）
当我们创建 `AsSeenOnTVAccount` 的实例并调用它的 `deposit` 或 `withdraw` 方法时，Python 会根据类的**方法解析顺序**来决定应该调用哪个父类的方法。

例如：
```python
account = AsSeenOnTVAccount('John')
account.deposit(20)  # 实际存入 20 - 2 = 18 美元
account.withdraw(5)  # 实际扣掉 5 + 1 = 6 美元
```

- **存款时**：`deposit` 方法首先在 `AsSeenOnTVAccount` 中查找，但没有找到，于是继续查找 `SavingsAccount`，找到并执行了 `SavingsAccount` 的 `deposit` 方法，扣除 $2 存款手续费。
- **提款时**：`withdraw` 方法首先在 `AsSeenOnTVAccount` 中查找，找到 `CheckingAccount` 的 `withdraw` 方法，执行时扣除 $1 提款手续费。

![QQ_1726463413219]({{ site.baseurl }}/docs/assets/QQ_1726463413219.png)

### MRO 的工作方式

Python 中的方法解析顺序是由 `C3 线性化算法` 决定的，它遵循以下规则：
1. **子类优先**：先查找子类本身是否定义了该方法。
2. **从左到右**：如果子类没有定义，则按继承列表从左到右查找父类。
3. **深度优先**：如果一个父类继承了其他类，继续在它的父类中递归查找。

可以通过 `mro()` 方法查看类的解析顺序：
```python
print(AsSeenOnTVAccount.mro())
```

输出：
```python
[<class '__main__.AsSeenOnTVAccount'>, <class '__main__.CheckingAccount'>, <class '__main__.SavingsAccount'>, <class '__main__.Account'>, <class 'object'>]
```
这表明，当我们调用 `AsSeenOnTVAccount` 的方法时，Python 会依次查找：
1. `AsSeenOnTVAccount`
2. `CheckingAccount`
3. `SavingsAccount`
4. `Account`
5. 最终回到 `object`

### 多重继承的潜在问题
尽管多重继承功能强大，但它也容易导致代码的复杂性和维护困难。特别是当多个父类拥有相同的方法或属性时，可能会产生混淆。因此，在设计类时应该谨慎使用多重继承。

![QQ_1726463447461]({{ site.baseurl }}/docs/assets/QQ_1726463447461.png)

### 使用组合代替继承
对于某些场景，**组合**是一种更简单的选择。例如，银行可以包含多个账户，而不必通过继承来实现。组合方式更加清晰，避免了多重继承的复杂性。

```python
class Bank:
    def __init__(self):
        self.accounts = []

    def add_account(self, account):
        self.accounts.append(account)
```



