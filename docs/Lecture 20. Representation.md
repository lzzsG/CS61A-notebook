# Lecture 20. Representation

## Announcements

### 1. 实验和作业的截止日期及项目更新

- **实验截止时间：**今天
- **作业截止时间：**周四
- **Ants 项目：**已经发布，截止日期为下周五，并且下周二有一个检查点。
  - 提前提交的奖励：如果在周四之前提交项目，将获得额外加分。
  - 项目中包含额外的加分问题。如果你希望获得加分，需要在周四之前完成该问题。

### 2. 指导小组和办公时间
- **指导小组：** 周四上午11点至12点，将有部分课程助教为学生提供关于课程内容以及伯克利学习体验的指导和答疑。届时，你可以向小组成员提问并听取他们的答复。
- **办公时间：** 每周五有与课程无关的内容咨询时间，如果你有相关疑问，可以预约一对一帮助。

### 3. 调查问卷
- **匿名调查：** 课程进行的反馈调查问卷已经发布。该问卷并非必填，但希望在下周一之前完成，以便教学团队了解课程的进展和学生的感受。

### 4. 期中考试提醒
- **期中考试二：** 将于9月28日（周三）晚上7点举行。考试形式和第一场期中考试相似，涵盖内容截至本周五的课程。

## String Representations 

## 字符串表示与面向对象编程（OOP）

**字符串表示的重要性：** 在面向对象编程中，一个对象应该能够表现出它所代表的数据类型的行为之一，尤其是能够将自身转化为一个字符串形式以供其他系统或用户使用。字符串不仅用于自然语言的交流，也常见于编程语言中。

**Python 中的字符串表示机制：** Python 中的对象有两种字符串表示：

1. **`__str__`**：面向人类可读的字符串表示，通常用于输出给用户。
2. **`__repr__`**：面向 Python 解释器的表示，通常用于调试，输出结果是一个合法的 Python 表达式。

### **`__repr__` 的用途：**

- 调用 `repr()` 函数时，返回对象的 "规范字符串表示"。即该字符串可以通过 `eval()` 函数重新生成与原对象相等的对象。
- `__repr__` 是在 Python 交互式会话中，直接显示结果时的默认输出。
- 对于简单的数据类型（如整数或浮点数），`__repr__` 和 `__str__` 通常一致。然而，对于复杂对象（如函数或类），它们的 `__repr__` 输出则往往会使用角括号 `<>` 来表示，这不是一个有效的 Python 表达式，而是一种方便人类理解的描述。

### **`__str__` 的用途：**

- `str()` 函数用于生成对象的 "人类可读字符串表示"。这通常用于用户界面或日志记录等场景。
- 例如，Python 的 `fractions` 模块中的 `Fraction` 类，`__repr__` 返回的形式是创建该对象的代码表达式，如 `Fraction(1, 2)`，而 `__str__` 则会返回更符合人类习惯的表示形式，如 `1/2`。

### `__repr__` 和 `__str__` 的区别
- **`__repr__` 方法：**  
  调用 `repr()` 函数时，`Fraction` 类的对象会返回这样的字符串表示：`Fraction(1, 2)`，这是构造该对象时的代码表达式。这种表示方式是面向 Python 解释器的，旨在生成能够重新构造该对象的表达式。
  
- **`__str__` 方法：**  
  当调用 `str()` 函数或使用 `print()` 输出对象时，`Fraction` 类的对象将返回 `1/2` 这样的字符串形式。这种表示方式更符合人类的直观理解，强调面向用户的可读性。

- **示例：**
  ```python
  from fractions import Fraction
  
  half = Fraction(1, 2)
  
  print(repr(half))  # 输出：Fraction(1, 2)
  print(str(half))   # 输出：1/2
  ```

  - 当调用 `repr(half)` 时，返回的是一个可以重新构造该对象的字符串表达式。
  - 当调用 `print(half)` 或 `str(half)` 时，返回的是一个更符合人类书写习惯的表达形式。

### 字符串与 `repr`、`str` 的作用
**字符串的 `repr` 和 `str`：**

- 当我们处理字符串时，`repr()` 和 `str()` 的表现不同。`repr()` 会显示带引号的字符串，而 `str()` 输出时则不会显示引号。

- 示例：
  ```python
  s = "hello, world"
  
  print(repr(s))  # 输出："hello, world"
  print(str(s))   # 输出：hello, world
  ```

- `repr(s)` 输出的字符串包含引号，是为了明确表示这是一个字符串对象。`str(s)` 则直接输出字符串内容，省去了引号。

- 如果我们不断调用 `repr()`，例如 `repr(repr(s))`，我们会看到越来越多的引号和转义符，表明这些是嵌套的字符串表示。多次调用 `repr()` 可能会导致复杂的嵌套表示，但最终都能通过 `eval()` 恢复成原始字符串。

### `repr` 和 `str` 的多态性
- **多态函数：**  
  Python 中的 `repr()` 和 `str()` 是多态函数，它们能够接受各种不同类型的对象并返回相应的字符串表示。这是因为这些函数内部会调用对象定义的 `__repr__` 或 `__str__` 方法，而这些方法是根据具体类型来定义的。

  - **`repr()` 的工作原理：**  
    调用 `repr()` 时，Python 实际上会调用对象的 `__repr__` 方法。该方法通常是通过查找类属性的方式实现的，因此它总是会返回类定义的 `__repr__` 方法，而忽略实例属性。

    - 实现方式：
      ```python
      def my_repr(x):
          return type(x).__repr__(x)
      ```

      这段代码通过 `type(x)` 获取对象 `x` 的类，并调用类的 `__repr__` 方法。这个实现确保了它查找的是类的属性，而不是实例属性。

  - **`str()` 的工作原理：**  
    同样，`str()` 函数会调用对象的 `__str__` 方法，生成面向人类的字符串表示。

- **忽略实例属性：**  
  当调用 `repr()` 时，它只会查找类定义的 `__repr__` 方法，而不会使用实例属性的同名方法。这样可以确保 `repr()` 总是调用类的通用方法。

  总结

###  `__repr__` 和 `__str__` 的实现细节
- **类属性与实例属性的区别：**
  - 当调用 `repr()` 时，Python 会忽略实例属性 `__repr__`，只查找类属性 `__repr__`。这保证了即使实例中有同名属性，`repr()` 也不会使用它，而是依赖类中定义的 `__repr__` 方法。这样可以确保对象的规范字符串表示始终由类定义，而不是实例临时覆盖。
  
  - **示例：**
    ```python
    class Bear:
        def __repr__(self):
            return "Bear"
    
    oski = Bear()
    print(repr(oski))  # 输出：Bear
    ```

  - 在这个例子中，尽管实例 `oski` 可以有自己的属性，`repr()` 依然只查找类 `Bear` 中的 `__repr__` 方法，而不会检查实例中的属性。

- **`__str__` 的默认行为：**
  - 如果类没有定义 `__str__` 方法，Python 会默认调用 `__repr__` 方法。这意味着在未显式区分两者时，它们的行为是相同的。只有当我们为类定义了 `__str__`，它们的表现才会不同。
  
  - **示例：**
    ```python
    class Bear:
        def __repr__(self):
            return "Bear"
        def __str__(self):
            return "A bear"
    
    oski = Bear()
    print(oski)           # 输出：A bear
    print(str(oski))      # 输出：A bear
    print(repr(oski))     # 输出：Bear
    ```

  - 通过定义 `__str__`，我们可以控制 `print()` 或 `str()` 输出的内容，而 `repr()` 仍会调用 `__repr__` 方法。

### 类的实例与类方法的调用
- **实例属性与类方法的区别：**
  - 当调用类方法时，Python 首先会在类的层级中查找方法，而不会考虑实例中的同名属性。这可以确保方法调用的一致性，即使实例中存在同名属性也不会影响类的行为。

  - **示例：**
    ```python
    class Bear:
        def __repr__(self):
            return "Bear"
        def __str__(self):
            return "A bear"
    
    oski = Bear()
    oski.__repr__ = lambda: "Instance of Bear"
    
    print(repr(oski))  # 输出：Bear，实例属性被忽略
    ```

  - 在这个例子中，虽然我们为 `oski` 实例定义了自己的 `__repr__` 属性，但 `repr(oski)` 仍然调用的是类的 `__repr__` 方法。

### 接口的概念
- **接口（Interface）：**  
  接口是指一组类共享的属性或方法。通过定义相同的方法名，不同的类可以实现相似的行为，而无需关心类的内部实现。这种机制极大地提高了代码的抽象性和灵活性。

- **接口的例子：**
  
  - `__repr__` 和 `__str__` 就是 Python 中的接口。任何类都可以实现这些方法，从而为对象提供特定的字符串表示。这种接口机制允许不同的类在同样的上下文中表现出一致的行为。
  
  - **类定义与初始化：**
    创建一个 `Ratio` 类，该类接收两个参数：**分子**和**分母**。为了确保类的实例可以被清晰地表示，我们需要实现 `__repr__` 和 `__str__` 方法。
    
    - **`__repr__`** 方法用于生成面向 Python 解释器的表示，返回类名和构造表达式。
    - **`__str__`** 方法则返回人类可读的分数形式。
    
    ```python
    class Ratio:
        def __init__(self, numerator, denominator):
            self.numerator = numerator
            self.denominator = denominator
        
        def __repr__(self):
            return f"Ratio({self.numerator}, {self.denominator})"
        
        def __str__(self):
            return f"{self.numerator}/{self.denominator}"
    
    r = Ratio(3, 4)
    print(repr(r))  # 输出：Ratio(3, 4)
    print(str(r))   # 输出：3/4
    ```
    
  - `Ratio` 类实现了 `__repr__` 和 `__str__` 接口，使得它的实例在不同的上下文中可以表现出不同的字符串表示形式。

## 特殊方法名与 Python 内置行为

- Python 的某些方法名具有特殊的含义，例如 `__init__`、`__repr__` 和 `__str__` 等，它们与 Python 的内置对象系统交互，自动触发某些行为。
  
- **`__add__` 方法：**
  `__add__` 是一个特殊的两参数方法，用于在对象之间执行加法运算。如果想让 `Ratio` 类的实例支持加法运算，需要实现 `__add__` 方法。

  **示例：**
  
  ```python
  class Ratio:
      def __init__(self, numerator, denominator):
          self.numerator = numerator
          self.denominator = denominator
      
      def __repr__(self):
          return f"Ratio({self.numerator}, {self.denominator})"
      
      def __str__(self):
          return f"{self.numerator}/{self.denominator}"
  
      def __add__(self, other):
          # 计算新分子和分母
          new_numerator = (self.numerator * other.denominator + 
                           self.denominator * other.numerator)
          new_denominator = self.denominator * other.denominator
          # 返回新创建的 Ratio 对象
          return Ratio(new_numerator, new_denominator)
  ```
  
  - 通过这个 `__add__` 方法，我们可以对 `Ratio` 对象进行加法运算。
  
  **示例：**
  ```python
  r1 = Ratio(1, 3)
  r2 = Ratio(1, 6)
  r3 = r1 + r2
  print(r3)  # 输出：9/18
  ```

### 使用 `__add__` 和 `__radd__`

- Python 还提供了 `__radd__` 方法，处理左右两侧对象的顺序问题。通常对于数值类型，加法是可交换的，因此 `__radd__` 和 `__add__` 是等价的，但在某些自定义对象中，顺序可能会影响结果。

- **`__radd__` 方法的实现：**
  ```python
  def __radd__(self, other):
      return self.__add__(other)
  ```

  这样一来，无论是左边还是右边是 `Ratio` 对象，结果都能正确计算。

### 扩展：使用最大公约数 (GCD) 简化分数

- 如果我们想要将分数化简成最简形式，可以使用 **最大公约数**（GCD）来约分。可以实现一个辅助函数来计算 GCD，并在加法运算后化简结果。

  **GCD 函数的实现：**
  ```python
  def gcd(a, b):
      while b:
          a, b = b, a % b
      return a
  ```

  **在 `Ratio` 类中使用 GCD：**
  ```python
  def __add__(self, other):
      new_numerator = (self.numerator * other.denominator +
                       self.denominator * other.numerator)
      new_denominator = self.denominator * other.denominator
      # 使用 gcd 约分
      common_divisor = gcd(new_numerator, new_denominator)
      return Ratio(new_numerator // common_divisor, new_denominator // common_divisor)
  ```

  **示例：**
  ```python
  r1 = Ratio(1, 3)
  r2 = Ratio(1, 6)
  r3 = r1 + r2
  print(r3)  # 输出：1/2
  ```

  在这个例子中，`1/3 + 1/6` 结果会被简化为 `1/2`。

## 在 `Ratio` 类中支持不同类型的加法

### 类型检查与调度
- **问题：** 当我们尝试将一个 `Ratio` 对象与整数或其他类型的对象相加时，需要根据另一个对象的类型决定如何处理。可以通过类型检查来实现这一点。
- **解决方案：** 通过检查 `other` 的类型，我们可以为不同类型的对象执行不同的加法逻辑。如果 `other` 是整数，则将其视为分母为 1 的 `Ratio` 进行相加。如果 `other` 是浮点数，则需要进行类型转换并返回浮点值。

### `__add__` 方法扩展
```python
class Ratio:
    def __init__(self, numerator, denominator):
        self.numerator = numerator
        self.denominator = denominator
    
    def __repr__(self):
        return f"Ratio({self.numerator}, {self.denominator})"
    
    def __str__(self):
        return f"{self.numerator}/{self.denominator}"
    
    def __add__(self, other):
        if isinstance(other, Ratio):
            # 添加两个 Ratio 对象
            new_numerator = (self.numerator * other.denominator +
                             self.denominator * other.numerator)
            new_denominator = self.denominator * other.denominator
            gcd_value = gcd(new_numerator, new_denominator)
            return Ratio(new_numerator // gcd_value, new_denominator // gcd_value)
        
        elif isinstance(other, int):
            # 如果是整数，将其视为分母为 1 的 Ratio
            new_numerator = self.numerator + other * self.denominator
            gcd_value = gcd(new_numerator, self.denominator)
            return Ratio(new_numerator // gcd_value, self.denominator // gcd_value)
        
        elif isinstance(other, float):
            # 如果是浮点数，将 Ratio 转换为浮点数并执行加法
            return float(self) + other
    
    def __radd__(self, other):
        return self.__add__(other)
    
    def __float__(self):
        # 将 Ratio 转换为浮点数
        return self.numerator / self.denominator
```

**示例：**

```python
r1 = Ratio(1, 3)
r2 = Ratio(1, 6)
print(r1 + r2)          # 输出：1/2，表示两个 Ratio 相加
print(r1 + 1)           # 输出：4/3，表示 Ratio 与整数相加
print(r1 + 0.5)         # 输出：0.8333...，表示 Ratio 与浮点数相加
print(1 + r1)           # 输出：4/3，支持右侧的加法
```

- **逻辑：**
  - 首先检查 `other` 的类型：
    - 如果是 `Ratio` 对象，则按前面介绍的加法公式相加。
    - 如果是整数，则将其视为分母为 1 的 `Ratio` 对象，并相加。
    - 如果是浮点数，则将 `Ratio` 转换为浮点数后执行加法。
  - `__radd__` 处理右侧操作，即当 `Ratio` 对象位于加号的右侧时，也能正常工作。
  - `__float__` 方法将 `Ratio` 对象转换为浮点数，方便与浮点数进行运算。

## 类型检查和类型转换（Type Dispatching 和 Type Coercion）
- **类型检查（Type Dispatching）：** 
  - 通过检查输入对象的类型，根据类型执行不同的操作。例如，在加法中，根据对象是否为 `int`、`float` 或 `Ratio` 来决定不同的相加方式。
  
- **类型转换（Type Coercion）：**
  - 当两种不同类型的对象需要一起操作时，将其中一个对象转换为另一种类型。例如，当 `Ratio` 对象与浮点数相加时，将 `Ratio` 转换为浮点数。

## 练习：实现 `Kangaroo` 类

我们需要实现一个 `Kangaroo` 类，用来模拟袋鼠的行为，尤其是袋鼠袋子的管理。袋鼠可以往袋子里放置物品，也可以查看袋子中的内容。

### 1. **构造函数：**

**要求：**
- `Kangaroo` 类的构造函数应初始化一个空列表 `pouch_contents`，用于存储袋子中的物品。

```python
class Kangaroo:
    def __init__(self):
        # 初始化袋子的内容为空列表
        self.pouch_contents = []
```

### 2. **`put_in_pouch` 方法的逻辑**

**要求：**
- 该方法的作用是将物品放入袋子中。在实现时，首先检查袋子中是否已经存在该物品。
- 如果物品已经存在，程序应打印提示信息，并且不再继续执行添加操作。
- 如果袋子中还没有该物品，则将它添加到 `pouch_contents` 列表中。

**逻辑步骤：**
1. **遍历袋子内容**：使用 `for` 循环遍历 `self.pouch_contents` 来检查该物品是否已经在袋子里。
2. **检查物品是否已存在**：使用 `==` 操作符比较当前的袋子内容与要放入的物品。
3. **添加物品**：如果遍历结束时没有找到重复的物品，则将物品添加到袋子中。

```python
    def put_in_pouch(self, item):
        # 遍历袋子内容，检查物品是否已存在
        for existing_item in self.pouch_contents:
            if existing_item == item:
                # 如果物品已存在，打印提示并返回
                print(f"{item} is already in the pouch.")
                return
        
        # 如果物品不在袋子中，则将其添加进去
        self.pouch_contents.append(item)
```

### 3. **`__str__` 方法的逻辑**

**要求：**
- 该方法的作用是返回袋子中的物品列表的字符串表示。
- 如果袋子是空的，返回 `"The kangaroo's pouch is empty."`。
- 如果袋子里有物品，输出所有物品的列表，物品之间以逗号分隔。

**逻辑步骤：**
1. **检查袋子是否为空**：如果 `pouch_contents` 的长度为 0，返回提示信息表示袋子为空。
2. **打印袋子中的物品**：使用 `", ".join(self.pouch_contents)` 将列表中的物品连接成一个字符串并返回。

```python
    def __str__(self):
        if len(self.pouch_contents) == 0:
            # 如果袋子是空的，返回提示信息
            return "The kangaroo's pouch is empty."
        else:
            # 返回袋子中的物品，物品之间以逗号分隔
            return "The kangaroo's pouch contains: " + ", ".join(self.pouch_contents)
```

### 4. **测试驱动程序**

**要求：**
- 编写一个测试程序来测试 `Kangaroo` 类的基本功能。
- 测试袋子的初始化状态、添加物品、处理重复物品的情况以及正确显示袋子内容。

```python
# 测试驱动程序
k = Kangaroo()

# 输出：袋子应该是空的
print(k)  # 输出：The kangaroo's pouch is empty.

# 向袋子中添加一个物品
k.put_in_pouch("Ball")
print(k)  # 输出：The kangaroo's pouch contains: Ball

# 再次添加一个不同的物品
k.put_in_pouch("Hammer")
print(k)  # 输出：The kangaroo's pouch contains: Ball, Hammer

# 尝试重复添加相同的物品
k.put_in_pouch("Ball")  # 输出：Ball is already in the pouch.
print(k)  # 确认袋子中没有重复物品，输出：The kangaroo's pouch contains: Ball, Hammer
```

### 5. **注意点与测试**

- **验证物品是否重复**：在添加物品时，必须确保不会重复添加同样的物品。这通过在 `put_in_pouch` 方法中遍历袋子来实现。
- **测试覆盖范围**：
  - 测试袋子初始状态是否为空。
  - 测试添加单个物品和多个不同物品。
  - 测试重复添加物品时，确保不会重复添加并且程序能正确处理。

通过以上的代码，`Kangaroo` 类可以正常运行并通过基本的功能测试，确保 `put_in_pouch` 和 `__str__` 方法都实现了正确的逻辑。





