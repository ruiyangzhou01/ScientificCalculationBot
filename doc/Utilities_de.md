# Dienstprogramme

[TOC]

[English](Utilities.md) | [简体中文](Utilities_zh-CN.md) | [Deutsch](Utilities_de.md) | [Español](Utilities_es.md) | [Français](Utilities_fr.md)

## Wissenschaftslexikon

<p>
    <img alt="Wolfram" src="https://img.shields.io/badge/-Wolfram-3572A5?style=flat&logo=Wolfram&logoColor=white" />
    <img alt="Wolfram Language" src="https://img.shields.io/badge/-Wolfram_Language-3572A5?style=flat&logo=WolframLanguage&logoColor=white" />
</p>

#### Beschreibung

Verwendet die Wolfram API, um das Wolfram-Wissenssystem abzufragen.

#### `easy_res` einfaches Ergebnis

##### Parameter

| Parameter | Typ    | Standard | Beschreibung |
| --------- | ------ | -------- | ------------ |
| `query`   | string | -        | Frage        |

##### Antwort

Gibt die Antwort als Textnachricht zurück.

#### `short_answers` kurze Antwort

##### Parameter

| Parameter | Typ    | Standard | Beschreibung |
| --------- | ------ | -------- | ------------ |
| `query`   | string | -        | Frage        |

##### Antwort

Gibt die Antwort als Textnachricht zurück.

#### `conversational` konversationelle Antwort

##### Parameter

| Parameter | Typ    | Standard | Beschreibung |
| --------- | ------ | -------- | ------------ |
| `query`   | string | -        | Frage        |
| `user_id` | number | -        | Benutzer-ID  |

##### Antwort

Gibt die Antwort als Textnachricht zurück.

## Sprachnachrichten

<p>
    <img alt="Alibaba Cloud" src="https://img.shields.io/badge/-Alibaba_Cloud-3572A5?style=flat&logo=AlibabaCloud&logoColor=white" />
</p>

#### Beschreibung

Verwendet die Alibaba-Cloud-API zur Sprachsynthese.

#### `group_send_record` Sprachnachricht in eine Gruppe senden

##### Parameter

| Parameter | Typ    | Standard | Beschreibung |
| --------- | ------ | -------- | ------------ |
| `text`    | string | -        | Text         |

##### Antwort

Gibt die Antwort als Textnachricht zurück.

## Experimentelle Funktionen (Beta)

### Gesichtserkennung

<p>
    <img alt="Tecent Cloud" src="https://img.shields.io/badge/-Tecent_Cloud-3572A5?style=flat&logo=tencentqq&logoColor=white" />
</p>

#### Beschreibung

Verwendet die Tencent-Cloud-API für die Gesichtserkennung.

### Rechtschreibkorrektur

### Wortstatistik

##### Eingabe

Gib den zu analysierenden Text an.

##### Verarbeitung

1. Normalisiere den Text: in Kleinbuchstaben umwandeln und irrelevante Zeichen entfernen.
2. Teile den Text in eine Wortliste auf.
3. Zähle die Vorkommen jedes Wortes und erstelle ein Wörterbuch.
4. Erstelle ein neues Wörterbuch mit der Häufigkeit als Schlüssel und Wortlisten als Werte.
5. Sortiere nach Häufigkeit und alphabetischer Reihenfolge.

##### Antwort

Gibt das Ergebnis als Textnachricht zurück.
