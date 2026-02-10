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

An intelligent QQ bot based on Python scientific calculation and plotting libraries plus the CQ-HTTP framework. It provides end-to-end services through the QQ client and integrates scientific calculation, plotting, layout, chat interaction, group management, and utility functions.

:warning: **This project is no longer maintained because the CQ-HTTP framework was discontinued in the fall of 2020.**

## Overview

Users send messages from QQ, the bot captures and processes the content, and the results are returned as text or as images rendered by the $\LaTeX$ engine. The implementation combines Python libraries with cloud services (Wolfram, Alibaba Cloud, Tencent Cloud) to deliver scientific features.

## Key capabilities

- End-to-end QQ bot workflow for scientific requests.
- Scientific calculation via NumPy and SymPy (symbolics, equation solving, calculus, and more).
- Plotting powered by matplotlib for explicit, implicit, and parametric curves.
- Chat interaction and group management via the CoolQ HTTP API.
- Utility services such as Wolfram-based knowledge search, voice messages, and experimental features.

## Documentation

- [Scientific calculation guide](doc/ScientificCalculation.md)
- [Plotting guide](doc/Plot.md)
- [Interaction & group management API](doc/Interaction.md)
- [Utilities guide](doc/Utilities.md)

## Prerequisites

- Python 3 environment with NumPy, SymPy, matplotlib, and related dependencies.
- CoolQ with the CQ-HTTP plugin (now deprecated).
- API credentials for Wolfram, Alibaba Cloud, and Tencent Cloud when enabling cloud-based features.

## License

[GPL-3.0 License](LICENSE) © ruiyangzhou01
