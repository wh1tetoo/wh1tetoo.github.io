---
title: python中的各种数据类型辨析
date: 2024-09-19 20:44:36
tags: python
categories: 程序猿
---

## 以 python 为基础的数据类型
Python 本身提供了一些基本的数据类型，这些类型用于存储简单的数据：  
- 整数（int）：用于存储整数值，如 10 或 -3。  
- 浮点数（float）：用于存储带小数点的数值，如 3.14 或 -1.0。  
- 布尔值（bool）：用于表示真值（True）或假值（False）。  
- 字符串（str）：用于存储文本数据，如 "Hello"。  

而为了存储多个数据，便又衍生除了四种数据类型：  
- 列表（list）：存储多个元素，可以包含不同类型的元素，如 [1, "apple", 3.14]。  
- 元组（tuple）：类似列表，但一旦创建不可修改，如 (1, "apple", 3.14)。  
- 字典（dict）：键值对的集合，如 {"name": "John", "age": 30}。  
- 集合（set）：不包含重复元素的无序集合，如 {1, 2, 3}。  

<!-- more -->

## 从 python 到 Numpy
为了优化数值计算，Numpy 自己又引入了一套数据类型(称为dtype: int, float, bool_, complex, str_, unicode_), 这些数据类型通常是定长的，支持更高效的内存使用和性能优化。  
NumPy 的数据类型通常用于在多维数组（ndarray）中存储数值数据。它们比 Python 的数据类型更高效，特别是当处理大量数值时。

对于数学统计的研究者来说这个应该经常用到，它可以进行线性代数的矩阵乘法，求逆，特征值，矩阵分解等操作。也可以进行概率论的生成随机数的分布的操作。对于高维数组，可以进行切片，索引，排序，聚合等操作。

```python
import numpy as np
# 整数数组
int_arr = np.array([1, 2, 3], dtype='int32')
# 浮点数数组
float_arr = np.array([1.5, 2.5, 3.5], dtype='float64')
# 布尔值数组
bool_arr = np.array([True, False, True])
# 复数数组
complex_arr = np.array([1+2j, 3+4j, 5+6j])
# 求均值
mean = np.mean(arr)
# 求标准差
std = np.std(arr)
# 矩阵乘法
b = np.dot(a, a)
# 求逆矩阵
inv_a = np.linalg.inv(a)
# 生成 10 个 0 到 100 之间的随机整数
random_integers = np.random.randint(0, 100, 10)
# 生成正态分布的随机数
random_normal = np.random.randn(5)
```

## 从 Numpy 到 Pandas
Pandas 是基于 NumPy 构建的库，专门用于处理结构化数据，如表格数据。Pandas 在内部使用了 NumPy 的 dtype，但也引入了一些自己的数据类型来增强功能：  
- 整数类型（int64）和浮点类型（float64）：与 NumPy 相同，但 Pandas 允许它们包含 NaN（缺失值）。
- 布尔类型（bool）：与 NumPy 相同，但允许包含缺失值。
- 对象类型（object）：用于存储任意 Python 对象（如字符串或混合类型）。
- 分类类型（category）：用于存储有限个不同的值（类似枚举），节省内存且提升性能。
- 时间类型（datetime64、timedelta[ns]）：用于处理时间和时间差。

Pandas 用 Series 和 DataFrame 结构存储多种不同的数据类型。
### 1. Series (序列)
我的理解就是带有标签的一列数，只不过这个标签（索引 index ）就像是excel里默认的最左边的那一列，然后这列数的话可以是任意类型，例如年龄，姓名等等。实际上它可以包含任意类型的数据（整数、浮点数、字符串、布尔值等）。但是每个 Series 对象倾向于包含相同数据类型的元素
```python
import pandas as pd
s = pd.Series([1, 2, 3, 4, 5])
print(s)
0    1
1    2
2    3
3    4
4    5
```
Series 可转化为 Numpy 中的数组：
```python
s = pd.Series([1, 2, 3, 4, 5])
numpy_array = s.values  # 转换为 NumPy 数组
```

### 2. DataFrame (数据表)
可以看作是一个带标签的二维数组（矩阵），类似于 Excel 表格或者 SQL 数据表。每列都是一个 Series 对象。例如：  
```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'San Francisco', 'Los Angeles']
}
df = pd.DataFrame(data)
print(df)
```
```markdown
      Name  Age           City
0    Alice   25       New York
1      Bob   30  San Francisco
2  Charlie   35    Los Angeles
```

### 3. Object
它的作用就是当某一列包含不同的数据类型时，就将这列标记为 object 类型。这是一种通用的数据类型，它允许在同一列中包含不同类型的值（如字符串、整数、浮点数混合在一起）。这是因为 object 是 Python 中可以存储任意对象的类型。

```python
s = pd.Series([1, "hello", 3.14, True])
```

## 对于从 Web 获得的 JSON 数据
通常需要使用 Python 的 requests 库来发送 HTTP 请求获取数据，再通过 json 模块或 Pandas 来解析并处理数据。  
```python
import requests
import json
import pandas as pd

url = "https://api.example.com/data"
response = requests.get(url)
# 检查请求是否成功
if response.status_code == 200:
    # 解析 JSON 数据
    json_data = response.json()
    print(json_data)  # 打印返回的 JSON 数据
else:
    print(f"请求失败，状态码：{response.status_code}")

# 假设从 API 获得的 JSON 数据
json_data = '''
{
    "users": [
        {"name": "Alice", "age": 25, "city": "New York"},
        {"name": "Bob", "age": 30, "city": "San Francisco"}
    ]
}
'''
# 将 JSON 字符串解析为 Python 对象
parsed_data = json.loads(json_data)
# 访问数据
for user in parsed_data['users']:
    print(f"Name: {user['name']}, Age: {user['age']}, City: {user['city']}")
# 假设 JSON 数据是从 API 获取的，并且返回的 JSON 格式是数组形式
json_data = [
    {"name": "Alice", "age": 25, "city": "New York"},
    {"name": "Bob", "age": 30, "city": "San Francisco"},
]
# 将 JSON 转换为 DataFrame
df = pd.DataFrame(json_data)

# 使用 json_normalize 展开嵌套数据
df = json_normalize(nested_json)
```