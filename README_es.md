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

Un bot inteligente de QQ basado en bibliotecas de cálculo y gráficos científicos de Python y en el marco CQ-HTTP. Ofrece servicios de extremo a extremo mediante el cliente de QQ e integra cálculo científico, trazado, maquetación, interacción de chat, administración de grupos y funciones utilitarias.

:warning: **Este proyecto ya no se mantiene porque el marco CQ-HTTP se descontinuó en otoño de 2020.**

## Visión general

Los usuarios envían mensajes desde QQ, el bot captura y procesa el contenido, y los resultados se devuelven como texto o como imágenes renderizadas por el motor $\LaTeX$. La implementación combina bibliotecas de Python con servicios en la nube (Wolfram, Alibaba Cloud, Tencent Cloud) para ofrecer capacidades científicas.

## Funcionalidades principales

- Flujo de trabajo completo de bot QQ para solicitudes científicas.
- Cálculo científico con NumPy y SymPy (simbólico, resolución de ecuaciones, cálculo, etc.).
- Trazado con matplotlib para curvas explícitas, implícitas y paramétricas.
- Interacción de chat y administración de grupos mediante la API HTTP de CoolQ.
- Utilidades como búsqueda científica en Wolfram, mensajes de voz y funciones experimentales.

## Documentación

- [Guía de cálculo científico](doc/ScientificCalculation.md)
- [Guía de trazado](doc/Plot.md)
- [API de interacción y gestión de grupos](doc/Interaction.md)
- [Guía de utilidades](doc/Utilities.md)

## Requisitos previos

- Python 3 con NumPy, SymPy, matplotlib y dependencias relacionadas.
- CoolQ con el complemento CQ-HTTP (obsoleto).
- Credenciales de API para Wolfram, Alibaba Cloud y Tencent Cloud cuando se habiliten funciones en la nube.

## Licencia

[GPL-3.0 License](LICENSE) © ruiyangzhou01
