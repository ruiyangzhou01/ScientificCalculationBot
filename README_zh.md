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

基于 Python 科学计算与绘图库以及 CQ-HTTP 框架的智能 QQ 机器人。它通过 QQ 客户端提供端到端服务，集科学计算、绘图、排版、聊天互动、群聊管理与实用功能于一体。

:warning: **由于 CQ-HTTP 框架已于 2020 年秋停止维护，本项目不再维护。**

## 概览

用户从 QQ 发送消息，机器人捕获并处理内容，结果通过文字或由 $\LaTeX$ 引擎渲染的图片返回。实现过程中结合了 Python 库与云服务（Wolfram、阿里云、腾讯云）来提供科学能力。

## 主要功能

- 端到端的 QQ 机器人工作流，覆盖科学计算需求。
- 依托 NumPy 与 SymPy 的科学计算（符号运算、方程求解、微积分等）。
- 基于 matplotlib 的绘图能力，支持显函数、隐函数与参数方程。
- 通过 CoolQ HTTP API 实现聊天互动与群聊管理。
- Wolfram 科学百科、语音消息以及实验性功能等实用服务。

## 文档

- [科学计算指南](doc/ScientificCalculation_zh-CN.md)
- [绘图指南](doc/Plot_zh-CN.md)
- [互动与群聊管理 API](doc/Interaction_zh-CN.md)
- [实用功能指南](doc/Utilities_zh-CN.md)

## 运行前提

- Python 3 环境，并安装 NumPy、SymPy、matplotlib 等依赖。
- CoolQ 与 CQ-HTTP 插件（已停止维护）。
- 若启用云服务功能，需要配置 Wolfram、阿里云与腾讯云 API 密钥。

## 许可证

[GPL-3.0 License](LICENSE) © ruiyangzhou01
