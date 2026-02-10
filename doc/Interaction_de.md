# Chat-Interaktion und Gruppenverwaltung

[TOC]

[English](Interaction.md) | [简体中文](Interaction_zh-CN.md) | [Deutsch](Interaction_de.md) | [Español](Interaction_es.md) | [Français](Interaction_fr.md)

## Überblick

Dieses Dokument fasst die Interaktions- und Gruppenverwaltungs-APIs zusammen, die der Bot verwendet. Die Endpunkte stammen aus dem CoolQ HTTP API Plugin. Für die vollständige Referenz siehe die Plugin-Dokumentation.

## API

### Grundlegende Interaktion

#### `send_private_msg` private Nachricht senden

##### Parameter

| Feld          | Typ     | Standard | Beschreibung                                                                 |
| ------------- | ------- | -------- | ---------------------------------------------------------------------------- |
| `user_id`     | number  | -        | Ziel-QQ-Nummer                                                               |
| `message`     | message | -        | Nachrichteninhalt                                                           |
| `auto_escape` | boolean | `false`  | Nachricht als Klartext senden (keine CQ-Codes); nur gültig, wenn `message` ein String ist |

##### Antwort

| Feld        | Typ            | Beschreibung |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | Nachrichten-ID |

#### `send_group_msg` Gruppennachricht senden

##### Parameter

| Feld          | Typ     | Standard | Beschreibung                                                                 |
| ------------- | ------- | -------- | ---------------------------------------------------------------------------- |
| `group_id`    | number  | -        | Gruppen-ID                                                                    |
| `message`     | message | -        | Nachrichteninhalt                                                           |
| `auto_escape` | boolean | `false`  | Nachricht als Klartext senden (keine CQ-Codes); nur gültig, wenn `message` ein String ist |

##### Antwort

| Feld        | Typ            | Beschreibung |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | Nachrichten-ID |

#### `send_discuss_msg` Nachricht in Diskussion senden

##### Parameter

| Feld          | Typ     | Standard | Beschreibung                                                                 |
| ------------- | ------- | -------- | ---------------------------------------------------------------------------- |
| `discuss_id`  | number  | -        | Diskussions-ID (oft nicht sichtbar; aus Diskussionsevents ableiten)          |
| `message`     | message | -        | Nachrichteninhalt                                                           |
| `auto_escape` | boolean | `false`  | Nachricht als Klartext senden (keine CQ-Codes); nur gültig, wenn `message` ein String ist |

##### Antwort

| Feld        | Typ            | Beschreibung |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | Nachrichten-ID |

#### `send_msg` Nachricht senden

##### Parameter

| Feld           | Typ     | Standard | Beschreibung                                                                 |
| -------------- | ------- | -------- | ---------------------------------------------------------------------------- |
| `message_type` | string  | -        | Nachrichtentyp: `private`, `group`, `discuss`. Ohne Angabe wird er aus `*_id` abgeleitet |
| `user_id`      | number  | -        | Ziel-QQ-Nummer (erforderlich bei `private`)                                   |
| `group_id`     | number  | -        | Gruppen-ID (erforderlich bei `group`)                                         |
| `discuss_id`   | number  | -        | Diskussions-ID (erforderlich bei `discuss`)                                   |
| `message`      | message | -        | Nachrichteninhalt                                                           |
| `auto_escape`  | boolean | `false`  | Nachricht als Klartext senden (keine CQ-Codes); nur gültig, wenn `message` ein String ist |

##### Antwort

| Feld        | Typ            | Beschreibung |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | Nachrichten-ID |

#### `delete_msg` Nachricht zurückziehen

##### Parameter

| Feld        | Typ            | Standard | Beschreibung |
| ----------- | -------------- | -------- | ------------ |
| `message_id`| number (int32) | -        | Nachrichten-ID |

##### Antwort

Keine.

#### `send_like` Like senden

##### Parameter

| Feld     | Typ    | Standard | Beschreibung                                  |
| -------- | ------ | -------- | --------------------------------------------- |
| `user_id`| number | -        | Ziel-QQ-Nummer                                 |
| `times`  | number | 1        | Anzahl der Likes (max. 10 pro Freund und Tag) |

##### Antwort

Keine.

### Gruppenverwaltung

#### `set_group_kick` Mitglied entfernen

##### Parameter

| Feld                 | Typ     | Standard | Beschreibung                       |
| -------------------- | ------- | -------- | ---------------------------------- |
| `group_id`           | number  | -        | Gruppen-ID                          |
| `user_id`            | number  | -        | QQ-Nummer des Mitglieds             |
| `reject_add_request` | boolean | `false`  | Weitere Beitrittsanfragen ablehnen |

##### Antwort

Keine.

#### `set_group_ban` Mitglied stummschalten

##### Parameter

| Feld      | Typ    | Standard    | Beschreibung                                  |
| --------- | ------ | ---------- | --------------------------------------------- |
| `group_id`| number | -          | Gruppen-ID                                     |
| `user_id` | number | -          | QQ-Nummer des Mitglieds                        |
| `duration`| number | `30 * 60`  | Dauer in Sekunden; 0 hebt Stummschaltung auf   |

##### Antwort

Keine.

#### `set_group_anonymous_ban` anonymen Nutzer stummschalten

##### Parameter

| Feld                     | Typ     | Standard   | Beschreibung                                                      |
| ------------------------ | ------- | ---------- | ----------------------------------------------------------------- |
| `group_id`               | number  | -          | Gruppen-ID                                                         |
| `anonymous`              | object  | -          | Optionales anonymes Nutzerobjekt (aus Gruppen-Events)              |
| `anonymous_flag` oder `flag` | string | -       | Optionales anonymes Flag (aus Gruppen-Events)                      |
| `duration`               | number  | `30 * 60`  | Dauer in Sekunden; anonymes Stummschalten kann nicht aufgehoben werden |

Gib entweder `anonymous` oder `anonymous_flag` an. Wenn beide vorhanden sind, wird `anonymous` verwendet.

##### Antwort

Keine.

#### `set_group_whole_ban` Alle stummschalten

##### Parameter

| Feld      | Typ    | Standard | Beschreibung |
| --------- | ------ | -------- | ------------ |
| `group_id`| number | -        | Gruppen-ID    |
| `enable`  | boolean| `true`   | Stummschaltung aktivieren |

##### Antwort

Keine.

#### `set_group_admin` Admin festlegen

##### Parameter

| Feld      | Typ    | Standard | Beschreibung                         |
| --------- | ------ | -------- | ------------------------------------ |
| `group_id`| number | -        | Gruppen-ID                            |
| `user_id` | number | -        | QQ-Nummer des Mitglieds               |
| `enable`  | boolean| `true`   | `true` setzen, `false` entfernen     |

##### Antwort

Keine.

#### `set_group_anonymous` anonymen Modus aktivieren

##### Parameter

| Feld      | Typ    | Standard | Beschreibung                |
| --------- | ------ | -------- | --------------------------- |
| `group_id`| number | -        | Gruppen-ID                   |
| `enable`  | boolean| `true`   | Anonymes Chatten erlauben    |

##### Antwort

Keine.

#### `set_group_card` Gruppenkarte setzen

##### Parameter

| Feld      | Typ   | Standard | Beschreibung                                      |
| --------- | ----- | -------- | ------------------------------------------------ |
| `group_id`| number| -        | Gruppen-ID                                        |
| `user_id` | number| -        | QQ-Nummer des Mitglieds                           |
| `card`    | string| leer     | Karteninhalt; leerer String löscht die Karte      |

##### Antwort

Keine.

#### `set_group_leave` Gruppe verlassen

##### Parameter

| Feld        | Typ     | Standard | Beschreibung                                       |
| ----------- | ------- | -------- | ------------------------------------------------- |
| `group_id`  | number  | -        | Gruppen-ID                                         |
| `is_dismiss`| boolean | `false`  | Gruppe auflösen, wenn das Bot-Konto Besitzer ist  |

##### Antwort

Keine.

#### `set_group_special_title` Spezialtitel setzen

##### Parameter

| Feld           | Typ    | Standard | Beschreibung                                                      |
| -------------- | ------ | -------- | ----------------------------------------------------------------- |
| `group_id`     | number | -        | Gruppen-ID                                                         |
| `user_id`      | number | -        | QQ-Nummer des Mitglieds                                            |
| `special_title`| string | leer     | Spezialtitel; leerer String entfernt den Titel                     |
| `duration`     | number | `-1`     | Dauer in Sekunden; `-1` bedeutet dauerhaft (Verhalten kann variieren) |

##### Antwort

Keine.

#### `set_discuss_leave` Diskussion verlassen

##### Parameter

| Feld        | Typ   | Standard | Beschreibung                                                     |
| ----------- | ----- | -------- | --------------------------------------------------------------- |
| `discuss_id`| number| -        | Diskussions-ID (falls verborgen, aus Diskussionsevents ableiten) |

##### Antwort

Keine.

### Anfragen bearbeiten

#### `set_friend_add_request` Freundschaftsanfrage bearbeiten

##### Parameter

| Feld     | Typ    | Standard | Beschreibung                                   |
| -------- | ------ | -------- | ---------------------------------------------- |
| `flag`   | string | -        | Flag der Anfrage (aus Event-Payload)           |
| `approve`| boolean| `true`   | Anfrage genehmigen                              |
| `remark` | string | leer     | Kommentar bei Genehmigung                       |

##### Antwort

Keine.

#### `set_group_add_request` Gruppenanfrage/-einladung bearbeiten

##### Parameter

| Feld                  | Typ    | Standard | Beschreibung                                                       |
| --------------------- | ------ | -------- | ------------------------------------------------------------------ |
| `flag`                | string | -        | Flag der Anfrage (aus Event-Payload)                               |
| `sub_type` oder `type`| string | -        | `add` oder `invite` (muss mit dem Event `sub_type` übereinstimmen) |
| `approve`             | boolean| `true`   | Anfrage/Einladung genehmigen                                       |
| `reason`              | string | leer     | Ablehnungsgrund (nur bei Ablehnung)                                |

##### Antwort

Keine.

### Informationen abrufen

#### `get_login_info` Login-Informationen

##### Parameter

Keine.

##### Antwort

| Feld      | Typ            | Beschreibung |
| --------- | -------------- | ------------ |
| `user_id` | number (int64) | QQ-Nummer    |
| `nickname`| string         | QQ-Spitzname |

#### `get_stranger_info` Fremdinformationen

##### Parameter

| Feld      | Typ     | Standard | Beschreibung                               |
| --------- | ------- | -------- | ------------------------------------------ |
| `user_id` | number  | -        | QQ-Nummer                                   |
| `no_cache`| boolean | `false`  | Cache deaktivieren (langsamer, aber aktueller) |

##### Antwort

| Feld      | Typ            | Beschreibung                           |
| --------- | -------------- | -------------------------------------- |
| `user_id` | number (int64) | QQ-Nummer                              |
| `nickname`| string         | Spitzname                               |
| `sex`     | string         | `male`, `female` oder `unknown`         |
| `age`     | number (int32) | Alter                                   |

#### `get_friend_list` Freundesliste

##### Parameter

Keine.

##### Antwort

Antwort ist ein JSON-Array. Jeder Eintrag enthält:

| Feld      | Typ            | Beschreibung |
| --------- | -------------- | ------------ |
| `user_id` | number (int64) | QQ-Nummer    |
| `nickname`| string         | Spitzname    |
| `remark`  | string         | Bemerkung    |

#### `get_group_list` Gruppenliste

##### Parameter

Keine.

##### Antwort

Antwort ist ein JSON-Array. Jeder Eintrag enthält:

| Feld        | Typ            | Beschreibung |
| ----------- | -------------- | ------------ |
| `group_id`  | number (int64) | Gruppen-ID   |
| `group_name`| string         | Gruppenname  |

#### `get_group_info` Gruppeninformationen

##### Parameter

| Feld      | Typ     | Standard | Beschreibung                               |
| --------- | ------- | -------- | ------------------------------------------ |
| `group_id`| number  | -        | Gruppen-ID                                  |
| `no_cache`| boolean | `false`  | Cache deaktivieren (langsamer, aber aktueller) |

##### Antwort

| Feld              | Typ            | Beschreibung          |
| ----------------- | -------------- | --------------------- |
| `group_id`        | number (int64) | Gruppen-ID             |
| `group_name`      | string         | Gruppenname            |
| `member_count`    | number (int32) | Mitgliederanzahl       |
| `max_member_count`| number (int32) | Maximale Mitgliederzahl |

#### `get_group_member_info` Gruppenmitglied-Informationen

##### Parameter

| Feld      | Typ     | Standard | Beschreibung                               |
| --------- | ------- | -------- | ------------------------------------------ |
| `group_id`| number  | -        | Gruppen-ID                                  |
| `user_id` | number  | -        | QQ-Nummer                                   |
| `no_cache`| boolean | `false`  | Cache deaktivieren (langsamer, aber aktueller) |

##### Antwort

| Feld               | Typ            | Beschreibung                                  |
| ------------------ | -------------- | --------------------------------------------- |
| `group_id`         | number (int64) | Gruppen-ID                                     |
| `user_id`          | number (int64) | QQ-Nummer                                      |
| `nickname`         | string         | Spitzname                                      |
| `card`             | string         | Gruppenkarte/Bemerkung                         |
| `sex`              | string         | `male`, `female` oder `unknown`                |
| `age`              | number (int32) | Alter                                          |
| `area`             | string         | Region                                         |
| `join_time`        | number (int32) | Beitrittszeitstempel                            |
| `last_sent_time`   | number (int32) | Zeitpunkt der letzten Nachricht                 |
| `level`            | string         | Mitgliedslevel                                  |
| `role`             | string         | `owner`, `admin` oder `member`                  |
| `unfriendly`       | boolean        | Ob das Mitglied als auffällig markiert ist     |
| `title`            | string         | Spezialtitel                                    |
| `title_expire_time`| number (int32) | Ablaufzeitstempel des Spezialtitels             |
| `card_changeable`  | boolean        | Ob die Karte geändert werden darf               |

#### `get_group_member_list` Gruppenmitgliederliste

##### Parameter

| Feld      | Typ   | Standard | Beschreibung |
| --------- | ----- | -------- | ------------ |
| `group_id`| number| -        | Gruppen-ID    |

##### Antwort

Antwort ist ein JSON-Array. Jeder Eintrag enthält die Felder von `get_group_member_info`, jedoch können einige Felder (z. B. `area`, `title`) fehlen. Verwende für vollständige Details die Einzelabfrage.

#### `get_cookies` Cookies abrufen

##### Parameter

| Feld    | Typ   | Standard | Beschreibung             |
| ------- | ----- | -------- | ------------------------ |
| `domain`| string| leer     | Domain für Cookies       |

##### Antwort

| Feld    | Typ   | Beschreibung |
| ------- | ----- | ------------ |
| `cookies`| string | Cookies     |

#### `get_csrf_token` CSRF-Token abrufen

##### Parameter

Keine.

##### Antwort

| Feld  | Typ            | Beschreibung |
| ----- | -------------- | ------------ |
| `token`| number (int32) | CSRF-Token   |

#### `get_credentials` QQ-Anmeldeinformationen

Kombiniert `get_cookies` und `get_csrf_token`.

##### Parameter

Keine.

##### Antwort

| Feld       | Typ            | Beschreibung |
| ---------- | -------------- | ------------ |
| `cookies`  | string         | Cookies      |
| `csrf_token`| number (int32)| CSRF-Token   |

#### `get_record` Sprachnachricht abrufen

Diese API konvertiert Sprachnachrichten in das gewünschte Format und gibt den Dateinamen zurück (unter `data\record`). **Für diese API muss die CoolQ-[Sprachkomponente](https://cqp.cc/t/21132) installiert sein.**

##### Parameter

| Feld        | Typ    | Standard | Beschreibung                                                                 |
| ----------- | ------ | -------- | ---------------------------------------------------------------------------- |
| `file`      | string | -        | Name der Sprachdatei aus dem CQ-Code, z. B. `0B38145AA44505000B38145AA4450500.silk` |
| `out_format`| string | -        | Ausgabeformat: `mp3`, `amr`, `wma`, `m4a`, `spx`, `ogg`, `wav`, `flac`        |
| `full_path` | boolean| `false`  | Absoluten Pfad zurückgeben (empfohlen unter Windows, nicht für Docker)        |

##### Antwort

| Feld | Typ   | Beschreibung                                                                                         |
| ---- | ----- | --------------------------------------------------------------------------------------------------- |
| `file`| string| Konvertierter Dateiname oder Pfad (vollständiger Pfad, wenn `full_path` true ist)                  |

#### `get_image` Bild abrufen

##### Parameter

| Feld | Typ   | Standard | Beschreibung                                                                |
| ---- | ----- | -------- | --------------------------------------------------------------------------- |
| `file`| string| -        | Bilddateiname aus dem CQ-Code, z. B. `6B4DE3DFD1BD271E3297859D41C530F5.jpg`  |

##### Antwort

| Feld | Typ   | Beschreibung                                                                                  |
| ---- | ----- | --------------------------------------------------------------------------------------------- |
| `file`| string| Pfad zur heruntergeladenen Datei, z. B. `C:\Apps\CoolQ\data\image\...`                   |

### Selbstprüfung

#### `can_send_image` Bildversand prüfen

##### Parameter

Keine.

##### Antwort

| Feld | Typ    | Beschreibung |
| ---- | ------ | ------------ |
| `yes`| boolean| Ja oder nein |

#### `can_send_record` Sprachversand prüfen

##### Parameter

Keine.

##### Antwort

| Feld | Typ    | Beschreibung |
| ---- | ------ | ------------ |
| `yes`| boolean| Ja oder nein |

#### `get_status` Plugin-Status abrufen

##### Parameter

Keine.

##### Antwort

| Feld             | Typ     | Beschreibung                                                     |
| ---------------- | ------- | ---------------------------------------------------------------- |
| `app_initialized`| boolean | HTTP-API-Plugin initialisiert                                   |
| `app_enabled`    | boolean | HTTP-API-Plugin aktiviert                                       |
| `plugins_good`   | object  | Interne Plugins laufen ordnungsgemäß                            |
| `app_good`       | boolean | Plugin läuft ordnungsgemäß (initialisiert, aktiviert, Plugins OK) |
| `online`         | boolean | QQ-Online-Status (`null` wenn unbekannt)                        |
| `good`           | boolean | Plugin-Status entspricht Erwartungen                            |

In der Regel reichen `online` und `good` zur Zustandsprüfung aus.

Der `online`-Status kann über `online_status_detection_method` konfiguriert werden:

| Methode                       | Vorteile                                                             | Nachteile                                                         |
| ----------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------ |
| `get_stranger_info` (Standard)| Meist genauer als `log_db`; benötigt Netzwerkaufrufe                 | Kann bei zu hoher Frequenz ungenau sein                            |
| `log_db`                      | Schnell; keine Netzwerkaufrufe (vermeidet Tencent-Risikokontrolle)   | Kann bei CoolQ-Änderungen brechen; Monatswechsel-Probleme          |

#### `get_version_info` Versionsinformationen abrufen

##### Parameter

Keine.

##### Antwort

| Feld                        | Typ    | Beschreibung                                  |
| --------------------------- | ------ | -------------------------------------------- |
| `coolq_directory`           | string | CoolQ-Stammverzeichnis                        |
| `coolq_edition`             | string | CoolQ-Edition, `air` oder `pro`               |
| `plugin_version`            | string | HTTP-API-Plugin-Version (z. B. `2.1.3`)       |
| `plugin_build_number`       | number | Build-Nummer des Plugins                      |
| `plugin_build_configuration`| string | Build-Konfiguration, `debug` oder `release`   |

#### `set_restart_plugin` HTTP-API-Plugin neu starten

Beim Neustart wird auch der API-Dienst neu gestartet, wodurch laufende API-Anfragen unterbrochen werden. Die Antwort hat `status` = `async`.

##### Parameter

| Feld  | Typ    | Standard | Beschreibung                                                    |
| ----- | ------ | -------- | --------------------------------------------------------------- |
| `delay`| number| `0`      | Verzögerung in Millisekunden; ggf. 2000 versuchen               |

##### Antwort

Keine.

#### `clean_data_dir` Datenverzeichnis bereinigen

Bereinigt angesammelte Dateien in `image`, `record`, `show` oder `bface`.

##### Parameter

| Feld     | Typ   | Standard | Beschreibung                             |
| -------- | ----- | -------- | ---------------------------------------- |
| `data_dir`| string| -       | Verzeichnisname: `image`, `record`, `show`, `bface` |

##### Antwort

Keine.

#### `clean_plugin_log` Plugin-Logs löschen

Leert die Logdateien des Plugins.

##### Parameter

Keine.

##### Antwort

Keine.
