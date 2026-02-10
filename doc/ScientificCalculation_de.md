# Leitfaden für wissenschaftliche Berechnungen

[TOC]

[English](ScientificCalculation.md) | [简体中文](ScientificCalculation_zh-CN.md) | [Deutsch](ScientificCalculation_de.md) | [Español](ScientificCalculation_es.md) | [Français](ScientificCalculation_fr.md)

## Überblick

Dieses Modul nutzt die Python-Bibliothek SymPy für wissenschaftliche Berechnungen. Eingehende QQ-Nachrichten werden als SymPy-Ausdrücke interpretiert, sodass sich theoretisch die meisten SymPy-Funktionen über QQ aufrufen lassen. Ergebnisse werden als Text oder gerenderte Bilder zurückgegeben.

Dieses Dokument listet häufig getestete Kernfunktionen. Eine vollständige Übersicht bietet die [SymPy-Dokumentation](https://docs.sympy.org/latest/index.html).

## Befehlsvorlage

```python
sympy
# Kommentare
a = cos(pi)

show([a])
play
```

## Ausgabe

### `show` Textausgabe

Gibt Ergebnisse als Textnachricht zurück. Der Parameter ist eine Variable oder ein Ausdruck.

- Einzelne Variable: `show(variable)`
- Mehrere Variablen: `show([var1, var2, var3])`

### `play` LaTeX-Rendering

Gib in der letzten Zeile `play` ein, um die Ergebnisse über die LaTeX-Engine als Bild auszugeben.

Einige Befehle lassen sich nicht per LaTeX rendern und müssen mit `show()` als Text ausgegeben werden.

## Häufige Funktionen

### Symbolische Darstellung

#### `Symbol` Symbole erstellen

##### Parameter

| Parameter    | Typ    | Standard | Beschreibung |
| ------------ | ------ | -------- | ------------ |
| `expression` | string | -        | Symbolname   |

##### Hinweise

- Variablennamen sollten aus einem einzelnen Buchstaben bestehen.
- Griechische Buchstaben (englische Schreibweise) und mathematische Konstanten werden unterstützt.

##### Beispiel

```python
# variable = Symbol('expression')
alpha = Symbol('alpha')
alpha_squared = alpha ** 2
x = Symbol('x')
```

### Identitätstransformationen

#### `expand` Ausdrücke erweitern

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung          |
| ------------ | ------------------ | -------- | --------------------- |
| `expression` | symbolischer Ausdruck | -     | Zu erweiternder Ausdruck |

##### Hinweise

- Der Ausdruck steht vor der Methode.
- Verwende Punktnotation.

##### Beispiel

```python
# expression.expand()
((x + y) ** 3).expand()
```

#### `factor` faktorisieren

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung            |
| ------------ | ------------------ | -------- | ----------------------- |
| `expression` | symbolischer Ausdruck | -     | Zu faktorisierender Ausdruck |

##### Hinweise

Keine.

##### Beispiel

```python
# factor(expression)
factor(x ** 2 + 2 * x * y + y ** 2)
```

#### `apart` Partialbruchzerlegung

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung                 |
| ------------ | ------------------ | -------- | ---------------------------- |
| `expression` | symbolischer Ausdruck | -     | Rationaler Ausdruck           |

##### Hinweise

Keine.

##### Beispiel

```python
# apart(expression)
apart((x + 3) / (x - 1))
```

#### `together` Brüche zusammenfassen

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung             |
| ------------ | ------------------ | -------- | ------------------------ |
| `expression` | symbolischer Ausdruck | -     | Zu kombinierender Ausdruck |

##### Hinweise

Keine.

##### Beispiel

```python
# together(expression)
together(1 / x + 1 / y + 1 / z)
```

### Vereinfachung

#### `simplify` allgemeine Vereinfachung

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung              |
| ------------ | ------------------ | -------- | ------------------------- |
| `expression` | symbolischer Ausdruck | -     | Zu vereinfachender Ausdruck |

##### Hinweise

Keine.

##### Beispiel

```python
# simplify(expression)
simplify((x ** 3 + x ** 2 - x - 1) / (x ** 2 + 2 * x + 1))
```

#### `trigsimp` trigonometrische Vereinfachung

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung                     |
| ------------ | ------------------ | -------- | -------------------------------- |
| `expression` | symbolischer Ausdruck | -     | Ausdruck mit trigonometrischen Termen |

##### Hinweise

Keine.

##### Beispiel

```python
# trigsimp(expression)
trigsimp(sin(x) / cos(x))
```

#### `powsimp` Potenzvereinfachung

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung               |
| ------------ | ------------------ | -------- | -------------------------- |
| `expression` | symbolischer Ausdruck | -     | Ausdruck mit Potenzen      |

##### Hinweise

Keine.

##### Beispiel

```python
# powsimp(expression)
powsimp(x ** a * x ** b)
```

### Gleichungen lösen

#### `solve` Gleichungen lösen

##### Parameter

| Parameter    | Typ   | Standard | Beschreibung                                  |
| ------------ | ----- | -------- | -------------------------------------------- |
| `expression` | list  | -        | Zu lösende Gleichungen (rechte Seite = 0)    |
| `unsolved`   | list  | -        | Unbekannte Variablen                          |

##### Hinweise

- Parameter müssen als Listen angegeben werden.

##### Beispiel

```python
# Lösen eines linearen Gleichungssystems
solve([2 * x - y - 3, 3 * x + y - 7], [x, y])
```

### Grenzwerte

#### `limit` Grenzwerte berechnen

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung              |
| ------------ | ------------------ | -------- | ------------------------- |
| `expression` | symbolischer Ausdruck | -     | Funktion                  |
| `var`        | symbolischer Ausdruck | -     | Variable                  |
| `aim`        | number            | -       | Grenzwertpunkt            |
| `direction`  | string            | -       | Optionale Richtung        |

##### Hinweise

- Verwende `oo` für unendlich (zwei Kleinbuchstaben).
- `dir='+'` für den rechten Grenzwert, `dir='-'` für den linken Grenzwert.
- Ohne `dir` wird der zweiseitige Grenzwert berechnet.

##### Beispiel

```python
# limit(function, variable, target, optional direction)
limit(1 / x, x, 2)
a = limit(1 / x, x, oo, dir='-')
show([a])
```

### Analysis

#### `diff` Ableitung

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung                     |
| ------------ | ------------------ | -------- | -------------------------------- |
| `expression` | symbolischer Ausdruck | -     | Zu differenzierende Funktion     |
| `var`        | symbolischer Ausdruck | -     | Differentiationsvariable         |
| `order`      | positive integer  | 1       | Optionale Ableitungsordnung      |

##### Hinweise

Keine.

##### Beispiel

```python
# diff(function, variable, optional order)
diff(x ** 3, x, 2)
```

#### `integrate` unbestimmtes Integral

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung |
| ------------ | ------------------ | -------- | ------------ |
| `expression` | symbolischer Ausdruck | -     | Integrand    |
| `var`        | symbolischer Ausdruck | -     | Integrationsvariable |

##### Hinweise

Keine.

##### Beispiel

```python
# integrate(integrand, variable)
integrate(sin(x), x)
```

#### `integrate` bestimmtes Integral

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung                              |
| ------------ | ------------------ | -------- | ----------------------------------------- |
| `expression` | symbolischer Ausdruck | -     | Integrand                                |
| `parameters` | tuple             | -        | (Variable, Untergrenze, Obergrenze)      |

##### Hinweise

Keine.

##### Beispiel

```python
# integrate(integrand, (variable, lower bound, upper bound))
integrate(sin(x), (x, 0, pi / 2))
```

### Differentialgleichungen

#### `dsolve` Differentialgleichungen lösen

##### Parameter

| Parameter    | Typ                | Standard | Beschreibung                                 |
| ------------ | ------------------ | -------- | -------------------------------------------- |
| `expression` | symbolischer Ausdruck | -     | Zu lösende Gleichung (rechte Seite = 0)      |
| `function`   | function          | -        | Zu lösende Funktion                          |

##### Hinweise

- Definiere die Funktionssymbole zuerst mit `Function`.

##### Beispiel

```python
# Beispiel: y' = 2xy
f = Function('f')
a = dsolve(diff(f(x), x) - 2 * f(x) * x, f(x))
show([a])
```

### Matrixvereinfachung

Matrixbezogene Vereinfachungen sind für zukünftige Updates geplant.
