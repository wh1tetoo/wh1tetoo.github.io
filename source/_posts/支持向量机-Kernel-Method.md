---
title: 支持向量机 & Kernel Method
date: 2024-10-10 11:31:04
tags: machinelearning
categories: 程序猿
---
> 非线性带来高维转换（从模型角度）
> $$ x \rightarrow \phi(x)  $$
> 
> 对偶带来内积 （从优化角度） 
> $${x_i}^T {x_j}$$

<!-- more -->

> cover theroem: 高维比低维 更易线性可分

### Kernel Function
#### 定义
$$ \kappa(x,x') = \phi(x)^T \phi(x') = <\phi(x),\phi(x')> $$

对任意的 $x, x' \in X$, 存在 $\phi: x \rightarrow z$, 满足：
$$ \kappa(x,x') = \phi(x)^T \phi(x') $$
则 $ \kappa(x,x') $ 是一个核函数。

#### 核函数种类


### 想法

### 定义
- 训练数据 $x_i$ 及标签 $y_i$   (+1,-1)
- 线性模型：向量 ω， 常数b 使得 $ω^T x + b = 0$. 其他：直线，平面，超平面（hyperspace）
- 一个训练集linear separable. definition

### SVM （support vector machine)
- 优化问题：  
    - 最小化minimize $1/2 ||ω||^2$
    - 限制subject to $y_i(ω^T x + b) ≥ 1$

- 二次规划问题：（要么无解，要么只有一个极值）  
    - 目标函数 objective function 二次项  
    - 限制条件一次项

### SVM处理非线性
#### 第一种方式
- 最小化： $1/2 ||ω||^2 + C \sum \xi_i$  ，不让$\xi_i$太大
- 限制条件： 
    - $y_i(ω^T x + b) ≥ 1 - \xi_i$
    - $\xi_i ≥ 0$
- 松弛变量  $\xi_i$
- 正则项 $C \sum \xi_i$
- 事先设定的参数 $C$
#### 第二种方式
- 例子：异或问题
- 定义高维映射 $\phi(x)$
- 核函数
  - 高斯核
  - 多项式核
- 泛函分析(Mercer's throrem)：$K(x_1,x_2)$能被写成 $\phi(x_1)^T \phi(x_2)$的充要条件：
  - (交换性) $K(x_1, x_2) = K(x_2, x_1)$
  - (半正定性) 任意$c_i, x_i$ 有$\sum \sum c_i c_j K(x_i, x_j) >= 0$

### 优化理论
- 教材
  - \<convex optimization\>. Stephen boyol
  - \<Nonlinear Programming>
- Prime Problem 原问题
  - 最小化 $f(\omega)$
  - 限制条件 $g_i(\omega) <= 0$,  $h_i(\omega)= 0$
- Dual Problem 对偶问题
  - 利用拉格朗日乘数法
- 定理：如果$\omega ^*$是原问题的解，而$\alpha ^*, \beta^*$是对偶问题的解，则有$f(\omega^*)>=\Theta(\alpha^*, \beta^*)$
- 定义：原问题与对偶问题的间距（Duality Gap）$G = f - \Theta$, 某些问题$G=0$
- 强对偶定理
- KKT条件 



