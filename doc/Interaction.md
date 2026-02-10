# Chat Interaction and Group Management

[TOC]

[English](Interaction.md) | [简体中文](Interaction_zh-CN.md) | [Deutsch](Interaction_de.md) | [Español](Interaction_es.md) | [Français](Interaction_fr.md)

## Overview

This document summarizes the interaction and group management APIs used by the bot. The endpoints come from the CoolQ HTTP API plugin. For the full API reference, see the plugin documentation.

## API

### Basic interaction

#### `send_private_msg` send a private message

##### Parameters

| Field         | Type    | Default | Description                                                                 |
| ------------- | ------- | ------- | --------------------------------------------------------------------------- |
| `user_id`     | number  | -       | Target QQ number                                                            |
| `message`     | message | -       | Message content                                                             |
| `auto_escape` | boolean | `false` | Send message as plain text (do not parse CQ codes); only valid if `message` is a string |

##### Response

| Field        | Type          | Description |
| ------------ | ------------- | ----------- |
| `message_id` | number (int32) | Message ID  |

#### `send_group_msg` send a group message

##### Parameters

| Field         | Type    | Default | Description                                                                 |
| ------------- | ------- | ------- | --------------------------------------------------------------------------- |
| `group_id`    | number  | -       | Group ID                                                                    |
| `message`     | message | -       | Message content                                                             |
| `auto_escape` | boolean | `false` | Send message as plain text (do not parse CQ codes); only valid if `message` is a string |

##### Response

| Field        | Type          | Description |
| ------------ | ------------- | ----------- |
| `message_id` | number (int32) | Message ID  |

#### `send_discuss_msg` send a discussion message

##### Parameters

| Field         | Type    | Default | Description                                                                 |
| ------------- | ------- | ------- | --------------------------------------------------------------------------- |
| `discuss_id`  | number  | -       | Discussion ID (not visible in most clients; obtain it from discussion message events) |
| `message`     | message | -       | Message content                                                             |
| `auto_escape` | boolean | `false` | Send message as plain text (do not parse CQ codes); only valid if `message` is a string |

##### Response

| Field        | Type          | Description |
| ------------ | ------------- | ----------- |
| `message_id` | number (int32) | Message ID  |

#### `send_msg` send a message

##### Parameters

| Field          | Type    | Default | Description                                                                 |
| -------------- | ------- | ------- | --------------------------------------------------------------------------- |
| `message_type` | string  | -       | Message type: `private`, `group`, or `discuss`. If omitted, it is inferred from the `*_id` fields. |
| `user_id`      | number  | -       | Target QQ number (required when `message_type` is `private`)                |
| `group_id`     | number  | -       | Group ID (required when `message_type` is `group`)                          |
| `discuss_id`   | number  | -       | Discussion ID (required when `message_type` is `discuss`)                   |
| `message`      | message | -       | Message content                                                             |
| `auto_escape`  | boolean | `false` | Send message as plain text (do not parse CQ codes); only valid if `message` is a string |

##### Response

| Field        | Type          | Description |
| ------------ | ------------- | ----------- |
| `message_id` | number (int32) | Message ID  |

#### `delete_msg` recall a message

##### Parameters

| Field        | Type          | Default | Description |
| ------------ | ------------- | ------- | ----------- |
| `message_id` | number (int32) | -       | Message ID  |

##### Response

None.

#### `send_like` send a like

##### Parameters

| Field     | Type   | Default | Description                          |
| --------- | ------ | ------- | ------------------------------------ |
| `user_id` | number | -       | Target QQ number                     |
| `times`   | number | 1       | Like count (max 10 per friend per day) |

##### Response

None.

### Group management

#### `set_group_kick` kick a member

##### Parameters

| Field                 | Type    | Default | Description                   |
| --------------------- | ------- | ------- | ----------------------------- |
| `group_id`            | number  | -       | Group ID                      |
| `user_id`             | number  | -       | QQ number to remove           |
| `reject_add_request`  | boolean | `false` | Reject future join requests   |

##### Response

None.

#### `set_group_ban` mute a member

##### Parameters

| Field      | Type    | Default    | Description                                |
| ---------- | ------- | ---------- | ------------------------------------------ |
| `group_id` | number  | -          | Group ID                                   |
| `user_id`  | number  | -          | QQ number to mute                          |
| `duration` | number  | `30 * 60`  | Mute duration in seconds; 0 cancels mute   |

##### Response

None.

#### `set_group_anonymous_ban` mute an anonymous user

##### Parameters

| Field                   | Type    | Default   | Description                                                   |
| ----------------------- | ------- | --------- | ------------------------------------------------------------- |
| `group_id`              | number  | -         | Group ID                                                      |
| `anonymous`             | object  | -         | Optional anonymous user object (from group message event)     |
| `anonymous_flag` or `flag` | string | -       | Optional anonymous user flag (from group message event)       |
| `duration`              | number  | `30 * 60` | Mute duration in seconds; anonymous mutes cannot be canceled  |

Provide either `anonymous` or `anonymous_flag`. If both are provided, `anonymous` is used.

##### Response

None.

#### `set_group_whole_ban` mute all members

##### Parameters

| Field      | Type    | Default | Description |
| ---------- | ------- | ------- | ----------- |
| `group_id` | number  | -       | Group ID    |
| `enable`   | boolean | `true`  | Enable mute |

##### Response

None.

#### `set_group_admin` set an admin

##### Parameters

| Field      | Type    | Default | Description                              |
| ---------- | ------- | ------- | ---------------------------------------- |
| `group_id` | number  | -       | Group ID                                 |
| `user_id`  | number  | -       | QQ number to promote                     |
| `enable`   | boolean | `true`  | `true` to set, `false` to unset          |

##### Response

None.

#### `set_group_anonymous` enable anonymous mode

##### Parameters

| Field      | Type    | Default | Description                   |
| ---------- | ------- | ------- | ----------------------------- |
| `group_id` | number  | -       | Group ID                      |
| `enable`   | boolean | `true`  | Allow anonymous chatting      |

##### Response

None.

#### `set_group_card` set a member card

##### Parameters

| Field      | Type   | Default | Description                                       |
| ---------- | ------ | ------- | ------------------------------------------------- |
| `group_id` | number | -       | Group ID                                          |
| `user_id`  | number | -       | QQ number to update                               |
| `card`     | string | empty   | Card content; empty string removes the card       |

##### Response

None.

#### `set_group_leave` leave a group

##### Parameters

| Field       | Type    | Default | Description                                               |
| ----------- | ------- | ------- | --------------------------------------------------------- |
| `group_id`  | number  | -       | Group ID                                                  |
| `is_dismiss`| boolean | `false` | Dismiss the group if the bot account is the owner         |

##### Response

None.

#### `set_group_special_title` set a special title

##### Parameters

| Field          | Type   | Default | Description                                                            |
| -------------- | ------ | ------- | ---------------------------------------------------------------------- |
| `group_id`     | number | -       | Group ID                                                               |
| `user_id`      | number | -       | QQ number to update                                                    |
| `special_title`| string | empty   | Title to set; empty string removes the special title                   |
| `duration`     | number | `-1`    | Duration in seconds; `-1` means permanent (behavior may vary)          |

##### Response

None.

#### `set_discuss_leave` leave a discussion group

##### Parameters

| Field        | Type   | Default | Description                                                        |
| ------------ | ------ | ------- | ------------------------------------------------------------------ |
| `discuss_id` | number | -       | Discussion ID (obtain from discussion message events if hidden)    |

##### Response

None.

### Handle requests

#### `set_friend_add_request` handle friend requests

##### Parameters

| Field     | Type    | Default | Description                                      |
| --------- | ------- | ------- | ------------------------------------------------ |
| `flag`    | string  | -       | Friend request flag (from event payload)         |
| `approve` | boolean | `true`  | Whether to approve the request                   |
| `remark`  | string  | empty   | Remark to set when approved                      |

##### Response

None.

#### `set_group_add_request` handle group requests/invites

##### Parameters

| Field                  | Type    | Default | Description                                                         |
| ---------------------- | ------- | ------- | ------------------------------------------------------------------- |
| `flag`                 | string  | -       | Group request flag (from event payload)                             |
| `sub_type` or `type`   | string  | -       | `add` or `invite` (must match the event `sub_type`)                 |
| `approve`              | boolean | `true`  | Whether to approve the request/invite                               |
| `reason`               | string  | empty   | Reason for rejection (only used when rejecting)                     |

##### Response

None.

### Get information

#### `get_login_info` get login information

##### Parameters

None.

##### Response

| Field     | Type           | Description |
| --------- | -------------- | ----------- |
| `user_id` | number (int64) | QQ number   |
| `nickname`| string         | QQ nickname |

#### `get_stranger_info` get stranger information

##### Parameters

| Field     | Type    | Default | Description                                |
| --------- | ------- | ------- | ------------------------------------------ |
| `user_id` | number  | -       | QQ number                                  |
| `no_cache`| boolean | `false` | Disable cache (slower but more up to date) |

##### Response

| Field     | Type           | Description                                |
| --------- | -------------- | ------------------------------------------ |
| `user_id` | number (int64) | QQ number                                  |
| `nickname`| string         | Nickname                                   |
| `sex`     | string         | `male`, `female`, or `unknown`             |
| `age`     | number (int32) | Age                                        |

#### `get_friend_list` get friend list

##### Parameters

None.

##### Response

Response is a JSON array. Each element contains:

| Field     | Type           | Description |
| --------- | -------------- | ----------- |
| `user_id` | number (int64) | QQ number   |
| `nickname`| string         | Nickname    |
| `remark`  | string         | Remark      |

#### `get_group_list` get group list

##### Parameters

None.

##### Response

Response is a JSON array. Each element contains:

| Field       | Type           | Description |
| ----------- | -------------- | ----------- |
| `group_id`  | number (int64) | Group ID    |
| `group_name`| string         | Group name  |

#### `get_group_info` get group information

##### Parameters

| Field     | Type    | Default | Description                                |
| --------- | ------- | ------- | ------------------------------------------ |
| `group_id`| number  | -       | Group ID                                   |
| `no_cache`| boolean | `false` | Disable cache (slower but more up to date) |

##### Response

| Field              | Type           | Description           |
| ------------------ | -------------- | --------------------- |
| `group_id`         | number (int64) | Group ID              |
| `group_name`       | string         | Group name            |
| `member_count`     | number (int32) | Member count          |
| `max_member_count` | number (int32) | Max group members     |

#### `get_group_member_info` get group member information

##### Parameters

| Field     | Type    | Default | Description                                |
| --------- | ------- | ------- | ------------------------------------------ |
| `group_id`| number  | -       | Group ID                                   |
| `user_id` | number  | -       | QQ number                                  |
| `no_cache`| boolean | `false` | Disable cache (slower but more up to date) |

##### Response

| Field               | Type           | Description                               |
| ------------------- | -------------- | ----------------------------------------- |
| `group_id`          | number (int64) | Group ID                                  |
| `user_id`           | number (int64) | QQ number                                 |
| `nickname`          | string         | Nickname                                  |
| `card`              | string         | Group card/remark                          |
| `sex`               | string         | `male`, `female`, or `unknown`            |
| `age`               | number (int32) | Age                                       |
| `area`              | string         | Area                                      |
| `join_time`         | number (int32) | Join timestamp                             |
| `last_sent_time`    | number (int32) | Last message timestamp                     |
| `level`             | string         | Member level                               |
| `role`              | string         | `owner`, `admin`, or `member`             |
| `unfriendly`        | boolean        | Whether the member is flagged              |
| `title`             | string         | Special title                              |
| `title_expire_time` | number (int32) | Special title expiration timestamp         |
| `card_changeable`   | boolean        | Whether the card can be changed            |

#### `get_group_member_list` get group member list

##### Parameters

| Field     | Type   | Default | Description |
| --------- | ------ | ------- | ----------- |
| `group_id`| number | -       | Group ID    |

##### Response

Response is a JSON array. Each element has the same fields as `get_group_member_info`, but some fields (such as `area` and `title`) may be missing. Use `get_group_member_info` for the full detail of a specific member.

#### `get_cookies` get cookies

##### Parameters

| Field    | Type   | Default | Description                |
| -------- | ------ | ------- | -------------------------- |
| `domain` | string | empty   | Domain to fetch cookies for |

##### Response

| Field    | Type   | Description |
| -------- | ------ | ----------- |
| `cookies`| string | Cookies     |

#### `get_csrf_token` get CSRF token

##### Parameters

None.

##### Response

| Field  | Type           | Description |
| ------ | -------------- | ----------- |
| `token`| number (int32) | CSRF token  |

#### `get_credentials` get QQ credential bundle

This is a combined response of `get_cookies` and `get_csrf_token`.

##### Parameters

None.

##### Response

| Field       | Type           | Description |
| ----------- | -------------- | ----------- |
| `cookies`   | string         | Cookies     |
| `csrf_token`| number (int32) | CSRF token  |

#### `get_record` get voice recording

This endpoint converts a voice message to the specified format and returns the file name (stored under the `data\record` directory). **To use this API, install the CoolQ [voice component](https://cqp.cc/t/21132).**

##### Parameters

| Field       | Type    | Default | Description                                                                 |
| ----------- | ------- | ------- | --------------------------------------------------------------------------- |
| `file`      | string  | -       | Voice file name from CQ code, e.g. `0B38145AA44505000B38145AA4450500.silk`   |
| `out_format`| string  | -       | Output format: `mp3`, `amr`, `wma`, `m4a`, `spx`, `ogg`, `wav`, `flac`       |
| `full_path` | boolean | `false` | Return absolute path (recommended on Windows, not in Docker)                |

##### Response

| Field | Type   | Description                                                                                                    |
| ----- | ------ | -------------------------------------------------------------------------------------------------------------- |
| `file`| string | Converted file name or path, e.g. `0B38145AA44505000B38145AA4450500.mp3` (absolute path when `full_path` is true) |

#### `get_image` get image

##### Parameters

| Field | Type   | Default | Description                                                                  |
| ----- | ------ | ------- | ---------------------------------------------------------------------------- |
| `file`| string | -       | Image file name from CQ code, e.g. `6B4DE3DFD1BD271E3297859D41C530F5.jpg`     |

##### Response

| Field | Type   | Description                                                                             |
| ----- | ------ | --------------------------------------------------------------------------------------- |
| `file`| string | Downloaded image path, e.g. `C:\Apps\CoolQ\data\image\6B4DE3DFD1BD271E3297859D41C530F5.jpg` |

### Self-check

#### `can_send_image` check image capability

##### Parameters

None.

##### Response

| Field | Type    | Description |
| ----- | ------- | ----------- |
| `yes` | boolean | Yes or no   |

#### `can_send_record` check voice capability

##### Parameters

None.

##### Response

| Field | Type    | Description |
| ----- | ------- | ----------- |
| `yes` | boolean | Yes or no   |

#### `get_status` get plugin status

##### Parameters

None.

##### Response

| Field             | Type    | Description                                                     |
| ----------------- | ------- | --------------------------------------------------------------- |
| `app_initialized` | boolean | HTTP API plugin initialized                                     |
| `app_enabled`     | boolean | HTTP API plugin enabled                                         |
| `plugins_good`    | object  | Whether internal plugins are running properly                   |
| `app_good`        | boolean | Plugin running properly (initialized, enabled, plugins healthy) |
| `online`          | boolean | QQ online status (`null` if unknown)                            |
| `good`            | boolean | Plugin status matches expectations                              |

Usually, `online` and `good` are sufficient for health checks. Other fields may change as the plugin evolves.

The `online` status can be detected using two methods, configured by `online_status_detection_method`:

| Detection method             | Pros                                                                 | Cons                                                                 |
| ---------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `get_stranger_info` (default)| More accurate than `log_db` in most cases; requires network requests  | Can be inaccurate if requests are too frequent                       |
| `log_db`                     | Fast query; no network requests (avoids Tencent risk control)         | Might break if CoolQ changes database schema; month-boundary issues   |

#### `get_version_info` get version information

##### Parameters

None.

##### Response

| Field                       | Type    | Description                           |
| --------------------------- | ------- | ------------------------------------- |
| `coolq_directory`           | string  | CoolQ root directory                   |
| `coolq_edition`             | string  | CoolQ edition, `air` or `pro`         |
| `plugin_version`            | string  | HTTP API plugin version (e.g. `2.1.3`) |
| `plugin_build_number`       | number  | HTTP API plugin build number          |
| `plugin_build_configuration`| string  | Plugin build configuration, `debug` or `release` |

#### `set_restart_plugin` restart the HTTP API plugin

Restarting the plugin also restarts the API service, so existing API requests will be interrupted. The response `status` is `async`.

##### Parameters

| Field  | Type   | Default | Description                                                   |
| ------ | ------ | ------- | ------------------------------------------------------------- |
| `delay`| number | `0`     | Delay in milliseconds; try 2000 if immediate restart fails     |

##### Response

None.

#### `clean_data_dir` clean data directory

Clean accumulated files under `image`, `record`, `show`, or `bface`.

##### Parameters

| Field    | Type   | Default | Description                                              |
| -------- | ------ | ------- | -------------------------------------------------------- |
| `data_dir`| string | -      | Directory name: `image`, `record`, `show`, or `bface`     |

##### Response

None.

#### `clean_plugin_log` clean plugin logs

Clear the plugin log files.

##### Parameters

None.

##### Response

None.
