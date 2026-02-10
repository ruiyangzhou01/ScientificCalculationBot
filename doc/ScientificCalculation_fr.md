# Guide de calcul scientifique

[TOC]

[English](ScientificCalculation.md) | [简体中文](ScientificCalculation_zh-CN.md) | [Deutsch](ScientificCalculation_de.md) | [Español](ScientificCalculation_es.md) | [Français](ScientificCalculation_fr.md)

## Présentation

Ce module utilise la bibliothèque SymPy de Python pour effectuer des calculs scientifiques. Les messages QQ sont convertis en expressions SymPy, ce qui permet en théorie d'utiliser la plupart des fonctionnalités de SymPy via QQ. Les résultats sont renvoyés en texte ou sous forme d'images rendues.

Ce document présente les fonctionnalités principales testées. Consultez la [documentation SymPy](https://docs.sympy.org/latest/index.html) pour l'API complète.

## Modèle de commande

```python
sympy
# commentaires
a = cos(pi)

show([a])
play
```

## Sortie

### `show` sortie texte

Renvoie les résultats sous forme de message texte. Le paramètre est une variable ou une expression.

- Variable unique : `show(variable)`
- Plusieurs variables : `show([var1, var2, var3])`

### `play` rendu LaTeX

Saisissez `play` sur la dernière ligne pour rendre le résultat via le moteur LaTeX et renvoyer une image.

Certaines commandes ne peuvent pas être rendues par LaTeX et doivent être renvoyées avec `show()`.

## Fonctions courantes

### Représentation symbolique

#### `Symbol` créer des symboles

##### Paramètres

| Paramètre    | Type   | Valeur par défaut | Description      |
| ------------ | ------ | ----------------- | ---------------- |
| `expression` | string | -                 | Nom du symbole   |

##### Notes

- Les noms de variables doivent être une seule lettre.
- Les lettres grecques (orthographe anglaise) et les constantes mathématiques sont prises en charge.

##### Exemple

```python
# variable = Symbol('expression')
alpha = Symbol('alpha')
alpha_squared = alpha ** 2
x = Symbol('x')
```

### Transformations d'identité

#### `expand` développer les expressions

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                 |
| ------------ | ------------------- | ----------------- | --------------------------- |
| `expression` | expression symbolique | -               | Expression à développer     |

##### Notes

- L'expression précède la méthode.
- Utilisez la notation par point.

##### Exemple

```python
# expression.expand()
((x + y) ** 3).expand()
```

#### `factor` factoriser

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                 |
| ------------ | ------------------- | ----------------- | --------------------------- |
| `expression` | expression symbolique | -               | Expression à factoriser     |

##### Notes

Aucune.

##### Exemple

```python
# factor(expression)
factor(x ** 2 + 2 * x * y + y ** 2)
```

#### `apart` décomposition en fractions partielles

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                 |
| ------------ | ------------------- | ----------------- | --------------------------- |
| `expression` | expression symbolique | -               | Expression rationnelle      |

##### Notes

Aucune.

##### Exemple

```python
# apart(expression)
apart((x + 3) / (x - 1))
```

#### `together` combiner les fractions

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                 |
| ------------ | ------------------- | ----------------- | --------------------------- |
| `expression` | expression symbolique | -               | Expression à combiner       |

##### Notes

Aucune.

##### Exemple

```python
# together(expression)
together(1 / x + 1 / y + 1 / z)
```

### Simplification

#### `simplify` simplification générale

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                 |
| ------------ | ------------------- | ----------------- | --------------------------- |
| `expression` | expression symbolique | -               | Expression à simplifier     |

##### Notes

Aucune.

##### Exemple

```python
# simplify(expression)
simplify((x ** 3 + x ** 2 - x - 1) / (x ** 2 + 2 * x + 1))
```

#### `trigsimp` simplification trigonométrique

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                          |
| ------------ | ------------------- | ----------------- | ------------------------------------ |
| `expression` | expression symbolique | -               | Expression contenant des termes trigonométriques |

##### Notes

Aucune.

##### Exemple

```python
# trigsimp(expression)
trigsimp(sin(x) / cos(x))
```

#### `powsimp` simplification des puissances

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                 |
| ------------ | ------------------- | ----------------- | --------------------------- |
| `expression` | expression symbolique | -               | Expression avec puissances  |

##### Notes

Aucune.

##### Exemple

```python
# powsimp(expression)
powsimp(x ** a * x ** b)
```

### Résoudre des équations

#### `solve` résoudre des équations

##### Paramètres

| Paramètre    | Type | Valeur par défaut | Description                                   |
| ------------ | ---- | ----------------- | --------------------------------------------- |
| `expression` | list | -                 | Équations à résoudre (côté droit = 0)         |
| `unsolved`   | list | -                 | Inconnues à résoudre                          |

##### Notes

- Les paramètres doivent être fournis sous forme de listes.

##### Exemple

```python
# Résoudre un système de deux équations linéaires
solve([2 * x - y - 3, 3 * x + y - 7], [x, y])
```

### Limites

#### `limit` calculer des limites

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description           |
| ------------ | ------------------- | ----------------- | --------------------- |
| `expression` | expression symbolique | -               | Fonction              |
| `var`        | expression symbolique | -               | Variable              |
| `aim`        | number             | -                 | Point limite           |
| `direction`  | string             | -                 | Direction optionnelle |

##### Notes

- Utilisez `oo` pour l'infini (deux lettres minuscules).
- `dir='+'` pour la limite à droite, `dir='-'` pour la limite à gauche.
- Sans `dir`, la limite bilatérale est calculée.

##### Exemple

```python
# limit(function, variable, target, optional direction)
limit(1 / x, x, 2)
a = limit(1 / x, x, oo, dir='-')
show([a])
```

### Calcul différentiel et intégral

#### `diff` dérivation

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                       |
| ------------ | ------------------- | ----------------- | --------------------------------- |
| `expression` | expression symbolique | -               | Fonction à dériver                |
| `var`        | expression symbolique | -               | Variable de dérivation            |
| `order`      | entier positif     | 1                 | Ordre de dérivée optionnel        |

##### Notes

Aucune.

##### Exemple

```python
# diff(function, variable, optional order)
diff(x ** 3, x, 2)
```

#### `integrate` intégrale indéfinie

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                |
| ------------ | ------------------- | ----------------- | -------------------------- |
| `expression` | expression symbolique | -               | Intégrande                 |
| `var`        | expression symbolique | -               | Variable d'intégration     |

##### Notes

Aucune.

##### Exemple

```python
# integrate(integrand, variable)
integrate(sin(x), x)
```

#### `integrate` intégrale définie

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                                   |
| ------------ | ------------------- | ----------------- | --------------------------------------------- |
| `expression` | expression symbolique | -               | Intégrande                                    |
| `parameters` | tuple              | -                 | (variable, borne inférieure, borne supérieure) |

##### Notes

Aucune.

##### Exemple

```python
# integrate(integrand, (variable, lower bound, upper bound))
integrate(sin(x), (x, 0, pi / 2))
```

### Équations différentielles

#### `dsolve` résoudre des équations différentielles

##### Paramètres

| Paramètre    | Type                | Valeur par défaut | Description                                  |
| ------------ | ------------------- | ----------------- | -------------------------------------------- |
| `expression` | expression symbolique | -               | Équation à résoudre (côté droit = 0)         |
| `function`   | function           | -                 | Fonction à résoudre                           |

##### Notes

- Utilisez `Function` pour définir le symbole de la fonction.

##### Exemple

```python
# Exemple : y' = 2xy
f = Function('f')
a = dsolve(diff(f(x), x) - 2 * f(x) * x, f(x))
show([a])
```

### Simplification de matrices

Les simplifications de matrices sont prévues pour de futures mises à jour.
