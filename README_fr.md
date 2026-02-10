<p align="center">
 <img width="100px" src="README.assets/logo.png"  align="center" />
  <h1 align="center">Scientific Calculation Bot</h1>
</p>
<p align="center">
    <img src="https://img.shields.io/github/v/release/ruiyangzhou01/ScientificCalculationBot?&color=blue&logo=hack-the-box"/>
    <img alt="ChatBot" src="https://img.shields.io/badge/-ChatBot-3572A5?style=flat&logo=ChatBot&logoColor=white" />
    <img alt="Python" src="https://img.shields.io/badge/-Python-3572A5?style=flat&logo=python&logoColor=white" />
    <img alt="CQ-HTTP" src="https://img.shields.io/badge/-CQ--HTTP-3572A5?style=flat&logo=tencentqq&logoColor=white" />
</p>
<p align="center">
    <a href="https://github.com/ruiyangzhou01/ScientificCalculationBot/blob/main/README.md">English</a> •
    <a href="https://github.com/ruiyangzhou01/ScientificCalculationBot/blob/main/README_zh.md">简体中文</a> •
    <a href="https://github.com/ruiyangzhou01/ScientificCalculationBot/blob/main/README_de.md">Deutsch</a> •
    <a href="https://github.com/ruiyangzhou01/ScientificCalculationBot/blob/main/README_es.md">Español</a> •
    <a href="https://github.com/ruiyangzhou01/ScientificCalculationBot/blob/main/README_fr.md">Français</a>
</p>

Un bot QQ intelligent basé sur les bibliothèques Python de calcul scientifique et de visualisation, ainsi que sur le framework CQ-HTTP. Il fournit des services de bout en bout via le client QQ et intègre le calcul scientifique, le tracé, la mise en page, l'interaction de chat, la gestion de groupes et des fonctionnalités utilitaires.

:warning: **Ce projet n'est plus maintenu, car le framework CQ-HTTP a été arrêté à l'automne 2020.**

## Présentation

Les utilisateurs envoient des messages depuis QQ, le bot capture et traite le contenu, puis renvoie les résultats sous forme de texte ou d'images rendues par le moteur $\LaTeX$. L'implémentation combine des bibliothèques Python avec des services cloud (Wolfram, Alibaba Cloud, Tencent Cloud) afin de fournir des fonctionnalités scientifiques.

## Fonctionnalités principales

- Flux de travail de bot QQ de bout en bout pour les demandes scientifiques.
- Calcul scientifique avec NumPy et SymPy (symbolique, résolution d'équations, calcul, etc.).
- Tracé avec matplotlib pour les courbes explicites, implicites et paramétriques.
- Interaction de chat et gestion de groupes via l'API HTTP de CoolQ.
- Services utilitaires comme la recherche scientifique Wolfram, les messages vocaux et des fonctions expérimentales.

## Documentation

- [Guide du calcul scientifique](doc/ScientificCalculation.md)
- [Guide de tracé](doc/Plot.md)
- [API d'interaction et de gestion de groupes](doc/Interaction.md)
- [Guide des utilitaires](doc/Utilities.md)

## Prérequis

- Python 3 avec NumPy, SymPy, matplotlib et les dépendances associées.
- CoolQ avec le plugin CQ-HTTP (obsolète).
- Identifiants d'API pour Wolfram, Alibaba Cloud et Tencent Cloud si vous activez les fonctionnalités cloud.

## Licence

[GPL-3.0 License](LICENSE) © ruiyangzhou01
