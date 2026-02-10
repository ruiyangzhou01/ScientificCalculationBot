# Interaction de chat et gestion des groupes

[TOC]

[English](Interaction.md) | [简体中文](Interaction_zh-CN.md) | [Deutsch](Interaction_de.md) | [Español](Interaction_es.md) | [Français](Interaction_fr.md)

## Présentation

Ce document résume les API d'interaction et de gestion de groupes utilisées par le bot. Les endpoints proviennent du plugin CoolQ HTTP API. Pour la référence complète, consultez la documentation du plugin.

## API

### Interaction de base

#### `send_private_msg` envoyer un message privé

##### Paramètres

| Champ         | Type    | Valeur par défaut | Description                                                                 |
| ------------- | ------- | ----------------- | --------------------------------------------------------------------------- |
| `user_id`     | number  | -                 | Numéro QQ cible                                                             |
| `message`     | message | -                 | Contenu du message                                                          |
| `auto_escape` | boolean | `false`           | Envoyer en texte brut (ne pas analyser les codes CQ) ; valide si `message` est une chaîne |

##### Réponse

| Champ        | Type           | Description  |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | ID du message |

#### `send_group_msg` envoyer un message de groupe

##### Paramètres

| Champ         | Type    | Valeur par défaut | Description                                                                 |
| ------------- | ------- | ----------------- | --------------------------------------------------------------------------- |
| `group_id`    | number  | -                 | ID du groupe                                                                |
| `message`     | message | -                 | Contenu du message                                                          |
| `auto_escape` | boolean | `false`           | Envoyer en texte brut (ne pas analyser les codes CQ) ; valide si `message` est une chaîne |

##### Réponse

| Champ        | Type           | Description  |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | ID du message |

#### `send_discuss_msg` envoyer un message dans une discussion

##### Paramètres

| Champ         | Type    | Valeur par défaut | Description                                                                 |
| ------------- | ------- | ----------------- | --------------------------------------------------------------------------- |
| `discuss_id`  | number  | -                 | ID de discussion (souvent invisible ; obtenu via les événements)            |
| `message`     | message | -                 | Contenu du message                                                          |
| `auto_escape` | boolean | `false`           | Envoyer en texte brut (ne pas analyser les codes CQ) ; valide si `message` est une chaîne |

##### Réponse

| Champ        | Type           | Description  |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | ID du message |

#### `send_msg` envoyer un message

##### Paramètres

| Champ          | Type    | Valeur par défaut | Description                                                                 |
| -------------- | ------- | ----------------- | --------------------------------------------------------------------------- |
| `message_type` | string  | -                 | Type de message : `private`, `group`, `discuss`. S'il est omis, il est déduit de `*_id` |
| `user_id`      | number  | -                 | Numéro QQ cible (requis si `message_type` vaut `private`)                   |
| `group_id`     | number  | -                 | ID du groupe (requis si `message_type` vaut `group`)                        |
| `discuss_id`   | number  | -                 | ID de discussion (requis si `message_type` vaut `discuss`)                  |
| `message`      | message | -                 | Contenu du message                                                          |
| `auto_escape`  | boolean | `false`           | Envoyer en texte brut (ne pas analyser les codes CQ) ; valide si `message` est une chaîne |

##### Réponse

| Champ        | Type           | Description  |
| ----------- | -------------- | ------------ |
| `message_id`| number (int32) | ID du message |

#### `delete_msg` rappeler un message

##### Paramètres

| Champ        | Type           | Valeur par défaut | Description |
| ----------- | -------------- | ----------------- | ----------- |
| `message_id`| number (int32) | -                 | ID du message |

##### Réponse

Aucune.

#### `send_like` envoyer un like

##### Paramètres

| Champ     | Type   | Valeur par défaut | Description                                |
| --------- | ------ | ----------------- | ------------------------------------------ |
| `user_id` | number | -                 | Numéro QQ cible                             |
| `times`   | number | 1                 | Nombre de likes (max 10 par ami et par jour) |

##### Réponse

Aucune.

### Gestion de groupe

#### `set_group_kick` expulser un membre

##### Paramètres

| Champ                 | Type    | Valeur par défaut | Description                     |
| --------------------- | ------- | ----------------- | ------------------------------- |
| `group_id`            | number  | -                 | ID du groupe                    |
| `user_id`             | number  | -                 | Numéro QQ à expulser            |
| `reject_add_request`  | boolean | `false`           | Rejeter les futures demandes    |

##### Réponse

Aucune.

#### `set_group_ban` mettre un membre en sourdine

##### Paramètres

| Champ      | Type    | Valeur par défaut | Description                               |
| ---------- | ------- | ----------------- | ----------------------------------------- |
| `group_id` | number  | -                 | ID du groupe                              |
| `user_id`  | number  | -                 | Numéro QQ à mettre en sourdine            |
| `duration` | number  | `30 * 60`         | Durée en secondes ; 0 annule la sourdine |

##### Réponse

Aucune.

#### `set_group_anonymous_ban` sourdine anonyme

##### Paramètres

| Champ                     | Type    | Valeur par défaut | Description                                                             |
| ------------------------- | ------- | ----------------- | ----------------------------------------------------------------------- |
| `group_id`                | number  | -                 | ID du groupe                                                            |
| `anonymous`               | object  | -                 | Objet utilisateur anonyme (depuis les événements)                       |
| `anonymous_flag` ou `flag`| string  | -                 | Flag utilisateur anonyme (depuis les événements)                        |
| `duration`                | number  | `30 * 60`         | Durée en secondes ; la sourdine anonyme ne peut pas être annulée         |

Indiquez `anonymous` ou `anonymous_flag`. Si les deux sont fournis, `anonymous` est utilisé.

##### Réponse

Aucune.

#### `set_group_whole_ban` sourdine globale

##### Paramètres

| Champ      | Type    | Valeur par défaut | Description |
| ---------- | ------- | ----------------- | ----------- |
| `group_id` | number  | -                 | ID du groupe |
| `enable`   | boolean | `true`            | Activer la sourdine |

##### Réponse

Aucune.

#### `set_group_admin` définir un administrateur

##### Paramètres

| Champ      | Type    | Valeur par défaut | Description                              |
| ---------- | ------- | ----------------- | ---------------------------------------- |
| `group_id` | number  | -                 | ID du groupe                             |
| `user_id`  | number  | -                 | Numéro QQ à promouvoir                   |
| `enable`   | boolean | `true`            | `true` pour définir, `false` pour retirer |

##### Réponse

Aucune.

#### `set_group_anonymous` activer le mode anonyme

##### Paramètres

| Champ      | Type    | Valeur par défaut | Description                 |
| ---------- | ------- | ----------------- | --------------------------- |
| `group_id` | number  | -                 | ID du groupe                |
| `enable`   | boolean | `true`            | Autoriser le chat anonyme   |

##### Réponse

Aucune.

#### `set_group_card` définir la carte de groupe

##### Paramètres

| Champ      | Type   | Valeur par défaut | Description                                       |
| ---------- | ------ | ----------------- | ------------------------------------------------- |
| `group_id` | number | -                 | ID du groupe                                      |
| `user_id`  | number | -                 | Numéro QQ à mettre à jour                         |
| `card`     | string | vide              | Contenu de la carte ; vide supprime la carte      |

##### Réponse

Aucune.

#### `set_group_leave` quitter un groupe

##### Paramètres

| Champ       | Type    | Valeur par défaut | Description                                      |
| ----------- | ------- | ----------------- | ------------------------------------------------ |
| `group_id`  | number  | -                 | ID du groupe                                     |
| `is_dismiss`| boolean | `false`           | Dissoudre le groupe si le bot en est propriétaire |

##### Réponse

Aucune.

#### `set_group_special_title` définir un titre spécial

##### Paramètres

| Champ           | Type   | Valeur par défaut | Description                                                   |
| --------------- | ------ | ----------------- | ------------------------------------------------------------- |
| `group_id`      | number | -                 | ID du groupe                                                  |
| `user_id`       | number | -                 | Numéro QQ à mettre à jour                                     |
| `special_title` | string | vide              | Titre spécial ; vide le supprime                              |
| `duration`      | number | `-1`              | Durée en secondes ; `-1` signifie permanent (peut varier)      |

##### Réponse

Aucune.

#### `set_discuss_leave` quitter une discussion

##### Paramètres

| Champ        | Type   | Valeur par défaut | Description                                                          |
| ------------ | ------ | ----------------- | -------------------------------------------------------------------- |
| `discuss_id` | number | -                 | ID de discussion (à récupérer depuis les événements si masqué)       |

##### Réponse

Aucune.

### Traiter les demandes

#### `set_friend_add_request` traiter une demande d'ami

##### Paramètres

| Champ     | Type    | Valeur par défaut | Description                                  |
| --------- | ------- | ----------------- | -------------------------------------------- |
| `flag`    | string  | -                 | Flag de la demande (depuis l'événement)      |
| `approve` | boolean | `true`            | Approuver la demande                          |
| `remark`  | string  | vide              | Remarque à définir lors de l'approbation     |

##### Réponse

Aucune.

#### `set_group_add_request` traiter une demande/invitation de groupe

##### Paramètres

| Champ                  | Type    | Valeur par défaut | Description                                                         |
| ---------------------- | ------- | ----------------- | ------------------------------------------------------------------- |
| `flag`                 | string  | -                 | Flag de la demande (depuis l'événement)                             |
| `sub_type` ou `type`   | string  | -                 | `add` ou `invite` (doit correspondre à `sub_type` de l'événement)   |
| `approve`              | boolean | `true`            | Approuver la demande/l'invitation                                   |
| `reason`               | string  | vide              | Motif du refus (uniquement en cas de refus)                         |

##### Réponse

Aucune.

### Obtenir des informations

#### `get_login_info` obtenir les informations de connexion

##### Paramètres

Aucun.

##### Réponse

| Champ      | Type           | Description |
| ---------- | -------------- | ----------- |
| `user_id`  | number (int64) | Numéro QQ   |
| `nickname` | string         | Surnom QQ   |

#### `get_stranger_info` obtenir des informations sur un inconnu

##### Paramètres

| Champ     | Type    | Valeur par défaut | Description                                |
| --------- | ------- | ----------------- | ------------------------------------------ |
| `user_id` | number  | -                 | Numéro QQ                                  |
| `no_cache`| boolean | `false`           | Désactiver le cache (plus lent, plus à jour) |

##### Réponse

| Champ     | Type           | Description                       |
| --------- | -------------- | --------------------------------- |
| `user_id` | number (int64) | Numéro QQ                          |
| `nickname`| string         | Surnom                             |
| `sex`     | string         | `male`, `female` ou `unknown`      |
| `age`     | number (int32) | Âge                                |

#### `get_friend_list` obtenir la liste d'amis

##### Paramètres

Aucun.

##### Réponse

La réponse est un tableau JSON. Chaque élément contient :

| Champ     | Type           | Description |
| --------- | -------------- | ----------- |
| `user_id` | number (int64) | Numéro QQ   |
| `nickname`| string         | Surnom      |
| `remark`  | string         | Remarque    |

#### `get_group_list` obtenir la liste des groupes

##### Paramètres

Aucun.

##### Réponse

La réponse est un tableau JSON. Chaque élément contient :

| Champ       | Type           | Description |
| ---------- | -------------- | ----------- |
| `group_id`  | number (int64) | ID du groupe |
| `group_name`| string         | Nom du groupe |

#### `get_group_info` obtenir les informations du groupe

##### Paramètres

| Champ     | Type    | Valeur par défaut | Description                                |
| --------- | ------- | ----------------- | ------------------------------------------ |
| `group_id`| number  | -                 | ID du groupe                               |
| `no_cache`| boolean | `false`           | Désactiver le cache (plus lent, plus à jour) |

##### Réponse

| Champ              | Type           | Description           |
| ----------------- | -------------- | --------------------- |
| `group_id`         | number (int64) | ID du groupe          |
| `group_name`       | string         | Nom du groupe         |
| `member_count`     | number (int32) | Nombre de membres     |
| `max_member_count` | number (int32) | Capacité maximale     |

#### `get_group_member_info` obtenir les informations d'un membre

##### Paramètres

| Champ     | Type    | Valeur par défaut | Description                                |
| --------- | ------- | ----------------- | ------------------------------------------ |
| `group_id`| number  | -                 | ID du groupe                               |
| `user_id` | number  | -                 | Numéro QQ                                  |
| `no_cache`| boolean | `false`           | Désactiver le cache (plus lent, plus à jour) |

##### Réponse

| Champ               | Type           | Description                               |
| ------------------- | -------------- | ----------------------------------------- |
| `group_id`          | number (int64) | ID du groupe                              |
| `user_id`           | number (int64) | Numéro QQ                                 |
| `nickname`          | string         | Surnom                                    |
| `card`              | string         | Carte/Remarque                            |
| `sex`               | string         | `male`, `female` ou `unknown`             |
| `age`               | number (int32) | Âge                                       |
| `area`              | string         | Région                                    |
| `join_time`         | number (int32) | Horodatage d'entrée                       |
| `last_sent_time`    | number (int32) | Horodatage du dernier message             |
| `level`             | string         | Niveau du membre                          |
| `role`              | string         | `owner`, `admin` ou `member`              |
| `unfriendly`        | boolean        | Indique si le membre est signalé          |
| `title`             | string         | Titre spécial                             |
| `title_expire_time` | number (int32) | Horodatage d'expiration du titre          |
| `card_changeable`   | boolean        | Autorise la modification de la carte      |

#### `get_group_member_list` obtenir la liste des membres

##### Paramètres

| Champ     | Type   | Valeur par défaut | Description |
| --------- | ------ | ----------------- | ----------- |
| `group_id`| number | -                 | ID du groupe |

##### Réponse

La réponse est un tableau JSON. Chaque élément possède les champs de `get_group_member_info`, mais certains champs (par exemple `area`, `title`) peuvent manquer. Utilisez la requête individuelle pour les détails.

#### `get_cookies` obtenir les cookies

##### Paramètres

| Champ   | Type   | Valeur par défaut | Description                  |
| ------- | ------ | ----------------- | ---------------------------- |
| `domain`| string | vide              | Domaine pour les cookies     |

##### Réponse

| Champ    | Type   | Description |
| -------- | ------ | ----------- |
| `cookies`| string | Cookies     |

#### `get_csrf_token` obtenir le jeton CSRF

##### Paramètres

Aucun.

##### Réponse

| Champ  | Type           | Description |
| ------ | -------------- | ----------- |
| `token`| number (int32) | Jeton CSRF  |

#### `get_credentials` obtenir les identifiants QQ

Combine `get_cookies` et `get_csrf_token`.

##### Paramètres

Aucun.

##### Réponse

| Champ       | Type           | Description |
| ----------- | -------------- | ----------- |
| `cookies`   | string         | Cookies     |
| `csrf_token`| number (int32) | Jeton CSRF  |

#### `get_record` obtenir un enregistrement vocal

Convertit le message vocal au format demandé et renvoie le nom de fichier (stocké sous `data\record`). **Pour utiliser cette API, installez le [composant vocal](https://cqp.cc/t/21132) de CoolQ.**

##### Paramètres

| Champ        | Type    | Valeur par défaut | Description                                                                 |
| ------------ | ------- | ----------------- | --------------------------------------------------------------------------- |
| `file`       | string  | -                 | Nom du fichier vocal, ex. `0B38145AA44505000B38145AA4450500.silk`           |
| `out_format` | string  | -                 | Format : `mp3`, `amr`, `wma`, `m4a`, `spx`, `ogg`, `wav`, `flac`            |
| `full_path`  | boolean | `false`           | Renvoyer le chemin absolu (recommandé sous Windows, pas dans Docker)        |

##### Réponse

| Champ | Type   | Description                                                                                           |
| ----- | ------ | ----------------------------------------------------------------------------------------------------- |
| `file`| string | Nom ou chemin du fichier converti (chemin complet si `full_path` est `true`)                         |

#### `get_image` obtenir une image

##### Paramètres

| Champ | Type   | Valeur par défaut | Description                                                             |
| ----- | ------ | ----------------- | ----------------------------------------------------------------------- |
| `file`| string | -                 | Nom du fichier image, ex. `6B4DE3DFD1BD271E3297859D41C530F5.jpg`        |

##### Réponse

| Champ | Type   | Description                                                                                  |
| ----- | ------ | -------------------------------------------------------------------------------------------- |
| `file`| string | Chemin de l'image téléchargée, ex. `C:\Apps\CoolQ\data\image\...`                          |

### Auto-vérification

#### `can_send_image` vérifier l'envoi d'images

##### Paramètres

Aucun.

##### Réponse

| Champ | Type    | Description |
| ----- | ------- | ----------- |
| `yes` | boolean | Oui ou non  |

#### `can_send_record` vérifier l'envoi de messages vocaux

##### Paramètres

Aucun.

##### Réponse

| Champ | Type    | Description |
| ----- | ------- | ----------- |
| `yes` | boolean | Oui ou non  |

#### `get_status` obtenir l'état du plugin

##### Paramètres

Aucun.

##### Réponse

| Champ             | Type    | Description                                                       |
| ----------------- | ------- | ----------------------------------------------------------------- |
| `app_initialized` | boolean | Plugin HTTP API initialisé                                        |
| `app_enabled`     | boolean | Plugin HTTP API activé                                            |
| `plugins_good`    | object  | Les plugins internes fonctionnent correctement                    |
| `app_good`        | boolean | Plugin en bon état (initialisé, activé, plugins OK)               |
| `online`          | boolean | Statut en ligne (`null` si non détectable)                        |
| `good`            | boolean | État attendu du plugin                                            |

En général, `online` et `good` suffisent.

Le statut `online` peut être détecté via `online_status_detection_method` :

| Méthode                         | Avantages                                                     | Inconvénients                                                |
| ------------------------------ | ------------------------------------------------------------- | ------------------------------------------------------------ |
| `get_stranger_info` (par défaut) | Plus précis dans la plupart des cas ; nécessite le réseau  | Peut être inexact si la fréquence est élevée                |
| `log_db`                        | Rapide ; pas de requêtes réseau                              | Peut échouer si CoolQ change la base ; problèmes fin de mois |

#### `get_version_info` obtenir les informations de version

##### Paramètres

Aucun.

##### Réponse

| Champ                        | Type   | Description                                  |
| --------------------------- | ------ | -------------------------------------------- |
| `coolq_directory`           | string | Répertoire racine de CoolQ                   |
| `coolq_edition`             | string | Édition CoolQ, `air` ou `pro`                |
| `plugin_version`            | string | Version du plugin HTTP API (ex. `2.1.3`)     |
| `plugin_build_number`       | number | Numéro de build du plugin                    |
| `plugin_build_configuration`| string | Configuration de build, `debug` ou `release` |

#### `set_restart_plugin` redémarrer le plugin HTTP API

Le redémarrage du plugin redémarre également le service API et interrompt les requêtes en cours. La réponse contient `status` = `async`.

##### Paramètres

| Champ  | Type   | Valeur par défaut | Description                                                |
| ------ | ------ | ----------------- | ---------------------------------------------------------- |
| `delay`| number | `0`               | Délai en millisecondes ; essayez 2000 si nécessaire        |

##### Réponse

Aucune.

#### `clean_data_dir` nettoyer le répertoire de données

Nettoie les fichiers accumulés dans `image`, `record`, `show` ou `bface`.

##### Paramètres

| Champ     | Type   | Valeur par défaut | Description                                         |
| --------- | ------ | ----------------- | --------------------------------------------------- |
| `data_dir`| string | -                 | Nom du répertoire : `image`, `record`, `show`, `bface` |

##### Réponse

Aucune.

#### `clean_plugin_log` nettoyer les journaux du plugin

Efface les fichiers journaux du plugin.

##### Paramètres

Aucun.

##### Réponse

Aucune.
