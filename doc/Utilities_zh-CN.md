# 实用功能指南

[TOC]

[English](Utilities.md) | [简体中文](Utilities_zh-CN.md) | [Deutsch](Utilities_de.md) | [Español](Utilities_es.md) | [Français](Utilities_fr.md)

## 科学百科

<p>
    <img alt="Wolfram" src="https://img.shields.io/badge/-Wolfram-3572A5?style=flat&logo=Wolfram&logoColor=white" />
    <img alt="Wolfram Language" src="https://img.shields.io/badge/-Wolfram_Language-3572A5?style=flat&logo=WolframLanguage&logoColor=white" />
</p>

#### 描述

调用 Wolfram API 查询科学百科。

#### `easy_res` 简单结果

##### 参数

| 参数    | 数据类型 | 默认值 | 说明 |
| ------- | -------- | ------ | ---- |
| `query` | 字符串   | -      | 问题 |

##### 响应

通过文字消息返回回答结果。

#### `short_answers` 简短回答

##### 参数

| 参数    | 数据类型 | 默认值 | 说明 |
| ------- | -------- | ------ | ---- |
| `query` | 字符串   | -      | 问题 |

##### 响应

通过文字消息返回回答结果。

#### `conversational` 会话式回答

##### 参数

| 参数     | 数据类型 | 默认值 | 说明   |
| -------- | -------- | ------ | ------ |
| `query`  | 字符串   | -      | 问题   |
| `user_id`| 数字     | -      | 用户 ID |

##### 响应

通过文字消息返回回答结果。

## 语音消息

<p>
    <img alt="Alibaba Cloud" src="https://img.shields.io/badge/-Alibaba_Cloud-3572A5?style=flat&logo=AlibabaCloud&logoColor=white" />
</p>

#### 描述

调用阿里云 API 合成语音消息。

#### `group_send_record` 群聊发送语音

##### 参数

| 参数   | 数据类型 | 默认值 | 说明 |
| ------ | -------- | ------ | ---- |
| `text` | 字符串   | -      | 文本 |

##### 响应

通过文字消息返回回答结果。

## 实验性功能（Beta）

### 人脸识别

<p>
    <img alt="Tecent Cloud" src="https://img.shields.io/badge/-Tecent_Cloud-3572A5?style=flat&logo=tencentqq&logoColor=white" />
</p>

#### 描述

调用腾讯云 API 实现人脸识别。

### 拼写纠正

### 单词统计

##### 输入

输入待统计的字符串。

##### 处理

1. 预处理文本：转为小写、移除无关字符。
2. 拆分文本，得到单词列表。
3. 统计每个单词出现次数，生成词频字典。
4. 将词频字典转换为“次数 -> 单词列表”的结构。
5. 按出现次数与字母顺序排序。

##### 响应

通过文字消息返回回答结果。
