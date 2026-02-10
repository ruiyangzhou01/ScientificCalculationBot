# Guía de utilidades

[TOC]

[English](Utilities.md) | [简体中文](Utilities_zh-CN.md) | [Deutsch](Utilities_de.md) | [Español](Utilities_es.md) | [Français](Utilities_fr.md)

## Enciclopedia científica

<p>
    <img alt="Wolfram" src="https://img.shields.io/badge/-Wolfram-3572A5?style=flat&logo=Wolfram&logoColor=white" />
    <img alt="Wolfram Language" src="https://img.shields.io/badge/-Wolfram_Language-3572A5?style=flat&logo=WolframLanguage&logoColor=white" />
</p>

#### Descripción

Utiliza la API de Wolfram para consultar el motor de conocimiento de Wolfram.

#### `easy_res` resultado simple

##### Parámetros

| Parámetro | Tipo   | Valor predeterminado | Descripción |
| --------- | ------ | -------------------- | ----------- |
| `query`   | string | -                    | Pregunta    |

##### Respuesta

Devuelve la respuesta como una imagen generada por Wolfram (endpoint `/v1/simple`), enviada en un mensaje `[CQ:image,...]`.

#### `short_answers` respuesta breve

##### Parámetros

| Parámetro | Tipo   | Valor predeterminado | Descripción |
| --------- | ------ | -------------------- | ----------- |
| `query`   | string | -                    | Pregunta    |

##### Respuesta

Devuelve la respuesta en un mensaje de texto.

#### `conversational` respuesta conversacional

##### Parámetros

| Parámetro | Tipo   | Valor predeterminado | Descripción |
| --------- | ------ | -------------------- | ----------- |
| `query`   | string | -                    | Pregunta    |
| `user_id` | number | -                    | ID de usuario |

##### Respuesta

Devuelve la respuesta en un mensaje de texto.

## Mensajes de voz

<p>
    <img alt="Alibaba Cloud" src="https://img.shields.io/badge/-Alibaba_Cloud-3572A5?style=flat&logo=AlibabaCloud&logoColor=white" />
</p>

#### Descripción

Utiliza la API de Alibaba Cloud para sintetizar mensajes de voz.

#### `group_send_record` enviar un mensaje de voz al grupo

##### Parámetros

| Parámetro | Tipo   | Valor predeterminado | Descripción |
| --------- | ------ | -------------------- | ----------- |
| `text`    | string | -                    | Texto       |

##### Respuesta

Envía al grupo un mensaje de voz en formato CQ `[record]`.

## Funciones experimentales (Beta)

### Reconocimiento facial

<p>
    <img alt="Tencent Cloud" src="https://img.shields.io/badge/-Tencent_Cloud-3572A5?style=flat&logo=tencentqq&logoColor=white" />
</p>

#### Descripción

Utiliza la API de Tencent Cloud para reconocimiento facial.

### Corrección ortográfica

### Estadísticas de palabras

##### Entrada

Proporciona la cadena que deseas analizar.

##### Procesamiento

1. Normaliza el texto: convierte a minúsculas y elimina caracteres irrelevantes.
2. Divide el texto en una lista de palabras.
3. Cuenta las apariciones de cada palabra para crear un diccionario.
4. Convierte el diccionario en una estructura con la frecuencia como clave y la lista de palabras como valor.
5. Ordena por frecuencia y orden alfabético.

##### Respuesta

Devuelve el resultado en un mensaje de texto.
