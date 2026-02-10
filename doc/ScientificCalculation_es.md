# Guía de cálculo científico

[TOC]

[English](ScientificCalculation.md) | [简体中文](ScientificCalculation_zh-CN.md) | [Deutsch](ScientificCalculation_de.md) | [Español](ScientificCalculation_es.md) | [Français](ScientificCalculation_fr.md)

## Visión general

Este módulo utiliza la biblioteca SymPy de Python para realizar cálculos científicos. Los mensajes de QQ se transforman en expresiones de SymPy, por lo que en teoría es posible usar la mayoría de las funciones de SymPy a través de QQ. Los resultados se devuelven como texto o como imágenes renderizadas.

Este documento enumera funciones principales probadas. Consulta la [documentación de SymPy](https://docs.sympy.org/latest/index.html) para el API completo.

## Plantilla de comandos

```python
sympy
# comentarios
a = cos(pi)

show([a])
play
```

## Salida

### `show` salida de texto

Devuelve resultados en un mensaje de texto. El parámetro de entrada es una variable o expresión.

- Variable única: `show(variable)`
- Varias variables: `show([var1, var2, var3])`

### `play` renderizado LaTeX

Introduce `play` en la última línea para renderizar el resultado con el motor LaTeX y devolver una imagen.

Algunos comandos no se pueden renderizar con LaTeX y deben devolverse con `show()`.

## Funciones comunes

### Representación simbólica

#### `Symbol` crear símbolos

##### Parámetros

| Parámetro    | Tipo   | Valor predeterminado | Descripción       |
| ------------ | ------ | -------------------- | ----------------- |
| `expression` | string | -                    | Nombre del símbolo |

##### Notas

- Los nombres de variables deben ser una sola letra.
- Se admiten letras griegas (en inglés) y constantes matemáticas.

##### Ejemplo

```python
# variable = Symbol('expression')
alpha = Symbol('alpha')
alpha_squared = alpha ** 2
x = Symbol('x')
```

### Transformaciones de identidad

#### `expand` expandir expresiones

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                |
| ------------ | ------------------- | -------------------- | -------------------------- |
| `expression` | expresión simbólica | -                    | Expresión a expandir       |

##### Notas

- La expresión va antes del método.
- Usa la notación con punto.

##### Ejemplo

```python
# expression.expand()
((x + y) ** 3).expand()
```

#### `factor` factorizar expresiones

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                  |
| ------------ | ------------------- | -------------------- | ---------------------------- |
| `expression` | expresión simbólica | -                    | Expresión a factorizar       |

##### Notas

Ninguna.

##### Ejemplo

```python
# factor(expression)
factor(x ** 2 + 2 * x * y + y ** 2)
```

#### `apart` fracciones parciales

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                       |
| ------------ | ------------------- | -------------------- | --------------------------------- |
| `expression` | expresión simbólica | -                    | Expresión racional                |

##### Notas

Ninguna.

##### Ejemplo

```python
# apart(expression)
apart((x + 3) / (x - 1))
```

#### `together` combinar fracciones

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                 |
| ------------ | ------------------- | -------------------- | --------------------------- |
| `expression` | expresión simbólica | -                    | Expresión a combinar        |

##### Notas

Ninguna.

##### Ejemplo

```python
# together(expression)
together(1 / x + 1 / y + 1 / z)
```

### Simplificación

#### `simplify` simplificación general

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                 |
| ------------ | ------------------- | -------------------- | --------------------------- |
| `expression` | expresión simbólica | -                    | Expresión a simplificar     |

##### Notas

Ninguna.

##### Ejemplo

```python
# simplify(expression)
simplify((x ** 3 + x ** 2 - x - 1) / (x ** 2 + 2 * x + 1))
```

#### `trigsimp` simplificación trigonométrica

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                          |
| ------------ | ------------------- | -------------------- | ------------------------------------ |
| `expression` | expresión simbólica | -                    | Expresión con términos trigonométricos |

##### Notas

Ninguna.

##### Ejemplo

```python
# trigsimp(expression)
trigsimp(sin(x) / cos(x))
```

#### `powsimp` simplificación de potencias

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción               |
| ------------ | ------------------- | -------------------- | ------------------------- |
| `expression` | expresión simbólica | -                    | Expresión con potencias   |

##### Notas

Ninguna.

##### Ejemplo

```python
# powsimp(expression)
powsimp(x ** a * x ** b)
```

### Resolver ecuaciones

#### `solve` resolver ecuaciones

##### Parámetros

| Parámetro    | Tipo  | Valor predeterminado | Descripción                                   |
| ------------ | ----- | -------------------- | --------------------------------------------- |
| `expression` | list  | -                    | Ecuaciones a resolver (lado derecho = 0)      |
| `unsolved`   | list  | -                    | Incógnitas a resolver                          |

##### Notas

- Los parámetros deben proporcionarse como listas.

##### Ejemplo

```python
# Resolver un sistema de dos ecuaciones lineales
solve([2 * x - y - 3, 3 * x + y - 7], [x, y])
```

### Límites

#### `limit` calcular límites

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción            |
| ------------ | ------------------- | -------------------- | ---------------------- |
| `expression` | expresión simbólica | -                    | Función                |
| `var`        | expresión simbólica | -                    | Variable               |
| `aim`        | number             | -                    | Punto de límite         |
| `direction`  | string             | -                    | Dirección opcional     |

##### Notas

- Usa `oo` para infinito (dos letras minúsculas).
- `dir='+'` para límite por la derecha, `dir='-'` para el límite por la izquierda.
- Sin `dir` se calcula el límite bilateral.

##### Ejemplo

```python
# limit(function, variable, target, optional direction)
limit(1 / x, x, 2)
a = limit(1 / x, x, oo, dir='-')
show([a])
```

### Cálculo

#### `diff` derivación

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                     |
| ------------ | ------------------- | -------------------- | ------------------------------- |
| `expression` | expresión simbólica | -                    | Función a derivar               |
| `var`        | expresión simbólica | -                    | Variable de derivación          |
| `order`      | entero positivo     | 1                    | Orden de derivada opcional      |

##### Notas

Ninguna.

##### Ejemplo

```python
# diff(function, variable, optional order)
diff(x ** 3, x, 2)
```

#### `integrate` integral indefinida

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción           |
| ------------ | ------------------- | -------------------- | --------------------- |
| `expression` | expresión simbólica | -                    | Integrando            |
| `var`        | expresión simbólica | -                    | Variable de integración |

##### Notas

Ninguna.

##### Ejemplo

```python
# integrate(integrand, variable)
integrate(sin(x), x)
```

#### `integrate` integral definida

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                                |
| ------------ | ------------------- | -------------------- | ------------------------------------------ |
| `expression` | expresión simbólica | -                    | Integrando                                 |
| `parameters` | tuple              | -                    | (variable, límite inferior, límite superior) |

##### Notas

Ninguna.

##### Ejemplo

```python
# integrate(integrand, (variable, lower bound, upper bound))
integrate(sin(x), (x, 0, pi / 2))
```

### Ecuaciones diferenciales

#### `dsolve` resolver ecuaciones diferenciales

##### Parámetros

| Parámetro    | Tipo                | Valor predeterminado | Descripción                                 |
| ------------ | ------------------- | -------------------- | ------------------------------------------- |
| `expression` | expresión simbólica | -                    | Ecuación a resolver (lado derecho = 0)      |
| `function`   | function           | -                    | Función a resolver                          |

##### Notas

- Usa `Function` para definir el símbolo de función.

##### Ejemplo

```python
# Ejemplo: y' = 2xy
f = Function('f')
a = dsolve(diff(f(x), x) - 2 * f(x) * x, f(x))
show([a])
```

### Simplificación de matrices

Las simplificaciones de matrices están planificadas para versiones futuras.
