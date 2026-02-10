# Plotting-Leitfaden

[TOC]

[English](Plot.md) | [简体中文](Plot_zh-CN.md) | [Deutsch](Plot_de.md) | [Español](Plot_es.md) | [Français](Plot_fr.md)

## Überblick

Dieses Modul verwendet die Python-Bibliothek matplotlib, um aus QQ-Nachrichten Plots zu erzeugen und die Ergebnisse als Bildnachricht zurückzugeben.

## Befehlsvorlage

```python
function('p1', 'p2')
```

- Jeder Parameter muss in einfache Anführungszeichen gesetzt werden.

## Funktionen

### `draw` explizite Funktion mit einer Variable

Zeichnet eine eindimensionale explizite Funktion.

##### Parameter

| Parameter | Typ    | Standard | Beschreibung                     |
| --------- | ------ | -------- | -------------------------------- |
| `fun`     | string | -        | Ausdruck der expliziten Funktion |
| `x_range` | string | -        | Startwert, Endwert und Schrittweite |

##### Hinweise

- Trenne die drei Werte mit Kommas.

##### Beispiel

```python
# draw(fun, x_range)
draw('sin(x) / x', '-10, 10, 0.1')
```

### `draw_imp` implizite Funktion

Zeichnet eine zweidimensionale implizite Funktion.

##### Parameter

| Parameter | Typ    | Standard | Beschreibung                                     |
| --------- | ------ | -------- | ------------------------------------------------ |
| `fun`     | string | -        | Implizite Gleichung in x und y                   |
| `x_range` | string | -        | Startwert, Endwert und Schrittweite für x        |
| `y_range` | string | -        | Startwert, Endwert und Schrittweite für y        |

##### Hinweise

- Trenne die Werte mit Kommas.

##### Beispiel

```python
# draw_imp(fun, x_range, y_range)
draw_imp('17 * x**2 - 16*abs(x)*y + 17 * y**2 - 256', '-6, 6', '-6, 6')
```

### `draw_para` parametrische Gleichung

Zeichnet eine parametrische Gleichung mit einem Parameter.

##### Parameter

| Parameter | Typ    | Standard | Beschreibung                           |
| --------- | ------ | -------- | -------------------------------------- |
| `x_eq`    | string | -        | Gleichung für x in Abhängigkeit von t |
| `y_eq`    | string | -        | Gleichung für y in Abhängigkeit von t |
| `t_range` | string | -        | Startwert, Endwert und Schrittweite für t |

##### Hinweise

- Trenne die Werte mit Kommas.

##### Beispiel

```python
# draw_para(x_eq, y_eq, t_range)
draw_para('2*sin(t)', '3*cos(t)', '0, 2*pi, 0.1')
```
