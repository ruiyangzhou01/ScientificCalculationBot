# Utilities Guide

[TOC]

[English](Utilities.md) | [简体中文](Utilities_zh-CN.md) | [Deutsch](Utilities_de.md) | [Español](Utilities_es.md) | [Français](Utilities_fr.md)

## Science encyclopedia

<p>
    <img alt="Wolfram" src="https://img.shields.io/badge/-Wolfram-3572A5?style=flat&logo=Wolfram&logoColor=white" />
    <img alt="Wolfram Language" src="https://img.shields.io/badge/-Wolfram_Language-3572A5?style=flat&logo=WolframLanguage&logoColor=white" />
</p>

#### Description

Use the Wolfram API to query the Wolfram knowledge engine.

#### `easy_res` simple result

##### Parameters

| Parameter | Type   | Default | Description |
| --------- | ------ | ------- | ----------- |
| `query`   | string | -       | Question    |

##### Response

Return the answer as a text message.

#### `short_answers` short answer

##### Parameters

| Parameter | Type   | Default | Description |
| --------- | ------ | ------- | ----------- |
| `query`   | string | -       | Question    |

##### Response

Return the answer as a text message.

#### `conversational` conversational answer

##### Parameters

| Parameter | Type   | Default | Description |
| --------- | ------ | ------- | ----------- |
| `query`   | string | -       | Question    |
| `user_id` | number | -       | User ID     |

##### Response

Return the answer as a text message.

## Voice messages

<p>
    <img alt="Alibaba Cloud" src="https://img.shields.io/badge/-Alibaba_Cloud-3572A5?style=flat&logo=AlibabaCloud&logoColor=white" />
</p>

#### Description

Use the Alibaba Cloud API to synthesize voice messages.

#### `group_send_record` send a voice message to a group

##### Parameters

| Parameter | Type   | Default | Description |
| --------- | ------ | ------- | ----------- |
| `text`    | string | -       | Text        |

##### Response

Return the answer as a text message.

## Experimental features (Beta)

### Face recognition

<p>
    <img alt="Tecent Cloud" src="https://img.shields.io/badge/-Tecent_Cloud-3572A5?style=flat&logo=tencentqq&logoColor=white" />
</p>

#### Description

Use the Tencent Cloud API for face recognition.

### Spelling correction

### Word statistics

##### Input

Provide the string to be analyzed.

##### Processing

1. Normalize the text by converting it to lowercase and removing irrelevant characters.
2. Split the normalized string into a word list.
3. Count occurrences of each word to form a dictionary of word counts.
4. Convert the dictionary into a structure keyed by count with word lists as values.
5. Sort by occurrence count and alphabetical order.

##### Response

Return the result as a text message.
