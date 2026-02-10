# Guide des utilitaires

[TOC]

[English](Utilities.md) | [简体中文](Utilities_zh-CN.md) | [Deutsch](Utilities_de.md) | [Español](Utilities_es.md) | [Français](Utilities_fr.md)

## Encyclopédie scientifique

<p>
    <img alt="Wolfram" src="https://img.shields.io/badge/-Wolfram-3572A5?style=flat&logo=Wolfram&logoColor=white" />
    <img alt="Wolfram Language" src="https://img.shields.io/badge/-Wolfram_Language-3572A5?style=flat&logo=WolframLanguage&logoColor=white" />
</p>

#### Description

Utilise l'API Wolfram pour interroger le moteur de connaissances de Wolfram.

#### `easy_res` résultat simple

##### Paramètres

| Paramètre | Type   | Valeur par défaut | Description |
| --------- | ------ | ----------------- | ----------- |
| `query`   | string | -                 | Question    |

##### Réponse

Renvoie une image contenant la réponse (Wolfram `/v1/simple`), encapsulée dans un message `[CQ:image,...]`.

#### `short_answers` réponse courte

##### Paramètres

| Paramètre | Type   | Valeur par défaut | Description |
| --------- | ------ | ----------------- | ----------- |
| `query`   | string | -                 | Question    |

##### Réponse

Renvoie la réponse sous forme de message texte.

#### `conversational` réponse conversationnelle

##### Paramètres

| Paramètre | Type   | Valeur par défaut | Description |
| --------- | ------ | ----------------- | ----------- |
| `query`   | string | -                 | Question    |
| `user_id` | number | -                 | ID utilisateur |

##### Réponse

Renvoie la réponse sous forme de message texte.

## Messages vocaux

<p>
    <img alt="Alibaba Cloud" src="https://img.shields.io/badge/-Alibaba_Cloud-3572A5?style=flat&logo=AlibabaCloud&logoColor=white" />
</p>

#### Description

Utilise l'API Alibaba Cloud pour synthétiser des messages vocaux.

#### `group_send_record` envoyer un message vocal au groupe

##### Paramètres

| Paramètre | Type   | Valeur par défaut | Description |
| --------- | ------ | ----------------- | ----------- |
| `text`    | string | -                 | Texte       |

##### Réponse

Renvoie un message vocal CQ `[record]` au groupe.

## Fonctionnalités expérimentales (Beta)

### Reconnaissance faciale

<p>
    <img alt="Tencent Cloud" src="https://img.shields.io/badge/-Tencent_Cloud-3572A5?style=flat&logo=tencentqq&logoColor=white" />
</p>

#### Description

Utilise l'API Tencent Cloud pour la reconnaissance faciale.

### Correction orthographique

### Statistiques de mots

##### Entrée

Fournissez la chaîne à analyser.

##### Traitement

1. Normalisez le texte : passez-le en minuscules et supprimez les caractères non pertinents.
2. Divisez le texte en une liste de mots.
3. Comptez les occurrences de chaque mot pour créer un dictionnaire.
4. Transformez le dictionnaire en une structure avec la fréquence comme clé et une liste de mots comme valeur.
5. Triez par fréquence puis par ordre alphabétique.

##### Réponse

Renvoie le résultat sous forme de message texte.
