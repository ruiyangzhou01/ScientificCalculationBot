# Interacción de chat y gestión de grupos

[TOC]

[English](Interaction.md) | [简体中文](Interaction_zh-CN.md) | [Deutsch](Interaction_de.md) | [Español](Interaction_es.md) | [Français](Interaction_fr.md)

## Visión general

Este documento resume las APIs de interacción y gestión de grupos que utiliza el bot. Los endpoints provienen del complemento CoolQ HTTP API. Para la referencia completa, consulta la documentación oficial del complemento.

## API

### Interacción básica

#### `send_private_msg` enviar mensaje privado

##### Parámetros

| Campo         | Tipo    | Valor predeterminado | Descripción                                                                 |
| ------------- | ------- | -------------------- | --------------------------------------------------------------------------- |
| `user_id`     | number  | -                    | Número QQ de destino                                                       |
| `message`     | message | -                    | Contenido del mensaje                                                      |
| `auto_escape` | boolean | `false`              | Enviar como texto plano (no analizar códigos CQ); solo válido si `message` es una cadena |

##### Respuesta

| Campo        | Tipo          | Descripción  |
| ----------- | ------------- | ------------ |
| `message_id`| number (int32) | ID del mensaje |

#### `send_group_msg` enviar mensaje de grupo

##### Parámetros

| Campo         | Tipo    | Valor predeterminado | Descripción                                                                 |
| ------------- | ------- | -------------------- | --------------------------------------------------------------------------- |
| `group_id`    | number  | -                    | ID del grupo                                                               |
| `message`     | message | -                    | Contenido del mensaje                                                      |
| `auto_escape` | boolean | `false`              | Enviar como texto plano (no analizar códigos CQ); solo válido si `message` es una cadena |

##### Respuesta

| Campo        | Tipo          | Descripción  |
| ----------- | ------------- | ------------ |
| `message_id`| number (int32) | ID del mensaje |

#### `send_discuss_msg` enviar mensaje a discusión

##### Parámetros

| Campo         | Tipo    | Valor predeterminado | Descripción                                                                 |
| ------------- | ------- | -------------------- | --------------------------------------------------------------------------- |
| `discuss_id`  | number  | -                    | ID de discusión (generalmente no visible; se obtiene de eventos)           |
| `message`     | message | -                    | Contenido del mensaje                                                      |
| `auto_escape` | boolean | `false`              | Enviar como texto plano (no analizar códigos CQ); solo válido si `message` es una cadena |

##### Respuesta

| Campo        | Tipo          | Descripción  |
| ----------- | ------------- | ------------ |
| `message_id`| number (int32) | ID del mensaje |

#### `send_msg` enviar mensaje

##### Parámetros

| Campo          | Tipo    | Valor predeterminado | Descripción                                                                 |
| -------------- | ------- | -------------------- | --------------------------------------------------------------------------- |
| `message_type` | string  | -                    | Tipo de mensaje: `private`, `group`, `discuss`. Si se omite, se infiere de `*_id` |
| `user_id`      | number  | -                    | Número QQ de destino (requerido si `message_type` es `private`)            |
| `group_id`     | number  | -                    | ID del grupo (requerido si `message_type` es `group`)                      |
| `discuss_id`   | number  | -                    | ID de discusión (requerido si `message_type` es `discuss`)                 |
| `message`      | message | -                    | Contenido del mensaje                                                      |
| `auto_escape`  | boolean | `false`              | Enviar como texto plano (no analizar códigos CQ); solo válido si `message` es una cadena |

##### Respuesta

| Campo        | Tipo          | Descripción  |
| ----------- | ------------- | ------------ |
| `message_id`| number (int32) | ID del mensaje |

#### `delete_msg` retirar mensaje

##### Parámetros

| Campo        | Tipo          | Valor predeterminado | Descripción |
| ----------- | ------------- | -------------------- | ----------- |
| `message_id`| number (int32) | -                    | ID del mensaje |

##### Respuesta

Ninguna.

#### `send_like` enviar like

##### Parámetros

| Campo     | Tipo   | Valor predeterminado | Descripción                                |
| --------- | ------ | -------------------- | ------------------------------------------ |
| `user_id` | number | -                    | Número QQ de destino                       |
| `times`   | number | 1                    | Número de likes (máximo 10 por amigo/día) |

##### Respuesta

Ninguna.

### Gestión de grupos

#### `set_group_kick` expulsar miembro

##### Parámetros

| Campo                 | Tipo    | Valor predeterminado | Descripción                     |
| --------------------- | ------- | -------------------- | ------------------------------- |
| `group_id`            | number  | -                    | ID del grupo                    |
| `user_id`             | number  | -                    | Número QQ a expulsar            |
| `reject_add_request`  | boolean | `false`              | Rechazar futuras solicitudes    |

##### Respuesta

Ninguna.

#### `set_group_ban` silenciar miembro

##### Parámetros

| Campo      | Tipo    | Valor predeterminado | Descripción                               |
| ---------- | ------- | -------------------- | ----------------------------------------- |
| `group_id` | number  | -                    | ID del grupo                              |
| `user_id`  | number  | -                    | Número QQ a silenciar                     |
| `duration` | number  | `30 * 60`            | Duración en segundos; 0 cancela el silencio |

##### Respuesta

Ninguna.

#### `set_group_anonymous_ban` silenciar usuario anónimo

##### Parámetros

| Campo                     | Tipo    | Valor predeterminado | Descripción                                                             |
| ------------------------- | ------- | -------------------- | ----------------------------------------------------------------------- |
| `group_id`                | number  | -                    | ID del grupo                                                            |
| `anonymous`               | object  | -                    | Objeto de usuario anónimo (de eventos de mensajes de grupo)             |
| `anonymous_flag` o `flag` | string  | -                    | Flag de usuario anónimo (de eventos de mensajes de grupo)               |
| `duration`                | number  | `30 * 60`            | Duración en segundos; el silencio anónimo no se puede cancelar          |

Indica `anonymous` o `anonymous_flag`. Si se proporcionan ambos, se usa `anonymous`.

##### Respuesta

Ninguna.

#### `set_group_whole_ban` silenciar a todos

##### Parámetros

| Campo      | Tipo    | Valor predeterminado | Descripción |
| ---------- | ------- | -------------------- | ----------- |
| `group_id` | number  | -                    | ID del grupo |
| `enable`   | boolean | `true`               | Habilitar silencio |

##### Respuesta

Ninguna.

#### `set_group_admin` establecer administrador

##### Parámetros

| Campo      | Tipo    | Valor predeterminado | Descripción                           |
| ---------- | ------- | -------------------- | ------------------------------------- |
| `group_id` | number  | -                    | ID del grupo                          |
| `user_id`  | number  | -                    | Número QQ a promover                  |
| `enable`   | boolean | `true`               | `true` para establecer, `false` para quitar |

##### Respuesta

Ninguna.

#### `set_group_anonymous` habilitar modo anónimo

##### Parámetros

| Campo      | Tipo    | Valor predeterminado | Descripción                |
| ---------- | ------- | -------------------- | -------------------------- |
| `group_id` | number  | -                    | ID del grupo               |
| `enable`   | boolean | `true`               | Permitir chat anónimo      |

##### Respuesta

Ninguna.

#### `set_group_card` establecer tarjeta del grupo

##### Parámetros

| Campo      | Tipo   | Valor predeterminado | Descripción                                       |
| ---------- | ------ | -------------------- | ------------------------------------------------- |
| `group_id` | number | -                    | ID del grupo                                      |
| `user_id`  | number | -                    | Número QQ a actualizar                            |
| `card`     | string | vacío                | Contenido de la tarjeta; vacío la elimina        |

##### Respuesta

Ninguna.

#### `set_group_leave` abandonar grupo

##### Parámetros

| Campo       | Tipo    | Valor predeterminado | Descripción                                      |
| ----------- | ------- | -------------------- | ------------------------------------------------ |
| `group_id`  | number  | -                    | ID del grupo                                     |
| `is_dismiss`| boolean | `false`              | Disolver el grupo si el bot es el propietario   |

##### Respuesta

Ninguna.

#### `set_group_special_title` establecer título especial

##### Parámetros

| Campo          | Tipo   | Valor predeterminado | Descripción                                                  |
| -------------- | ------ | -------------------- | ------------------------------------------------------------ |
| `group_id`     | number | -                    | ID del grupo                                                 |
| `user_id`      | number | -                    | Número QQ a actualizar                                       |
| `special_title`| string | vacío                | Título especial; vacío lo elimina                            |
| `duration`     | number | `-1`                 | Duración en segundos; `-1` significa permanente (puede variar) |

##### Respuesta

Ninguna.

#### `set_discuss_leave` abandonar discusión

##### Parámetros

| Campo        | Tipo   | Valor predeterminado | Descripción                                                          |
| ------------ | ------ | -------------------- | -------------------------------------------------------------------- |
| `discuss_id` | number | -                    | ID de discusión (obtener de eventos si está oculto)                  |

##### Respuesta

Ninguna.

### Gestionar solicitudes

#### `set_friend_add_request` gestionar solicitud de amistad

##### Parámetros

| Campo     | Tipo    | Valor predeterminado | Descripción                                  |
| --------- | ------- | -------------------- | -------------------------------------------- |
| `flag`    | string  | -                    | Flag de la solicitud (del evento)           |
| `approve` | boolean | `true`               | Aprobar la solicitud                         |
| `remark`  | string  | vacío                | Nota a añadir al aprobar                     |

##### Respuesta

Ninguna.

#### `set_group_add_request` gestionar solicitud/invitación de grupo

##### Parámetros

| Campo                  | Tipo    | Valor predeterminado | Descripción                                                         |
| ---------------------- | ------- | -------------------- | ------------------------------------------------------------------- |
| `flag`                 | string  | -                    | Flag de la solicitud (del evento)                                   |
| `sub_type` o `type`    | string  | -                    | `add` o `invite` (debe coincidir con `sub_type` del evento)         |
| `approve`              | boolean | `true`               | Aprobar solicitud/invitación                                        |
| `reason`               | string  | vacío                | Motivo del rechazo (solo si se rechaza)                             |

##### Respuesta

Ninguna.

### Obtener información

#### `get_login_info` obtener información de inicio de sesión

##### Parámetros

Ninguno.

##### Respuesta

| Campo      | Tipo           | Descripción |
| ---------- | -------------- | ----------- |
| `user_id`  | number (int64) | Número QQ   |
| `nickname` | string         | Apodo QQ    |

#### `get_stranger_info` obtener información de desconocido

##### Parámetros

| Campo     | Tipo    | Valor predeterminado | Descripción                                |
| --------- | ------- | -------------------- | ------------------------------------------ |
| `user_id` | number  | -                    | Número QQ                                  |
| `no_cache`| boolean | `false`              | Desactivar caché (más lento pero actualizado) |

##### Respuesta

| Campo     | Tipo           | Descripción                          |
| --------- | -------------- | ------------------------------------ |
| `user_id` | number (int64) | Número QQ                            |
| `nickname`| string         | Apodo                                |
| `sex`     | string         | `male`, `female` o `unknown`         |
| `age`     | number (int32) | Edad                                 |

#### `get_friend_list` obtener lista de amigos

##### Parámetros

Ninguno.

##### Respuesta

La respuesta es un arreglo JSON. Cada elemento contiene:

| Campo     | Tipo           | Descripción |
| --------- | -------------- | ----------- |
| `user_id` | number (int64) | Número QQ   |
| `nickname`| string         | Apodo       |
| `remark`  | string         | Nota        |

#### `get_group_list` obtener lista de grupos

##### Parámetros

Ninguno.

##### Respuesta

La respuesta es un arreglo JSON. Cada elemento contiene:

| Campo       | Tipo           | Descripción |
| ---------- | -------------- | ----------- |
| `group_id`  | number (int64) | ID del grupo |
| `group_name`| string         | Nombre del grupo |

#### `get_group_info` obtener información del grupo

##### Parámetros

| Campo     | Tipo    | Valor predeterminado | Descripción                                |
| --------- | ------- | -------------------- | ------------------------------------------ |
| `group_id`| number  | -                    | ID del grupo                               |
| `no_cache`| boolean | `false`              | Desactivar caché (más lento pero actualizado) |

##### Respuesta

| Campo              | Tipo           | Descripción           |
| ----------------- | -------------- | --------------------- |
| `group_id`         | number (int64) | ID del grupo          |
| `group_name`       | string         | Nombre del grupo      |
| `member_count`     | number (int32) | Número de miembros    |
| `max_member_count` | number (int32) | Capacidad máxima      |

#### `get_group_member_info` obtener información del miembro

##### Parámetros

| Campo     | Tipo    | Valor predeterminado | Descripción                                |
| --------- | ------- | -------------------- | ------------------------------------------ |
| `group_id`| number  | -                    | ID del grupo                               |
| `user_id` | number  | -                    | Número QQ                                 |
| `no_cache`| boolean | `false`              | Desactivar caché (más lento pero actualizado) |

##### Respuesta

| Campo               | Tipo           | Descripción                               |
| ------------------- | -------------- | ----------------------------------------- |
| `group_id`          | number (int64) | ID del grupo                              |
| `user_id`           | number (int64) | Número QQ                                 |
| `nickname`          | string         | Apodo                                      |
| `card`              | string         | Tarjeta/nota del grupo                    |
| `sex`               | string         | `male`, `female` o `unknown`              |
| `age`               | number (int32) | Edad                                       |
| `area`              | string         | Región                                     |
| `join_time`         | number (int32) | Marca de tiempo de ingreso                 |
| `last_sent_time`    | number (int32) | Marca de tiempo del último mensaje         |
| `level`             | string         | Nivel del miembro                          |
| `role`              | string         | `owner`, `admin` o `member`                |
| `unfriendly`        | boolean        | Indica si el miembro es marcado            |
| `title`             | string         | Título especial                            |
| `title_expire_time` | number (int32) | Caducidad del título especial              |
| `card_changeable`   | boolean        | Permite modificar la tarjeta               |

#### `get_group_member_list` obtener lista de miembros

##### Parámetros

| Campo     | Tipo   | Valor predeterminado | Descripción |
| --------- | ------ | -------------------- | ----------- |
| `group_id`| number | -                    | ID del grupo |

##### Respuesta

La respuesta es un arreglo JSON. Cada elemento tiene los campos de `get_group_member_info`, pero algunos campos (como `area` o `title`) pueden faltar. Usa la consulta individual para más detalle.

#### `get_cookies` obtener cookies

##### Parámetros

| Campo   | Tipo   | Valor predeterminado | Descripción                     |
| ------- | ------ | -------------------- | ------------------------------- |
| `domain`| string | vacío                | Dominio del que se obtienen cookies |

##### Respuesta

| Campo    | Tipo   | Descripción |
| -------- | ------ | ----------- |
| `cookies`| string | Cookies     |

#### `get_csrf_token` obtener token CSRF

##### Parámetros

Ninguno.

##### Respuesta

| Campo  | Tipo           | Descripción |
| ------ | -------------- | ----------- |
| `token`| number (int32) | Token CSRF  |

#### `get_credentials` obtener credenciales QQ

Combina `get_cookies` y `get_csrf_token`.

##### Parámetros

Ninguno.

##### Respuesta

| Campo       | Tipo           | Descripción |
| ----------- | -------------- | ----------- |
| `cookies`   | string         | Cookies     |
| `csrf_token`| number (int32) | Token CSRF  |

#### `get_record` obtener grabación de voz

Convierte el mensaje de voz al formato indicado y devuelve el nombre del archivo (guardado en `data\record`). **Para usar esta API, instala el [componente de voz](https://cqp.cc/t/21132) de CoolQ.**

##### Parámetros

| Campo        | Tipo   | Valor predeterminado | Descripción                                                                 |
| ------------ | ------ | -------------------- | --------------------------------------------------------------------------- |
| `file`       | string | -                    | Nombre de archivo del mensaje de voz, p. ej. `0B38145AA44505000B38145AA4450500.silk` |
| `out_format` | string | -                    | Formato: `mp3`, `amr`, `wma`, `m4a`, `spx`, `ogg`, `wav`, `flac`             |
| `full_path`  | boolean| `false`              | Devolver ruta absoluta (recomendado en Windows, no en Docker)               |

##### Respuesta

| Campo | Tipo   | Descripción                                                                                          |
| ----- | ------ | ---------------------------------------------------------------------------------------------------- |
| `file`| string | Nombre o ruta del archivo convertido (ruta completa si `full_path` es `true`)                       |

#### `get_image` obtener imagen

##### Parámetros

| Campo | Tipo   | Valor predeterminado | Descripción                                                            |
| ----- | ------ | -------------------- | ---------------------------------------------------------------------- |
| `file`| string | -                    | Nombre del archivo de imagen, p. ej. `6B4DE3DFD1BD271E3297859D41C530F5.jpg` |

##### Respuesta

| Campo | Tipo   | Descripción                                                                                  |
| ----- | ------ | -------------------------------------------------------------------------------------------- |
| `file`| string | Ruta de la imagen descargada, p. ej. `C:\Apps\CoolQ\data\image\...`                       |

### Autocomprobación

#### `can_send_image` comprobar envío de imágenes

##### Parámetros

Ninguno.

##### Respuesta

| Campo | Tipo    | Descripción |
| ----- | ------- | ----------- |
| `yes` | boolean | Sí o no     |

#### `can_send_record` comprobar envío de audio

##### Parámetros

Ninguno.

##### Respuesta

| Campo | Tipo    | Descripción |
| ----- | ------- | ----------- |
| `yes` | boolean | Sí o no     |

#### `get_status` obtener estado del complemento

##### Parámetros

Ninguno.

##### Respuesta

| Campo             | Tipo    | Descripción                                                      |
| ----------------- | ------- | ---------------------------------------------------------------- |
| `app_initialized` | boolean | Complemento HTTP API inicializado                                |
| `app_enabled`     | boolean | Complemento HTTP API habilitado                                  |
| `plugins_good`    | object  | Los complementos internos funcionan correctamente                |
| `app_good`        | boolean | Complemento en buen estado (inicializado, habilitado, interno OK) |
| `online`          | boolean | Estado en línea (`null` si no se puede comprobar)               |
| `good`            | boolean | Estado esperado del complemento                                  |

Normalmente basta con `online` y `good`.

El estado `online` puede detectarse con `online_status_detection_method`:

| Método                       | Ventajas                                                    | Desventajas                                                  |
| ---------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
| `get_stranger_info` (por defecto) | Más preciso en la mayoría de casos; requiere red        | Puede ser inexacto si se consulta con demasiada frecuencia   |
| `log_db`                     | Rápido; sin solicitudes de red                             | Puede fallar si CoolQ cambia la base de datos; problemas en fin de mes |

#### `get_version_info` obtener información de versión

##### Parámetros

Ninguno.

##### Respuesta

| Campo                        | Tipo   | Descripción                                  |
| --------------------------- | ------ | -------------------------------------------- |
| `coolq_directory`           | string | Ruta raíz de CoolQ                           |
| `coolq_edition`             | string | Edición de CoolQ, `air` o `pro`              |
| `plugin_version`            | string | Versión del complemento HTTP API (ej. `2.1.3`) |
| `plugin_build_number`       | number | Número de compilación del complemento        |
| `plugin_build_configuration`| string | Configuración de compilación, `debug` o `release` |

#### `set_restart_plugin` reiniciar el complemento HTTP API

Reiniciar el complemento también reinicia el servicio API, por lo que las solicitudes actuales se interrumpen. La respuesta devuelve `status` como `async`.

##### Parámetros

| Campo  | Tipo   | Valor predeterminado | Descripción                                              |
| ------ | ------ | -------------------- | -------------------------------------------------------- |
| `delay`| number | `0`                  | Retardo en milisegundos; prueba 2000 si falla             |

##### Respuesta

Ninguna.

#### `clean_data_dir` limpiar directorio de datos

Limpia archivos acumulados en `image`, `record`, `show` o `bface`.

##### Parámetros

| Campo     | Tipo   | Valor predeterminado | Descripción                                      |
| --------- | ------ | -------------------- | ------------------------------------------------ |
| `data_dir`| string | -                    | Nombre del directorio: `image`, `record`, `show`, `bface` |

##### Respuesta

Ninguna.

#### `clean_plugin_log` limpiar registros del complemento

Elimina los archivos de registro del complemento.

##### Parámetros

Ninguno.

##### Respuesta

Ninguna.
