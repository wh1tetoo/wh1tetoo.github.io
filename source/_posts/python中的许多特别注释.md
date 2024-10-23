---
title: python中的许多特别注释
date: 2024-09-20 22:00:52
tags: python
categories: 程序猿
---

起初是在深度学习的书中看到了一个特别注释 #@save， 书上说这个注释可以将我自己定义的类，函数等东西放到我的库里面，然后以后调用库中的这个函数就可以了。不过有点疑惑，一个是他为什么直接就保存到 d2l 这个库中了，他还 import 了许多其他的库，例如 matplotlib， numpy。为什么没有保存到这个库里面。还有一个问题是 import 库到底有几种方法？顺着这个，我得查一查GPT。
<!-- more -->

## 导入库的方式
在 Python 中，导入模块（库）的方式有多种，每种方式适用于不同的场景。以下是常见的导入方式及其示例：

### 直接导入模块
这是最常见的导入方式，适用于导入整个模块。
```python
import numpy
```
使用时需要通过模块名访问其功能：

### 导入模块并指定别名
使用 as 关键字为模块指定一个简短的别名，方便调用。
```python
import numpy as np
```

### 从模块中导入特定的函数或类
只导入某个模块的部分功能，避免导入整个模块。
```python
from numpy import array
array([1, 2, 3])
```

### 从模块中导入多个函数或类
导入多个特定的功能，使用逗号分隔。
```python
from numpy import array, mean
```

### 从模块中导入所有内容
使用 * 导入模块中的所有公共对象。一般不推荐这种方式，因为容易造成命名冲突。
```python
from numpy import *
```

### 嵌套导入（按需导入）
在函数或代码块中导入库，仅在需要时导入，可以减少程序启动时的内存消耗。
```python
def my_function():
    import numpy as np
    return np.array([1, 2, 3])
```

## 特殊注释
在 Python 中，除了普通的注释（使用 #），还有一些特殊的注释和装饰器（decorators），用于为代码增加特定的行为或标识。以下是一些常见的特殊注释和装饰器的解释：

### 1. 普通注释
使用 # 表示单行注释，注释的内容不会执行。
```python
# 这是一个普通的注释
x = 10  # 变量 x 赋值为 10
```

### 2. #@save 注释
这种注释通常出现在特定的代码框架或工具中，用于标记某些代码块。它本身并不是 Python 语言的内置特性。比如在深度学习书籍或教程的代码中，#@save 常用来表示要保存某些重要代码片段。
```python
#@save
def my_model():
    pass
```
用途：这种注释通常与工具集成，用于代码块的管理、保存或特殊处理。它不会直接影响 Python 的运行。

### 3. 装饰器（@decorator）
装饰器是 Python 提供的一种函数或类的高级功能，允许在函数或方法的定义前后增加行为。装饰器使用 @ 符号来引用，紧跟在函数或方法定义之前。

常见装饰器有：
#### a. @property
将一个方法变成一个属性，使得你可以像访问属性一样调用它，而**不需要显式加上括号 ()**。
```python
class Person:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name

person = Person('Alice')
print(person.name)  # 像访问属性一样，调用 name 而不是 name()
```

#### b. @staticmethod
用于定义一个静态方法。静态方法不需要访问实例或类属性。
```python
class MyClass:
    @staticmethod
    def my_static_method():
        print("This is a static method.")
```

#### c. @classmethod
定义类方法。类方法的第一个参数是类本身，而不是实例对象。
```python
class MyClass:
    @classmethod
    def my_class_method(cls):
        print("This is a class method.")
```

#### d. 自定义装饰器
你可以定义自己的装饰器，用于修改或增强函数的行为。
```python
def my_decorator(func):
    def wrapper():
        print("Before the function.")
        func()
        print("After the function.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
# 输出:
# Before the function.
# Hello!
# After the function.
```
### 4. # type: ignore 注释
这是一种类型注释，通常与 mypy 等静态类型检查器结合使用，用于忽略特定行代码的类型检查。
```python
x = "Hello"  # type: ignore
x = 123  # 类型不匹配，但忽略类型检查
```

### 5. # TODO 注释
虽然 # TODO 并不是 Python 特有的注释类型，但它是开发者常用的一种注释，标记未完成的任务或代码中的改进项。
```python
# TODO: 实现此函数
def my_function():
    pass
```

### 6. # noqa 注释
# noqa 是用于忽略某些代码检查工具（如 flake8）的注释，用于忽略某一行的检查错误。
```python

def my_function():  # noqa: E501
    print("This is a very long line that might break some style guides.")
```
### 7. 类型注解 (# type:)
可以为变量或函数加上类型注释，用来帮助工具做静态类型检查。
```python
x: int = 10  # 表示 x 是一个整数
```

这些特殊的注释和装饰器让 Python 代码在可读性、功能扩展和类型检查方面变得更加强大。




---
 - [x] 明白了注释怎么用，和库的调用 
 - [ ] 再看word2vec之前，需要看 softmax 和 求梯度

