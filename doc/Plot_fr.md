# Guide de tracé

[TOC]

[English](Plot.md) | [简体中文](Plot_zh-CN.md) | [Deutsch](Plot_de.md) | [Español](Plot_es.md) | [Français](Plot_fr.md)

## Présentation

Ce module utilise la bibliothèque matplotlib de Python pour générer des tracés à partir des commandes envoyées via QQ, puis renvoie l'image du graphique.

## Modèle de commande

```python
function('p1', 'p2')
```

- Chaque paramètre doit être entouré de guillemets simples.

## Fonctions

### `draw` fonction explicite à une variable

Trace et renvoie une fonction explicite à une variable.

##### Paramètres

| Paramètre | Type   | Valeur par défaut | Description                            |
| --------- | ------ | ----------------- | -------------------------------------- |
| `fun`     | string | -                 | Expression de la fonction explicite    |
| `x_range` | string | -                 | Valeur de début, valeur de fin et pas  |

##### Notes

- Séparez les trois valeurs par des virgules.

##### Exemple

```python
# draw(fun, x_range)
draw('sin(x) / x', '-10, 10, 0.1')
```

### `draw_imp` fonction implicite

Trace et renvoie une fonction implicite à deux variables.

##### Paramètres

| Paramètre | Type   | Valeur par défaut | Description                                     |
| --------- | ------ | ----------------- | ----------------------------------------------- |
| `fun`     | string | -                 | Équation implicite en x et y                    |
| `x_range` | string | -                 | Valeur de début, de fin et pas pour x           |
| `y_range` | string | -                 | Valeur de début, de fin et pas pour y           |

##### Notes

- Séparez les valeurs par des virgules.

##### Exemple

```python
# draw_imp(fun, x_range, y_range)
draw_imp('17 * x**2 - 16*abs(x)*y + 17 * y**2 - 256', '-6, 6', '-6, 6')
```

### `draw_para` équation paramétrique

Trace et renvoie une équation paramétrique à un seul paramètre.

##### Paramètres

| Paramètre | Type   | Valeur par défaut | Description                               |
| --------- | ------ | ----------------- | ----------------------------------------- |
| `x_eq`    | string | -                 | Équation de x en fonction de t            |
| `y_eq`    | string | -                 | Équation de y en fonction de t            |
| `t_range` | string | -                 | Valeur de début, de fin et pas pour t     |

##### Notes

- Séparez les valeurs par des virgules.

##### Exemple

```python
# draw_para(x_eq, y_eq, t_range)
draw_para('2*sin(t)', '3*cos(t)', '0, 2*pi, 0.1')
```
