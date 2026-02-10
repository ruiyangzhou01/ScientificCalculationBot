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

Ein intelligenter QQ-Bot auf Basis von Python-Bibliotheken für wissenschaftliche Berechnungen und Visualisierung sowie dem CQ-HTTP-Framework. Er bietet End-to-End-Services über den QQ-Client und vereint wissenschaftliche Berechnungen, Plotting, Layout, Chat-Interaktion, Gruppenverwaltung und nützliche Funktionen.

:warning: **Dieses Projekt wird nicht mehr gepflegt, da das CQ-HTTP-Framework im Herbst 2020 eingestellt wurde.**

## Überblick

Nutzer senden Nachrichten über QQ, der Bot verarbeitet den Inhalt und liefert Ergebnisse als Text oder als durch $\LaTeX$ gerenderte Bilder zurück. Die Implementierung kombiniert Python-Bibliotheken mit Cloud-Diensten (Wolfram, Alibaba Cloud, Tencent Cloud), um wissenschaftliche Funktionen bereitzustellen.

## Hauptfunktionen

- End-to-End-QQ-Bot-Workflow für wissenschaftliche Anfragen.
- Wissenschaftliche Berechnungen mit NumPy und SymPy (Symbolik, Gleichungslösung, Analysis u. a.).
- Plotting mit matplotlib für explizite, implizite und parametrische Kurven.
- Chat-Interaktion und Gruppenverwaltung über die CoolQ HTTP API.
- Dienstprogramme wie Wolfram-Wissenssuche, Sprachnachrichten und experimentelle Funktionen.

## Dokumentation

- [Leitfaden für wissenschaftliche Berechnungen](doc/ScientificCalculation_de.md)
- [Plotting-Leitfaden](doc/Plot_de.md)
- [Interaktion & Gruppenverwaltung API](doc/Interaction_de.md)
- [Dienstprogramme](doc/Utilities_de.md)

## Voraussetzungen

- Python 3 mit NumPy, SymPy, matplotlib und weiteren Abhängigkeiten.
- CoolQ mit CQ-HTTP-Plugin (veraltet).
- API-Zugangsdaten für Wolfram, Alibaba Cloud und Tencent Cloud, falls Cloud-Funktionen aktiviert werden.

## Lizenz

[GPL-3.0 License](LICENSE) © ruiyangzhou01
