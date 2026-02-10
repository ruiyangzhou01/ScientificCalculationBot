# 科学计算指南

[TOC]

[English](ScientificCalculation.md) | [简体中文](ScientificCalculation_zh-CN.md) | [Deutsch](ScientificCalculation_de.md) | [Español](ScientificCalculation_es.md) | [Français](ScientificCalculation_fr.md)

## 概览

本模块基于 Python 的 SymPy 库进行科学计算。机器人会解析 QQ 消息为 SymPy 表达式，因此理论上可以通过 QQ 调用大部分 SymPy 功能，并以文字消息或图片形式返回结果。

本文档列出经过测试的核心功能。完整功能请参考 [SymPy 文档](https://docs.sympy.org/latest/index.html)。

## 指令模板

```python
sympy
# 注释
a = cos(pi)

show([a])
play
```

## 输出

### `show` 文字输出

以文字消息输出结果，输入参数为变量或表达式。

- 单变量：`show(variable)`
- 多变量：`show([var1, var2, var3])`

### `play` LaTeX 渲染输出

最后一行输入 `play`，机器人会通过 LaTeX 引擎渲染结果并输出图片。

部分命令无法通过 LaTeX 渲染时，请使用 `show()` 以文本方式输出。

## 常用功能

### 符号表示

#### `Symbol` 创建符号

##### 参数

| 参数         | 数据类型 | 默认值 | 说明     |
| ------------ | -------- | ------ | -------- |
| `expression` | 字符串   | -      | 符号名称 |

##### 注意

- 变量名建议为单个字母。
- 支持希腊字母（英文拼写）与数学常数。

##### 示例

```python
# variable = Symbol('expression')
alpha = Symbol('alpha')
alpha_squared = alpha ** 2
x = Symbol('x')
```

### 恒等变换

#### `expand` 展开表达式

##### 参数

| 参数         | 数据类型     | 默认值 | 说明         |
| ------------ | ------------ | ------ | ------------ |
| `expression` | 符号表达式   | -      | 待展开表达式 |

##### 注意

- 表达式写在最前面。
- 通过点号调用方法。

##### 示例

```python
# expression.expand()
((x + y) ** 3).expand()
```

#### `factor` 因式分解

##### 参数

| 参数         | 数据类型     | 默认值 | 说明         |
| ------------ | ------------ | ------ | ------------ |
| `expression` | 符号表达式   | -      | 待分解表达式 |

##### 注意

无。

##### 示例

```python
# factor(expression)
factor(x ** 2 + 2 * x * y + y ** 2)
```

#### `apart` 分式拆分

##### 参数

| 参数         | 数据类型     | 默认值 | 说明         |
| ------------ | ------------ | ------ | ------------ |
| `expression` | 符号表达式   | -      | 待拆分表达式 |

##### 注意

无。

##### 示例

```python
# apart(expression)
apart((x + 3) / (x - 1))
```

#### `together` 合并分式

##### 参数

| 参数         | 数据类型     | 默认值 | 说明         |
| ------------ | ------------ | ------ | ------------ |
| `expression` | 符号表达式   | -      | 待合并表达式 |

##### 注意

无。

##### 示例

```python
# together(expression)
together(1 / x + 1 / y + 1 / z)
```

### 化简

#### `simplify` 常规化简

##### 参数

| 参数         | 数据类型     | 默认值 | 说明         |
| ------------ | ------------ | ------ | ------------ |
| `expression` | 符号表达式   | -      | 待化简表达式 |

##### 注意

无。

##### 示例

```python
# simplify(expression)
simplify((x ** 3 + x ** 2 - x - 1) / (x ** 2 + 2 * x + 1))
```

#### `trigsimp` 三角化简

##### 参数

| 参数         | 数据类型     | 默认值 | 说明         |
| ------------ | ------------ | ------ | ------------ |
| `expression` | 符号表达式   | -      | 含三角函数的表达式 |

##### 注意

无。

##### 示例

```python
# trigsimp(expression)
trigsimp(sin(x) / cos(x))
```

#### `powsimp` 幂化简

##### 参数

| 参数         | 数据类型     | 默认值 | 说明         |
| ------------ | ------------ | ------ | ------------ |
| `expression` | 符号表达式   | -      | 含幂的表达式 |

##### 注意

无。

##### 示例

```python
# powsimp(expression)
powsimp(x ** a * x ** b)
```

### 解方程

#### `solve` 解方程

##### 参数

| 参数         | 数据类型 | 默认值 | 说明                                   |
| ------------ | -------- | ------ | -------------------------------------- |
| `expression` | 列表     | -      | 待求解方程列表（右端等于 0）           |
| `unsolved`   | 列表     | -      | 待求解的未知量列表                     |

##### 注意

- 参数需要使用列表形式。

##### 示例

```python
# 二元一次方程
solve([2 * x - y - 3, 3 * x + y - 7], [x, y])
```

### 极限

#### `limit` 求极限

##### 参数

| 参数         | 数据类型     | 默认值 | 说明           |
| ------------ | ------------ | ------ | -------------- |
| `expression` | 符号表达式   | -      | 函数           |
| `var`        | 符号表达式   | -      | 变量           |
| `aim`        | 数值         | -      | 趋近点         |
| `direction`  | 字符串       | -      | 可选：趋近方向 |

##### 注意

- 无穷用两个小写的 `oo` 表示。
- `dir='+'` 求右极限，`dir='-'` 求左极限。
- 不写 `dir` 表示求双侧极限。

##### 示例

```python
# limit(function, variable, target, optional direction)
limit(1 / x, x, 2)
a = limit(1 / x, x, oo, dir='-')
show([a])
```

### 微积分

#### `diff` 求导

##### 参数

| 参数         | 数据类型     | 默认值 | 说明               |
| ------------ | ------------ | ------ | ------------------ |
| `expression` | 符号表达式   | -      | 待求导函数         |
| `var`        | 符号表达式   | -      | 求导变量           |
| `order`      | 正整数       | 1      | 可选：求导阶数     |

##### 注意

无。

##### 示例

```python
# diff(function, variable, optional order)
diff(x ** 3, x, 2)
```

#### `integrate` 不定积分

##### 参数

| 参数         | 数据类型     | 默认值 | 说明     |
| ------------ | ------------ | ------ | -------- |
| `expression` | 符号表达式   | -      | 被积函数 |
| `var`        | 符号表达式   | -      | 积分变量 |

##### 注意

无。

##### 示例

```python
# integrate(integrand, variable)
integrate(sin(x), x)
```

#### `integrate` 定积分

##### 参数

| 参数         | 数据类型     | 默认值 | 说明                                 |
| ------------ | ------------ | ------ | ------------------------------------ |
| `expression` | 符号表达式   | -      | 被积函数                             |
| `parameters` | 元组         | -      | (积分变量, 下限, 上限)               |

##### 注意

无。

##### 示例

```python
# integrate(integrand, (variable, lower bound, upper bound))
integrate(sin(x), (x, 0, pi / 2))
```

### 微分方程

#### `dsolve` 求解微分方程

##### 参数

| 参数         | 数据类型     | 默认值 | 说明                               |
| ------------ | ------------ | ------ | ---------------------------------- |
| `expression` | 符号表达式   | -      | 待求解方程（右端等于 0）           |
| `function`   | 函数         | -      | 要求解的函数                       |

##### 注意

- 先使用 `Function` 定义函数符号。

##### 示例

```python
# 以 y' = 2xy 为例
f = Function('f')
a = dsolve(diff(f(x), x) - 2 * f(x) * x, f(x))
show([a])
```

### 矩阵化简

矩阵相关化简功能计划在后续版本补充。
