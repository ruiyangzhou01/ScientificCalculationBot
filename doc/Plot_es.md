# Guía de trazado

[TOC]

[English](Plot.md) | [简体中文](Plot_zh-CN.md) | [Deutsch](Plot_de.md) | [Español](Plot_es.md) | [Français](Plot_fr.md)

## Visión general

Este módulo utiliza la biblioteca matplotlib de Python para generar gráficos a partir de comandos enviados por QQ y devuelve la figura como imagen.

## Plantilla de comandos

```python
function('p1', 'p2')
```

- Cada parámetro debe ir entre comillas simples.

## Funciones

### `draw` función explícita de una variable

Traza y devuelve una función explícita de una variable.

##### Parámetros

| Parámetro | Tipo   | Valor predeterminado | Descripción                          |
| --------- | ------ | -------------------- | ------------------------------------ |
| `fun`     | string | -                    | Expresión de la función explícita    |
| `x_range` | string | -                    | Valor inicial, final y paso          |

##### Notas

- Separe los tres valores con comas.

##### Ejemplo

```python
# draw(fun, x_range)
draw('sin(x) / x', '-10, 10, 0.1')
```

### `draw_imp` función implícita

Traza y devuelve una función implícita de dos variables.

##### Parámetros

| Parámetro | Tipo   | Valor predeterminado | Descripción                          |
| --------- | ------ | -------------------- | ------------------------------------ |
| `equation`| string | -                    | Ecuación implícita en x e y          |
| `x_range` | string | -                    | Valor inicial y final para x         |
| `y_range` | string | -                    | Valor inicial y final para y         |

##### Notas

- Separe los dos valores con comas.

##### Ejemplo

```python
# draw_imp(equation, x_range, y_range)
draw_imp('17 * x**2 - 16*abs(x)*y + 17 * y**2 - 256', '-6, 6', '-6, 6')
```

### `draw_para` ecuación paramétrica

Traza y devuelve una ecuación paramétrica de un solo parámetro.

##### Parámetros

| Parámetro | Tipo   | Valor predeterminado | Descripción                               |
| --------- | ------ | -------------------- | ----------------------------------------- |
| `x_eq`    | string | -                    | Ecuación de x en función de t             |
| `y_eq`    | string | -                    | Ecuación de y en función de t             |
| `t_range` | string | -                    | Valor inicial, final y paso para t        |

##### Notas

- Separe los valores con comas.

##### Ejemplo

```python
# draw_para(x_eq, y_eq, t_range)
draw_para('2*sin(t)', '3*cos(t)', '0, 2*pi, 0.1')
```
