# Plotting Guide

[TOC]

[English](Plot.md) | [简体中文](Plot_zh-CN.md) | [Deutsch](Plot_de.md) | [Español](Plot_es.md) | [Français](Plot_fr.md)

## Overview

This module uses Python's matplotlib library to generate plots from commands sent via QQ. The bot returns the rendered figure as an image message.

## Command template

```python
function('p1', 'p2')
```

- Wrap each parameter in single quotes.

## Functions

### `draw` explicit single-variable function

Plot and output a one-dimensional explicit function.

##### Parameters

| Parameter   | Type   | Default | Description                            |
| ----------- | ------ | ------- | -------------------------------------- |
| `fun`       | string | -       | Explicit function expression           |
| `x_range`   | string | -       | Start value, end value, and step size  |

##### Notes

- Separate the three range values with commas.

##### Example

```python
# draw(fun, x_range)
draw('sin(x) / x', '-10, 10, 0.1')
```

### `draw_imp` implicit function

Plot and output a two-variable implicit function.

##### Parameters

| Parameter   | Type   | Default | Description                    |
| ----------- | ------ | ------- | ------------------------------ |
| `equation`  | string | -       | Implicit equation in x and y   |
| `x_range`   | string | -       | Start value and end value for x |
| `y_range`   | string | -       | Start value and end value for y |

##### Notes

- Provide two values (start and end) separated by commas.

##### Example

```python
# draw_imp(equation, x_range, y_range)
draw_imp('17 * x**2 - 16*abs(x)*y + 17 * y**2 - 256', '-6, 6', '-6, 6')
```

### `draw_para` parametric equation

Plot and output a single-parameter parametric equation.

##### Parameters

| Parameter  | Type   | Default | Description                              |
| ---------- | ------ | ------- | ---------------------------------------- |
| `x_eq`     | string | -       | Equation for the x variable in terms of t |
| `y_eq`     | string | -       | Equation for the y variable in terms of t |
| `t_range`  | string | -       | Start value, end value, and step size for t |

##### Notes

- Separate the range values with commas.

##### Example

```python
# draw_para(x_eq, y_eq, t_range)
draw_para('2*sin(t)', '3*cos(t)', '0, 2*pi, 0.1')
```
