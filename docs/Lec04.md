---
layout: page
title: Lecture 4. Higher-Order Functions
permalink: /Lec04/
nav_order: 4



---

# Lecture 4. Higher-Order Functions



---

### 高阶函数（Higher-Order Functions）

#### 引言

函数是一种抽象工具，用来描述不依赖于具体参数值的复合操作。例如：

```python
def square(x):
    return x * x
```

函数 `square` 并不依赖于特定的数字，而是定义了一种获取任意数字平方的方法。如果没有函数定义，我们可以通过直接写表达式来计算平方，但这对于更复杂的操作来说会变得很麻烦。函数定义允许我们在更高的抽象层次上工作。

为了进一步提高抽象能力，我们需要一种“可以接收其他函数作为参数”或“可以返回函数”的函数。这种函数被称为高阶函数。高阶函数是强大的抽象工具，能够极大地提升编程语言的表达能力。

#### 1.6.1 作为参数的函数

考虑以下三个计算求和的函数：

1. 计算从 1 到 n 的自然数之和：

```python
def sum_naturals(n):
    total, k = 0, 1
    while k <= n:
        total, k = total + k, k + 1
    return total

print(sum_naturals(100))  # 输出：5050
```

2. 计算从 1 到 n 的自然数的立方和：

```python
def sum_cubes(n):
    total, k = 0, 1
    while k <= n:
        total, k = total + k**3, k + 1
    return total

print(sum_cubes(100))  # 输出：25502500
```

3. 计算特定数列的和，数列值会缓慢收敛到 π：

```python
def pi_sum(n):
    total, k = 0, 1
    while k <= n:
        total, k = total + 8 / ((4*k-3) * (4*k-1)), k + 1
    return total

print(pi_sum(100))  # 输出：3.1365926848388144
```

这三个函数的结构非常相似，主要区别在于计算被加项的方式。我们可以抽象出一个通用的求和模板：

```python
def summation(n, term):
    total, k = 0, 1
    while k <= n:
        total, k = total + term(k), k + 1
    return total
```

通过这种方式，我们可以将求和的具体计算方式作为参数传递给 `summation` 函数：

```python
def identity(x):
    return x

def sum_naturals(n):
    return summation(n, identity)

print(sum_naturals(10))  # 输出：55
```

`summation` 函数还可以直接调用，而无需定义特定的求和函数：

```python
def square(x):
    return x * x

print(summation(10, square))  # 输出：385
```

#### 高阶函数示例

我们可以定义 `pi_term` 函数来计算 π 的近似值：

```python
def pi_term(x):
    return 8 / ((4*x-3) * (4*x-1))

def pi_sum(n):
    return summation(n, pi_term)

print(pi_sum(1_000_000))  # 输出：3.141592153589902
```

#### 总结

高阶函数通过将函数作为参数或返回函数来实现更高层次的抽象，简化了代码，并增强了代码的复用性。总结其关键点：

1. **提高抽象层次**：允许我们在更高层次上工作，不必关注底层细节。
2. **代码复用**：通过抽象通用的操作模式，提高代码的复用性。
3. **简化代码**：减少重复代码，使代码更简洁、更易读。

高阶函数是现代编程语言中的强大工具，充分利用它们可以使我们的代码更灵活、更易维护。





### 计算黄金比例的通用方法：迭代改进

#### 背景
黄金比例（phi）是一个接近 1.618 的常数，广泛存在于自然、艺术和建筑中。我们将使用一种通用的方法（函数）来计算黄金比例，这种方法称为迭代改进（iterative improvement）。

#### 迭代改进的通用方法

首先，我们定义一个通用的迭代改进函数 `improve`：

```python
def improve(update, close, guess=1):
    while not close(guess):
        guess = update(guess)
    return guess
```

- `update`: 用于改进当前猜测值的函数。
- `close`: 用于检查当前猜测值是否足够接近正确值的函数。
- `guess`: 初始猜测值，默认为 1。

`improve` 函数通过不断应用 `update` 函数来改进 `guess`，直到 `close` 函数返回 `True`。

#### 黄金比例的特性

黄金比例（phi）的一个特性是：
\[ \phi = 1 + \frac{1}{\phi} \]

这个特性可以通过反复叠加任何正数的倒数加上 1 来计算。我们利用这个特性定义 `golden_update` 函数：

```python
def golden_update(guess):
    return 1 / guess + 1
```

黄金比例的另一个特性是它的平方减去 1 等于它本身。我们用 `square_close_to_successor` 函数来表示这一特性：

```python
def square_close_to_successor(guess):
    return approx_eq(guess * guess, guess + 1)
```

#### 近似相等函数

为了比较两个数是否近似相等，我们定义一个 `approx_eq` 函数：

```python
def approx_eq(x, y, tolerance=1e-15):
    return abs(x - y) < tolerance
```

#### 使用迭代改进计算黄金比例

通过将 `golden_update` 和 `square_close_to_successor` 作为参数传递给 `improve` 函数，我们可以计算黄金比例的近似值：

```python
result = improve(golden_update, square_close_to_successor)
print(result)  # 输出：1.618033988749895
```

#### 计算过程追踪

让我们一步一步追踪 `improve` 函数的计算过程：

1. 初始 `guess` 为 1。
2. 检查 `close(guess)`，即 `square_close_to_successor(1)`，返回 `False`，因为 \(1 \times 1\) 不等于 \(1 + 1\)。
3. 改进 `guess`：`guess = golden_update(1)`，返回 `2.0`。
4. 再次检查 `close(guess)`：`square_close_to_successor(2.0)`，返回 `False`，因为 \(2.0 \times 2.0\) 不等于 \(2.0 + 1\)。
5. 继续改进 `guess`：`guess = golden_update(2.0)`，返回 `1.5`。
6. 再次检查 `close(guess)`：`square_close_to_successor(1.5)`，返回 `False`，因为 \(1.5 \times 1.5\) 不等于 \(1.5 + 1\)。
7. 继续改进 `guess`：`guess = golden_update(1.5)`，返回 `1.6666666666666665`。
8. 再次检查 `close(guess)`：`square_close_to_successor(1.6666666666666665)`，返回 `False`，因为 \(1.6666666666666665 \times 1.6666666666666665\) 不等于 \(1.6666666666666665 + 1\)。

这个过程继续下去，直到 `close(guess)` 返回 `True`，即 `guess` 足够接近黄金比例的值。

#### 完整代码

```python
def improve(update, close, guess=1):
    while not close(guess):
        guess = update(guess)
    return guess

def golden_update(guess):
    return 1 / guess + 1

def square_close_to_successor(guess):
    return approx_eq(guess * guess, guess + 1)

def approx_eq(x, y, tolerance=1e-15):
    return abs(x - y) < tolerance

result = improve(golden_update, square_close_to_successor)
print(result)  # 输出：1.618033988749895
```

通过以上方法，我们成功计算出黄金比例的有限近似值，并展示了迭代改进作为通用方法的强大抽象能力。





---





### 计算平方根的数学原理

计算平方根的方法有很多种，本文主要介绍牛顿法（Newton's method），也称为牛顿-拉弗森法（Newton-Raphson method）。这种方法利用迭代改进，逐步逼近平方根。

#### 牛顿法的基本思想

牛顿法用于求解方程 \(f(x) = 0\) 的根。对于平方根问题，我们希望找到一个数 \(x\)，使得 \(x^2 = a\)，即求解 \(f(x) = x^2 - a = 0\)。

牛顿法的迭代公式为：
\[ x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)} \]

对于 \(f(x) = x^2 - a\)，其导数 \(f'(x) = 2x\)，代入公式得到：
\[ x_{n+1} = x_n - \frac{x_n^2 - a}{2x_n} = \frac{x_n + \frac{a}{x_n}}{2} \]

这个公式表示，新猜测值是当前猜测值和 \(a\) 除以当前猜测值的平均值。

#### 迭代过程

1. 选择一个初始猜测值 \(x_0\)。
2. 根据公式计算新猜测值：
   \[ x_{n+1} = \frac{x_n + \frac{a}{x_n}}{2} \]
3. 重复步骤 2，直到猜测值的变化小于某个预设的容差值。

#### 平方根计算代码中的实现

```python
def improve(update, close, guess=1):
    while not close(guess):
        guess = update(guess)
    return guess

def average(x, y):
    return (x + y) / 2

def approx_eq(x, y, tolerance=1e-15):
    return abs(x - y) < tolerance

def sqrt(a):
    def sqrt_update(x):
        return average(x, a / x)
    
    def sqrt_close(x):
        return approx_eq(x * x, a)
    
    return improve(sqrt_update, sqrt_close)

result = sqrt(256)
print(result)  # 输出：16.0
```

在上面的代码中，`sqrt_update` 函数实现了牛顿法的迭代公式，`sqrt_close` 函数检查当前猜测值的平方是否接近目标值 `a`。



### 高阶函数：作为返回值的函数

高阶函数不仅可以接受其他函数作为参数，还可以返回一个函数作为其结果。通过创建“返回值是函数”的函数，我们可以实现更强大的表达能力，特别是当我们希望函数在不同的上下文中有不同的行为时。这种特性在带有词法作用域的编程语言中尤为重要，因为局部定义的函数在它们返回时仍旧持有所关联的环境。

#### 函数组合

函数组合（composition）是一种自然的编程方法，它允许我们将两个或多个函数组合在一起，形成一个新函数。例如，给定两个函数 `f(x)` 和 `g(x)`，我们可能想要定义 `h(x) = f(g(x))`。我们可以使用高阶函数来实现这一点：

```python
def compose1(f, g):
    def h(x):
        return f(g(x))
    return h
```

在这个示例中：
- `compose1` 是一个高阶函数，它接受两个函数 `f` 和 `g` 作为参数。
- 它返回一个新函数 `h`，这个函数应用 `g` 到输入 `x`，然后将结果传递给 `f`。

#### 环境模型

在解释高阶函数时，环境模型能够很好地展示函数如何解析名称。例如，在 `compose1` 中，`h` 函数能够正确解析 `f` 和 `g`，即使它们存在于不同的作用域中。这是因为 `h` 持有对定义它的环境的引用，即使在返回之后。

### 牛顿法示例

牛顿法（Newton's method）是一种用于查找函数零点的经典迭代方法。通过函数返回值和局部定义，我们可以简洁地实现这一算法。

##### 牛顿法基本原理

牛顿法用于求解方程 \( f(x) = 0 \) 的根。该方法通过线性近似逐步逼近函数的零点。具体步骤如下：
1. 选择一个初始猜测值 \( x_0 \)。
2. 通过公式 \( x_{n+1} = x_n - \frac{f(x_n)}{f'(x_n)} \) 计算新猜测值。
3. 重复步骤 2，直到结果收敛。

##### 实现牛顿法

我们首先定义一个更新函数 `newton_update`：

```python
def newton_update(f, df):
    def update(x):
        return x - f(x) / df(x)
    return update
```

然后使用 `improve` 算法来实现 `find_zero` 函数：

```python
def find_zero(f, df):
    def near_zero(x):
        return approx_eq(f(x), 0)
    return improve(newton_update(f, df), near_zero)
```

##### 计算平方根

我们可以使用牛顿法来计算平方根。平方根 \( \sqrt{a} \) 是使得 \( x^2 = a \) 的值。我们定义 `square_root_newton` 函数：

```python
def square_root_newton(a):
    def f(x):
        return x * x - a
    def df(x):
        return 2 * x
    return find_zero(f, df)

print(square_root_newton(64))  # 输出：8.0
```

##### 计算任意次方根

我们可以推广这一方法来计算任意次方根。给定 \( a \) 和 \( n \)，\( a \) 的 \( n \) 次方根是使得 \( x^n = a \) 的值。我们定义 `nth_root_of_a` 函数：

```python
def power(x, n):
    """返回 x 的 n 次方"""
    product, k = 1, 0
    while k < n:
        product, k = product * x, k + 1
    return product

def nth_root_of_a(n, a):
    def f(x):
        return power(x, n) - a
    def df(x):
        return n * power(x, n-1)
    return find_zero(f, df)

print(nth_root_of_a(2, 64))  # 输出：8.0
print(nth_root_of_a(3, 64))  # 输出：4.0
print(nth_root_of_a(6, 64))  # 输出：2.0
```









### 闭包（Closures）

闭包是指在其词法环境中引用了自由变量的函数。自由变量是指未在局部范围内定义的变量，而是来自外部环境。闭包使得这些变量的绑定得以保留，即使在外部函数已经执行完毕之后。

#### 闭包的定义

闭包包括以下三个部分：
1. 一个内部函数。
2. 内部函数所引用的外部函数的变量。
3. 外部函数返回内部函数。

通过这种方式，内部函数“记住”了它的定义环境，即使外部函数已经执行完毕。

#### 示例解释

在 `sqrt` 函数中，我们定义了 `sqrt_update` 和 `sqrt_close` 函数：

```python
def sqrt(a):
    def sqrt_update(x):
        return average(x, a / x)
    
    def sqrt_close(x):
        return approx_eq(x * x, a)
    
    return improve(sqrt_update, sqrt_close)
```

在这个示例中：
- `sqrt_update` 和 `sqrt_close` 是在 `sqrt` 函数内部定义的。
- 这两个内部函数引用了外部函数 `sqrt` 的参数 `a`。
- 当 `sqrt` 函数返回 `improve(sqrt_update, sqrt_close)` 时，内部函数仍然可以访问 `a`。

#### 闭包的作用

1. **数据封装**：闭包将数据（例如 `a`）与操作该数据的函数（例如 `sqrt_update` 和 `sqrt_close`）绑定在一起，形成一个封装单元。
2. **函数工厂**：闭包可以用来创建带有特定环境的函数。例如，不同的 `a` 值生成不同的平方根计算器。
3. **减少全局变量**：使用闭包可以避免污染全局命名空间，将变量的作用范围限制在函数内部。

#### 闭包示例

下面是一个简单的闭包示例：

```python
def make_multiplier(factor):
    def multiplier(x):
        return x * factor
    return multiplier

times2 = make_multiplier(2)
times3 = make_multiplier(3)

print(times2(5))  # 输出：10
print(times3(5))  # 输出：15
```

在这个示例中：
- `make_multiplier` 函数返回一个内部函数 `multiplier`。
- `multiplier` 引用了 `make_multiplier` 的参数 `factor`。
- `times2` 和 `times3` 是不同的闭包，它们各自记住了不同的 `factor` 值（2 和 3）。

通过理解和使用闭包，可以编写更灵活和模块化的代码，有效管理变量的作用范围，并实现复杂的功能。





---



# 1.6.6 柯里化

柯里化（Currying）是一种技术，它将一个接受多个参数的函数转换为一系列接受单个参数的函数。这在某些编程场景中非常有用，特别是当需要将函数应用于某些固定参数时。下面我们将详细介绍柯里化的概念和应用。

## 什么是柯里化？

柯里化是指将一个接受多个参数的函数转换为一系列接受单个参数的函数。例如，给定一个函数 `f(x, y)`，我们可以定义一个高阶函数 `g`，使得 `g(x)(y)` 等价于 `f(x, y)`。

### 示例：pow 函数的柯里化版本

我们可以将 `pow` 函数柯里化，使其接受一个参数 `x` 并返回另一个接受参数 `y` 的函数：

```python
def curried_pow(x):
    def h(y):
        return pow(x, y)
    return h

print(curried_pow(2)(3))  # 输出：8
```

在这个示例中：
- `curried_pow` 是一个高阶函数，它接受参数 `x` 并返回函数 `h`。
- 函数 `h` 接受参数 `y` 并返回 `pow(x, y)` 的结果。

## 柯里化的应用

柯里化在需要单参数函数的场景中非常有用。例如，Python 的 `map` 函数应用于一个可迭代对象时，需要一个单参数函数。通过柯里化，我们可以简化代码并提高复用性。

### 示例：map_to_range 函数

定义一个 `map_to_range` 函数，它将一个单参数函数应用于从 `start` 到 `end` 的一串值：

```python
def map_to_range(start, end, f):
    while start < end:
        print(f(start))
        start += 1

# 使用 curried_pow 和 map_to_range 计算 2 的前十次方
map_to_range(0, 10, curried_pow(2))
```

输出：
```
1
2
4
8
16
32
64
128
256
512
```

在这个例子中，我们使用 `curried_pow` 来生成一个计算 2 的幂次的函数，并将其应用于范围 `[0, 10)` 中的每个数字。

## 自动柯里化和逆柯里化

我们可以定义通用的柯里化和逆柯里化函数，来自动处理函数的柯里化和逆柯里化。

### 自动柯里化

定义一个 `curry2` 函数，将一个双参数函数转换为其柯里化版本：

```python
def curry2(f):
    """返回给定的双参数函数的柯里化版本"""
    def g(x):
        def h(y):
            return f(x, y)
        return h
    return g

# 测试自动柯里化
pow_curried = curry2(pow)
print(pow_curried(2)(5))  # 输出：32
map_to_range(0, 10, pow_curried(2))
```

### 逆柯里化

定义一个 `uncurry2` 函数，将柯里化的函数转换回双参数版本：

```python
def uncurry2(g):
    """返回给定的柯里化函数的双参数版本"""
    def f(x, y):
        return g(x)(y)
    return f

# 测试逆柯里化
print(uncurry2(pow_curried)(2, 5))  # 输出：32
```

### 总结

柯里化是一种强大的工具，特别是在函数式编程中。通过柯里化，我们可以创建更灵活的函数，并简化代码结构。在 Python 中，柯里化和逆柯里化可以帮助我们在需要单参数函数的场景中提高代码的复用性和简洁性。

通过这些例子和解释，我们可以更好地理解柯里化的概念及其应用。在实际编程中，掌握这些技巧将使我们能够编写更高效、更模块化的代码。



#### 为什么使用柯里化？

柯里化有以下几个主要优点：

1. **部分应用**：柯里化允许你固定一个函数的部分参数，然后返回一个新的函数，可以在稍后时间接受剩余的参数。这使得函数可以更灵活地组合和复用。

2. **函数式编程**：在函数式编程中，函数通常是单参数的，柯里化允许将多参数函数转换为多个单参数函数，以便于在函数式编程的环境中使用。

3. **简化代码**：在某些情况下，柯里化可以使代码更简洁、更易读。

#### 柯里化示例

假设我们有一个普通的双参数函数 `f(x, y)`：

```python
def add(x, y):
    return x + y

print(add(2, 3))  # 输出：5
```

如果我们将这个函数柯里化，那么我们将其转换为一系列单参数函数：

```python
def curried_add(x):
    def inner(y):
        return x + y
    return inner

# 使用柯里化函数
add_2 = curried_add(2)
print(add_2(3))  # 输出：5
print(curried_add(2)(3))  # 输出：5
```

在这里，`curried_add` 是一个高阶函数，它接受参数 `x`，并返回一个新函数 `inner`，这个新函数接受参数 `y` 并返回 `x + y` 的结果。

#### 对比普通函数和柯里化函数

普通函数：
```python
add(2, 3)  # 直接传递两个参数
```

柯里化函数：
```python
curried_add(2)(3)  # 先传递第一个参数，然后传递第二个参数
```

虽然看起来只是括号的位置不同，但柯里化函数提供了灵活性，可以部分应用参数：

```python
add_2 = curried_add(2)  # 部分应用第一个参数
print(add_2(3))  # 输出：5
```

#### 自动柯里化和逆柯里化

通过定义通用的柯里化和逆柯里化函数，我们可以自动将双参数函数转换为柯里化版本，或者将柯里化函数转换为普通版本。

```python
def curry2(f):
    """返回给定的双参数函数的柯里化版本"""
    def g(x):
        def h(y):
            return f(x, y)
        return h
    return g

def uncurry2(g):
    """返回给定的柯里化函数的双参数版本"""
    def f(x, y):
        return g(x)(y)
    return f

# 测试
def add(x, y):
    return x + y

curried_add = curry2(add)
print(curried_add(2)(3))  # 输出：5

uncurried_add = uncurry2(curried_add)
print(uncurried_add(2, 3))  # 输出：5
```

在上面的例子中，`curry2` 函数将一个双参数函数转换为其柯里化版本，而 `uncurry2` 函数将一个柯里化函数转换回双参数版本。

#### 总结

柯里化通过将多参数函数转换为一系列单参数函数，提供了函数部分应用的能力，使代码更灵活、更具复用性。在函数式编程中，柯里化是一个重要的工具，可以帮助简化代码结构，并使函数的组合更加自然。

虽然在语法上看起来只是括号的不同，但柯里化在实际编程中带来了很多便利，使得函数处理更加灵活和强大。理解柯里化及其应用，可以帮助我们更好地编写高效、简洁和模块化的代码。

---

# 1.6.7 Lambda 表达式

在编写代码时，我们通常会为函数命名，但有时候我们只需要一个临时函数，不想给它起名字。这时，我们可以使用 lambda 表达式来创建匿名函数。

## 什么是 Lambda 表达式？

Lambda 表达式是一种创建匿名函数的方式，这些函数只有一个返回表达式。它们没有名字，行为与普通函数相同。Lambda 表达式的语法如下：

```python
lambda 参数: 表达式
```

### 示例：使用 Lambda 表达式

以下是一个简单的 lambda 表达式示例，用于计算一个数的平方：

```python
square = lambda x: x * x
print(square(5))  # 输出：25
```

这里，`lambda x: x * x` 创建了一个匿名函数，并将其赋值给变量 `square`。我们可以像使用普通函数一样调用这个匿名函数。

### 组合函数示例

我们可以使用 lambda 表达式创建组合函数：

```python
def compose1(f, g):
    return lambda x: f(g(x))

# 示例使用
add_one = lambda x: x + 1
times_two = lambda x: x * 2
compose_fn = compose1(add_one, times_two)
print(compose_fn(3))  # 输出：7
```

在这个例子中，`compose1` 使用 lambda 表达式返回了一个组合函数，使 `compose_fn(3)` 等价于 `add_one(times_two(3))`。

## Lambda 表达式的优缺点

### 优点
1. **简洁**：可以在需要简单函数的地方直接使用，无需单独定义函数。
2. **灵活**：特别适用于一次性函数，比如 `map` 和 `filter` 的参数。

### 缺点
1. **可读性差**：过于复杂的 lambda 表达式可能难以理解。
2. **功能有限**：不能包含多行表达式或复杂的逻辑。

虽然 lambda 表达式可以使代码简洁，但在 Python 编程风格中，通常建议在需要复杂逻辑时使用 `def` 语句来定义函数，以提高代码的可读性和维护性。

## 历史背景

术语“lambda”源于 λ 演算（lambda calculus），这是计算机科学中的一个基础概念。Alonzo Church 在 1930 年代引入了这个符号，最初使用的是帽子符号（^），后来由于排版问题改成了希腊字母 λ。

# 1.6.8 抽象和一等函数

抽象是编程中的重要概念。用户定义函数是一种关键的抽象机制，因为它们可以将计算的一般方法表达为编程语言中的显式元素。

## 高阶函数

高阶函数是接受其他函数作为参数或返回函数的函数。它们使得我们能够创建更高级别的抽象。

### 一等函数的特权
在 Python 中，函数是一等公民（first-class citizens），这意味着：
1. **可以赋值给变量**。
2. **可以作为参数传递**。
3. **可以作为返回值**。
4. **可以存储在数据结构中**。

# 1.6.9 函数装饰器

函数装饰器（decorator）是一个用于在函数定义时修改函数行为的语法。装饰器是高阶函数的一种常见应用。

## 示例：trace 装饰器

以下是一个简单的装饰器示例，用于在函数调用时打印函数名和参数：

```python
def trace(fn):
    def wrapped(x):
        print(f'-> {fn.__name__}({x})')
        return fn(x)
    return wrapped

@trace
def square(x):
    return x * x

print(square(5))  # 输出：-> square(5) \n 25
```

在这个例子中，`@trace` 语法相当于 `square = trace(square)`，使得每次调用 `square` 时都会打印函数的调用信息。

## 装饰器的高级用法

装饰器还可以接受参数，并且可以叠加使用。使用 `@` 符号可以简化高阶函数的应用，使代码更简洁。

通过理解 lambda 表达式、抽象和高阶函数，我们可以编写出更加灵活、简洁和可维护的代码。这些概念不仅提升了代码的表达能力，还增强了代码的可复用性。l