# Scientific Calculation Guide

[TOC]

[English](ScientificCalculation.md) | [简体中文](ScientificCalculation_zh-CN.md) | [Deutsch](ScientificCalculation_de.md) | [Español](ScientificCalculation_es.md) | [Français](ScientificCalculation_fr.md)

## Overview

This module uses Python's SymPy library to perform scientific calculations. Incoming QQ messages are parsed into SymPy expressions, so in theory you can access most SymPy features through QQ. The bot returns results as text messages or rendered images.

This document lists commonly tested, core features. See the [SymPy documentation](https://docs.sympy.org/latest/index.html) for the full API.

## Command template

```python
sympy
# comments
a = cos(pi)

show([a])
play
```

## Output

### `show` text output

Send results back as text messages. The input parameter is a variable or expression.

- Single variable: `show(variable)`
- Multiple variables: `show([var1, var2, var3])`

### `play` LaTeX rendering

Enter `play` on the last line to render the results as an image through the LaTeX engine.

Some commands cannot be rendered by LaTeX and must use `show()` for text output.

## Common functions

### Symbolic representation

#### `Symbol` create symbols

##### Parameters

| Parameter    | Type   | Default | Description         |
| ------------ | ------ | ------- | ------------------- |
| `expression` | string | -       | Variable expression |

##### Notes

- Variable names should be a single letter.
- Greek letters (by English spelling) and mathematical constants are supported.

##### Example

```python
# variable = Symbol('expression')
a = Symbol('alpha ** 2')
x = Symbol('x')
```

### Identity transformations

#### `expand` expand expressions

##### Parameters

| Parameter    | Type              | Default | Description         |
| ------------ | ----------------- | ------- | ------------------- |
| `expression` | symbolic expression | -     | Expression to expand |

##### Notes

- The expression appears before the method.
- Use dot notation to call the method.

##### Example

```python
# expression.expand()
((x + y) ** 3).expand()
```

#### `factor` factor expressions

##### Parameters

| Parameter    | Type              | Default | Description        |
| ------------ | ----------------- | ------- | ------------------ |
| `expression` | symbolic expression | -     | Expression to factor |

##### Notes

None.

##### Example

```python
# factor(expression)
factor(x ** 2 + 2 * x * y + y ** 2)
```

#### `apart` partial fraction decomposition

##### Parameters

| Parameter    | Type              | Default | Description               |
| ------------ | ----------------- | ------- | ------------------------- |
| `expression` | symbolic expression | -     | Rational expression input |

##### Notes

None.

##### Example

```python
# apart(expression)
apart((x + 3) / (x - 1))
```

#### `together` combine fractions

##### Parameters

| Parameter    | Type              | Default | Description          |
| ------------ | ----------------- | ------- | -------------------- |
| `expression` | symbolic expression | -     | Expression to combine |

##### Notes

None.

##### Example

```python
# together(expression)
together(1 / x + 1 / y + 1 / z)
```

### Simplification

#### `simplify` general simplification

##### Parameters

| Parameter    | Type              | Default | Description             |
| ------------ | ----------------- | ------- | ----------------------- |
| `expression` | symbolic expression | -     | Expression to simplify |

##### Notes

None.

##### Example

```python
# simplify(expression)
simplify((x ** 3 + x ** 2 - x - 1) / (x ** 2 + 2 * x + 1))
```

#### `trigsimp` trigonometric simplification

##### Parameters

| Parameter    | Type              | Default | Description                       |
| ------------ | ----------------- | ------- | --------------------------------- |
| `expression` | symbolic expression | -     | Expression containing trigonometry |

##### Notes

None.

##### Example

```python
# trigsimp(expression)
trigsimp(sin(x) / cos(x))
```

#### `powsimp` exponential simplification

##### Parameters

| Parameter    | Type              | Default | Description            |
| ------------ | ----------------- | ------- | ---------------------- |
| `expression` | symbolic expression | -     | Expression with powers |

##### Notes

None.

##### Example

```python
# powsimp(expression)
powsimp(x ** a * x ** b)
```

### Solve equations

#### `solve` solve equations

##### Parameters

| Parameter    | Type   | Default | Description                                |
| ------------ | ------ | ------- | ------------------------------------------ |
| `expression` | list   | -       | Equations to solve (right-hand side is 0) |
| `unsolved`   | list   | -       | Unknowns to solve for                      |

##### Notes

- Parameters must be provided as lists.

##### Example

```python
# Solve a system of two linear equations
solve([2 * x - y - 3, 3 * x + y - 7], [x, y])
```

### Limits

#### `limit` compute limits

##### Parameters

| Parameter    | Type              | Default | Description           |
| ------------ | ----------------- | ------- | --------------------- |
| `expression` | symbolic expression | -     | Function              |
| `var`        | symbolic expression | -     | Variable              |
| `aim`        | number            | -       | Limit point            |
| `direction`  | string            | -       | Optional direction    |

##### Notes

- Use `oo` for infinity (two lowercase letters).
- `dir='+'` for right-hand limits, `dir='-'` for left-hand limits.
- Without `dir`, the two-sided limit is computed.

##### Example

```python
# limit(function, variable, target, optional direction)
limit(1 / x, x, 2)
a = limit(1 / x, x, oo, dir='-')
show([a])
```

### Calculus

#### `diff` differentiation

##### Parameters

| Parameter    | Type              | Default | Description              |
| ------------ | ----------------- | ------- | ------------------------ |
| `expression` | symbolic expression | -     | Function to differentiate |
| `var`        | symbolic expression | -     | Differentiation variable |
| `order`      | positive integer  | 1       | Optional derivative order |

##### Notes

None.

##### Example

```python
# diff(function, variable, optional order)
diff(x ** 3, x, 2)
```

#### `integrate` indefinite integral

##### Parameters

| Parameter    | Type              | Default | Description    |
| ------------ | ----------------- | ------- | -------------- |
| `expression` | symbolic expression | -     | Integrand      |
| `var`        | symbolic expression | -     | Integration variable |

##### Notes

None.

##### Example

```python
# integrate(integrand, variable)
integrate(sin(x), x)
```

#### `integrate` definite integral

##### Parameters

| Parameter    | Type              | Default | Description                          |
| ------------ | ----------------- | ------- | ------------------------------------ |
| `expression` | symbolic expression | -     | Integrand                            |
| `parameters` | tuple             | -       | (variable, lower bound, upper bound) |

##### Notes

None.

##### Example

```python
# integrate(integrand, (variable, lower bound, upper bound))
integrate(sin(x), (x, 0, pi / 2))
```

### Differential equations

#### `dsolve` solve differential equations

##### Parameters

| Parameter    | Type              | Default | Description                               |
| ------------ | ----------------- | ------- | ----------------------------------------- |
| `expression` | symbolic expression | -     | Equation to solve (right-hand side is 0) |
| `function`   | function          | -       | Function to solve for                     |

##### Notes

- Use `Function` first to define the function symbol.

##### Example

```python
# Example: y' = 2xy
f = Function('f')
a = dsolve(diff(f(x), x) - 2 * f(x) * x, f(x))
show([a])
```

### Matrix simplification

Matrix-related simplifications are planned for future updates.
