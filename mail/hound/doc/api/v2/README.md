# hound API  version 2 documentation

```https://{host}/v2```

* **host**: *(required)  string*
  default: localhost

## Identifiers schemas

Here are identifiers used in the API and it's entities
* [Revision](common/schemas/revision.schema.json) - user mailbox revision.
* [Mid](common/schemas/mid.schema.json) - message mailbox unique identifier.
* [Fid](common/schemas/fid.schema.json) - folder mailbox unique identifier.
* [Lid](common/schemas/lid.schema.json) - label mailbox unique identifier.
* [Tid](common/schemas/tid.schema.json) - messages' thread unique identifier.
* [Hid](common/schemas/hid.schema.json) - messages' attachment unique identifier.
* [Tab Type](common/schemas/tab-type.schema.json) - tab mailbox unique identifier.
* [Archive State](common/schemas/archive_state.schema.json) - user's archivation state identifier.
* [User State](common/schemas/user_state.schema.json) - user's current state identifier.

## Identifier array schemas

There are identifier arrays used in the API
* [mids](common/schemas/mids.schema.json) - message unique identifier array.

## Entities schemas

These entities are used within this API
* [Envelope](changes/schemas/envelope.schema.json) - message metadata representation
* [Folder](folders/schemas/folder.schema.json) - folder representation
* [Folder with subfolders](folders_tree/schemas/folder_with_subfolders.schema.json) - folders_tree's folder representation
* [Label](changes/schemas/label.schema.json) - label representation
* [Tab](tabs/schemas/tab.schema.json) - tab representation

## Changes

Please refer to [change.schema.json](changes/schemas/change.schema.json) to learn about how to recognize changes. These next changes are available:
* [store](changes/schemas/store.schema.json) - messages have been stored,
* [update](changes/schemas/update.schema.json) - messages labels have been updated,
* [delete](changes/schemas/delete.schema.json) - messages have been deleted,
* [copy](changes/schemas/copy.schema.json) - messages have been copied with IMAP,
* [move](changes/schemas/move.schema.json) - messages have been moved between folders,
* [quick-save](changes/schemas/quick-save.schema.json) - messages' drafts have been saved,
* [threads-join](changes/schemas/threads-join.schema.json) - messages' threads have been joined,
* [label-create](changes/schemas/label-create.schema.json) - labels have been created,
* [label-delete](changes/schemas/label-delete.schema.json) - labels have been deleted,
* [label-modify](changes/schemas/label-modify.schema.json) - labels have been modified,
* [folder-create](changes/schemas/folder-create.schema.json) - folders have been created,
* [folder-delete](changes/schemas/folder-delete.schema.json) - folders have been deleted,
* [folder-modify](changes/schemas/folder-modify.schema.json) - folders have been modified,
* [fresh-reset](changes/schemas/fresh-reset.schema.json) - fresh counter has been reseted,
* [folder-reset-unvisited](changes/schemas/folder-reset-unvisited.schema.json) - folder's unvisited flag has been reseted,
* [tab-create](changes/schemas/tab-create.schema.json) - tabs have been created,
* [move-to-tab](changes/schemas/move-to-tab.schema.json) - messages have been moved between tabs.

---

## /attach_sid

### GET /attach_sid

Get secure id of attachment(s).

```GET https://{host}/v2/attach_sid```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **uid**: *(required)  integer*

  user's id

* **mid**: *(required)  json*

  message's id

* **hids**: *(required)  array of hid*

  attachment ids

#### HTTP status code [200](https://httpstatuses.com/200)

Per attachment secured id.

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
  "$id": "attach_sid.schema.json",
  "title": "attach_sid",
  "description": "Secured identifiers of attachments",
  "type": "object",
  "properties": {
    "/^\\d+\\.\\d+$/": {
      "description": "Per attachment secured id. Key is hid, value is sid",
      "type": "string"
    },
    "all": {
      "description": "Secured id for all attachments. Will be returned in case when more than 1 attachment",
      "type": "string",
      "required": false
    }
  },
  "additionalProperties": false
}

```

**Example**

```json

{
  "1.1": "YWVzX3NpZDp7ImFlc0tleUlkIjoiMTc4IiwiaG1hY0tleUlkIjoiMTc4IiwiaXZCYXNlNjQiOiJncWYwejUrVnFvOGdKcVI4d2VENjNnPT0iLCJzaWRCYXNlNjQiOiJYS3RuNGRtQkhtWkkwWGtrK3NFV3VKdWZNWHRJc1ZuRmNaYmhYSGM3UE8wNGZHUEtaU2xYWjVQbENLaGxUNHVZbmR5K0g0Y0VsaUh4MHBsTXhjUlZiUW5ycEZ4dTdMRmpCekZzQkVEd2ltaz0iLCJobWFjQmFzZTY0IjoiZHNXZzlVVk1KL0YvaUVmM1RiTHJDdXNpUzU4TEpYY3V2QitzNnJWNlRLUT0ifQ%3D%3D",
  "all": "YWVzX3NpZDp7ImFlc0tleUlkIjoiMTc4IiwiaG1hY0tleUlkIjoiMTc4IiwiaXZCYXNlNjQiOiJncWYwejUrVnFvOGdKcVI4d2VENjNnPT0iLCJzaWRCYXNlNjQiOiJUWVVPUWE2dWkyZmxyVjBuZ1c0bmxEaDZlL2hLTFRadUJ6Vk9Ba0ZNSmZ3NVJ3eG8yZFFWY2ZpZGNiMGpkN0hZUGh4bXVoMVJnMEJsNVBtemV1UGxzRWdvTGxTemxxMGhxMENsd0ZyMWNiRT0iLCJobWFjQmFzZTY0Ijoibzg5cDZyU3N3aFM0M0ViNStKS2lDWWRid1FkZ09qSDhxdUxSSDJpdGdqQT0ifQ%3D%3D",
  "1.2": "YWVzX3NpZDp7ImFlc0tleUlkIjoiMTc4IiwiaG1hY0tleUlkIjoiMTc4IiwiaXZCYXNlNjQiOiJncWYwejUrVnFvOGdKcVI4d2VENjNnPT0iLCJzaWRCYXNlNjQiOiJYS3RuNGRtQkhtWkkwWGtrK3NFV3VKdWZNWHRJc1ZuRmNaYmhYSGM3UE8wNGZHUEtaU2xYWjVQbENLaGxUNHVZbmR5K0g0Y0VsaUh4MHBsTXhjUlZiU0lVZVAzczZJRldiKzNSV3RsOThPTT0iLCJobWFjQmFzZTY0IjoiQ3pqVEwxV3V5KzVhQ0ZpdHVtZnlCeHZWVEM2aVFBVm1Yc1lWVExFU0tpND0ifQ%3D%3D"
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /changes

### GET /changes

Get user changes from specified revision to current revision.

```GET https://{host}/v2/changes```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **revision**: *(required)  integer*

  Start revision for changes to select, in case of the revision can not be found error will be returned

* **max_count**: *(required)  integer*

  Maximum number of changes allowed to return, if it exceeded then the error will be returned

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

Revision found in users change log and data delta events will be returned in the response body. Please refer to Changes documentation to learn more.

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "changes.schema.json",
    "title": "Changes",
    "description": "List of changes sorted by revision",
    "type":"object",
    "properties": {
        "changes" : {"type": "array","items": { "$ref": "change.schema.json"}}
    },
    "required": ["changes"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "changes": [
        {
            "revision": 861,
            "type": "store",
            "value": [
                {
                    "attachments": [],
                    "attachmentsCount": 0,
                    "attachmentsFullSize": 0,
                    "bcc": [],
                    "cc": [],
                    "date": 1533560112,
                    "fid": "1",
                    "tab": "relevant",
                    "firstline": "asdfasdf asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdf",
                    "from": [
                        {
                            "displayName": "Abdul Akhmed",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "imapId": "164",
                    "inReplyTo": "",
                    "labels": [
                        "103",
                        "24",
                        "FAKE_MULCA_SHARED_LBL",
                        "FAKE_RECENT_LBL"
                    ],
                    "mid": "166351711235998026",
                    "newCount": 0,
                    "receiveDate": 1533560112,
                    "references": "",
                    "replyTo": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "revision": 861,
                    "rfcId": "&lt;1281533560112@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                    "size": 1826,
                    "stid": "320.mail:0.E3960:3118342638140744549041442953089",
                    "subject": "asdf",
                    "subjectInfo": {
                        "isSplitted": true,
                        "postfix": "",
                        "prefix": "",
                        "subject": "asdf",
                        "type": ""
                    },
                    "threadCount": 0,
                    "threadId": "164944336352444719",
                    "to": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "types": [
                        4,
                        55
                    ],
                    "uidl": ""
                }
            ]
        },
        {
            "revision": 866,
            "type": "delete",
            "value": [
                "166351711235998027"
            ]
        },
        {
            "revision": 867,
            "type": "store",
            "value": [
                {
                    "attachments": [],
                    "attachmentsCount": 0,
                    "attachmentsFullSize": 0,
                    "bcc": [],
                    "cc": [],
                    "date": 1533560269,
                    "fid": "4",
                    "tab": "",
                    "firstline": "asdfasdfsdf asdf",
                    "from": [
                        {
                            "displayName": "Abdul Akhmed",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "imapId": "64",
                    "inReplyTo": "",
                    "labels": [
                        "103",
                        "24",
                        "FAKE_MULCA_SHARED_LBL",
                        "FAKE_RECENT_LBL",
                        "FAKE_SEEN_LBL"
                    ],
                    "mid": "166351711235998028",
                    "newCount": 0,
                    "receiveDate": 1533560269,
                    "references": "",
                    "replyTo": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "revision": 867,
                    "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                    "size": 3175,
                    "stid": "320.mail:0.E4192:3118342638107170542233819674492",
                    "subject": "No subject",
                    "subjectInfo": {
                        "isSplitted": true,
                        "postfix": "",
                        "prefix": "",
                        "subject": "No subject",
                        "type": ""
                    },
                    "threadCount": 0,
                    "threadId": "166351711235998028",
                    "to": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "types": [
                        4,
                        55
                    ],
                    "uidl": ""
                }
            ]
        },
        {
            "revision": 868,
            "type": "store",
            "value": [
                {
                    "attachments": [],
                    "attachmentsCount": 0,
                    "attachmentsFullSize": 0,
                    "bcc": [],
                    "cc": [],
                    "date": 1533560269,
                    "fid": "1",
                    "tab": "news",
                    "firstline": "asdfasdfsdf asdf",
                    "from": [
                        {
                            "displayName": "Abdul Akhmed",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "imapId": "165",
                    "inReplyTo": "",
                    "labels": [
                        "103",
                        "24",
                        "FAKE_MULCA_SHARED_LBL",
                        "FAKE_RECENT_LBL",
                        "FAKE_SEEN_LBL"
                    ],
                    "mid": "166351711235998029",
                    "newCount": 0,
                    "receiveDate": 1533560269,
                    "references": "",
                    "replyTo": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "revision": 871,
                    "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                    "size": 3175,
                    "stid": "320.mail:0.E4192:3118342638107170542233819674492",
                    "subject": "No subject",
                    "subjectInfo": {
                        "isSplitted": true,
                        "postfix": "",
                        "prefix": "",
                        "subject": "No subject",
                        "type": ""
                    },
                    "threadCount": 0,
                    "threadId": "166351711235998028",
                    "to": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "types": [
                        4,
                        55
                    ],
                    "uidl": ""
                }
            ]
        },
        {
            "revision": 871,
            "type": "update",
            "value": [
                {
                    "labels": [
                        "FAKE_SEEN_LBL",
                        "FAKE_RECENT_LBL",
                        "24",
                        "103"
                    ],
                    "mid": "166351711235998029"
                }
            ]
        }
    ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /folders

### POST /folders

```POST https://{host}/v2/folders```

### GET /folders

Get list of user folders

```GET https://{host}/v2/folders```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **with_hidden**: *string*

  Returns all folders together with hidden ones, if the parameter is given.

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "folders.schema.json",
    "title": "Folders",
    "description": "Sequence of user folders",
    "type":"object",
    "properties": {
        "folders" : {"type": "array","items": { "$ref": "folder.schema.json"}}
    },
    "required": ["folders"],
    "additionalProperties": false
}

```

**Example**

```json

{
   "folders" : [
      {
         "id" : "1",
         "unreadMessagesCount" : 88,
         "isUnvisited" : false,
         "isThreadable" : true,
         "messagesCount" : 141,
         "name" : "Inbox",
         "recentMessagesCount" : 141,
         "createDate" : "2017-08-29T19:05:56+0300",
         "symbol" : "inbox",
         "revision" : 342,
         "bytes" : 659727,
         "type" : "system",
         "subscribedForSharedFolder" : false,
         "parentId" : "0"
      },
      {
         "bytes" : 0,
         "revision" : 382,
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "parentId" : "0",
         "id" : "45",
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "messagesCount" : 0,
         "name" : "AA",
         "createDate" : "2018-09-17T21:06:37+0300",
         "recentMessagesCount" : 0,
         "symbol" : ""
      },
      {
         "parentId" : "0",
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "revision" : 317,
         "bytes" : 0,
         "createDate" : "2018-08-20T15:35:40+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "name" : "english",
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true,
         "messagesCount" : 0,
         "id" : "13"
      },
      {
         "id" : "14",
         "messagesCount" : 0,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "name" : "algo",
         "symbol" : "",
         "createDate" : "2018-08-20T15:36:09+0300",
         "recentMessagesCount" : 0,
         "revision" : 318,
         "bytes" : 0,
         "subscribedForSharedFolder" : false,
         "type" : "user",
         "parentId" : "13"
      },
      {
         "messagesCount" : 0,
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true,
         "id" : "16",
         "symbol" : "",
         "recentMessagesCount" : 0,
         "createDate" : "2018-08-20T15:36:36+0300",
         "name" : "qwerty",
         "revision" : 321,
         "bytes" : 0,
         "parentId" : "13",
         "subscribedForSharedFolder" : false,
         "type" : "user"
      },
      {
         "parentId" : "13",
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "bytes" : 0,
         "revision" : 320,
         "createDate" : "2018-08-20T15:36:21+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "name" : "web",
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true,
         "messagesCount" : 0,
         "id" : "15"
      },
      {
         "symbol" : "",
         "recentMessagesCount" : 0,
         "createDate" : "2018-09-17T21:06:50+0300",
         "name" : "hh",
         "messagesCount" : 0,
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true,
         "id" : "47",
         "parentId" : "0",
         "subscribedForSharedFolder" : false,
         "type" : "user",
         "revision" : 384,
         "bytes" : 0
      },
      {
         "bytes" : 0,
         "revision" : 312,
         "parentId" : "0",
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true,
         "messagesCount" : 0,
         "id" : "8",
         "recentMessagesCount" : 0,
         "createDate" : "2018-08-20T15:34:01+0300",
         "symbol" : "",
         "name" : "russian"
      },
      {
         "isUnvisited" : false,
         "isThreadable" : true,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "id" : "37",
         "recentMessagesCount" : 0,
         "createDate" : "2018-09-12T15:58:13+0300",
         "symbol" : "",
         "name" : "аа",
         "bytes" : 0,
         "revision" : 374,
         "parentId" : "8",
         "type" : "user",
         "subscribedForSharedFolder" : false
      },
      {
         "parentId" : "8",
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "revision" : 376,
         "bytes" : 0,
         "recentMessagesCount" : 0,
         "createDate" : "2018-09-12T15:58:24+0300",
         "symbol" : "",
         "name" : "бб",
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "messagesCount" : 0,
         "id" : "39"
      },
      {
         "bytes" : 0,
         "revision" : 377,
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "parentId" : "8",
         "id" : "40",
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "messagesCount" : 0,
         "name" : "ёё",
         "createDate" : "2018-09-12T15:58:33+0300",
         "recentMessagesCount" : 0,
         "symbol" : ""
      },
      {
         "name" : "яя",
         "recentMessagesCount" : 0,
         "createDate" : "2018-09-12T15:58:21+0300",
         "symbol" : "",
         "id" : "38",
         "isUnvisited" : false,
         "isThreadable" : true,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "parentId" : "8",
         "bytes" : 0,
         "revision" : 375
      },
      {
         "revision" : 378,
         "bytes" : 0,
         "parentId" : "0",
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "isUnvisited" : false,
         "isThreadable" : true,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "id" : "41",
         "recentMessagesCount" : 0,
         "createDate" : "2018-09-17T20:43:14+0300",
         "symbol" : "",
         "name" : "test"
      },
      {
         "parentId" : "41",
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "revision" : 379,
         "bytes" : 0,
         "createDate" : "2018-09-17T20:43:21+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "name" : "аа",
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "messagesCount" : 0,
         "id" : "42"
      },
      {
         "id" : "44",
         "messagesCount" : 0,
         "isThreadable" : true,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "name" : "бб",
         "symbol" : "",
         "createDate" : "2018-09-17T20:43:29+0300",
         "recentMessagesCount" : 0,
         "revision" : 381,
         "bytes" : 0,
         "subscribedForSharedFolder" : false,
         "type" : "user",
         "parentId" : "41"
      },
      {
         "id" : "43",
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true,
         "messagesCount" : 0,
         "name" : "яя",
         "createDate" : "2018-09-17T20:43:25+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "bytes" : 0,
         "revision" : 380,
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "parentId" : "41"
      },
      {
         "createDate" : "2018-08-20T15:37:17+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "name" : "Türk",
         "isThreadable" : true,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "id" : "17",
         "parentId" : "0",
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "bytes" : 0,
         "revision" : 322
      },
      {
         "revision" : 323,
         "bytes" : 0,
         "parentId" : "17",
         "subscribedForSharedFolder" : false,
         "type" : "user",
         "messagesCount" : 0,
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true,
         "id" : "18",
         "symbol" : "",
         "createDate" : "2018-08-20T15:38:14+0300",
         "recentMessagesCount" : 0,
         "name" : "Arnavutluk"
      },
      {
         "name" : "geyik",
         "createDate" : "2018-08-20T15:39:34+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "id" : "20",
         "isThreadable" : true,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "parentId" : "17",
         "revision" : 325,
         "bytes" : 0
      },
      {
         "isThreadable" : true,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "id" : "46",
         "createDate" : "2018-09-17T21:06:43+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "name" : "ZZ",
         "revision" : 383,
         "bytes" : 0,
         "parentId" : "0",
         "type" : "user",
         "subscribedForSharedFolder" : false
      },
      {
         "id" : "21",
         "isThreadable" : true,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "name" : "український",
         "createDate" : "2018-08-20T15:40:07+0300",
         "recentMessagesCount" : 0,
         "symbol" : "",
         "bytes" : 0,
         "revision" : 326,
         "type" : "user",
         "subscribedForSharedFolder" : false,
         "parentId" : "0"
      },
      {
         "parentId" : "21",
         "subscribedForSharedFolder" : false,
         "type" : "user",
         "bytes" : 0,
         "revision" : 327,
         "symbol" : "",
         "createDate" : "2018-08-20T15:40:19+0300",
         "recentMessagesCount" : 0,
         "name" : "Абетка",
         "messagesCount" : 0,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "id" : "22"
      },
      {
         "id" : "23",
         "messagesCount" : 0,
         "isThreadable" : true,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "name" : "яблуко",
         "symbol" : "",
         "createDate" : "2018-08-20T15:40:29+0300",
         "recentMessagesCount" : 0,
         "bytes" : 0,
         "revision" : 328,
         "subscribedForSharedFolder" : false,
         "type" : "user",
         "parentId" : "21"
      },
      {
         "name" : "არქივი",
         "recentMessagesCount" : 0,
         "createDate" : "2018-02-15T15:38:36+0300",
         "symbol" : "archive",
         "id" : "7",
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "messagesCount" : 0,
         "type" : "system",
         "subscribedForSharedFolder" : false,
         "parentId" : "0",
         "revision" : 32,
         "bytes" : 0
      },
      {
         "parentId" : "0",
         "type" : "system",
         "subscribedForSharedFolder" : false,
         "bytes" : 622763,
         "revision" : 332,
         "createDate" : "2017-08-29T19:05:56+0300",
         "recentMessagesCount" : 95,
         "symbol" : "sent",
         "name" : "Sent",
         "isThreadable" : true,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "messagesCount" : 95,
         "id" : "4"
      },
      {
         "recentMessagesCount" : 0,
         "createDate" : "2017-08-29T19:05:56+0300",
         "symbol" : "trash",
         "name" : "Trash",
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : false,
         "messagesCount" : 0,
         "id" : "3",
         "parentId" : "0",
         "type" : "system",
         "subscribedForSharedFolder" : false,
         "revision" : 26,
         "bytes" : 0
      },
      {
         "symbol" : "spam",
         "createDate" : "2017-08-29T19:05:56+0300",
         "recentMessagesCount" : 0,
         "name" : "Spam",
         "messagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : false,
         "unreadMessagesCount" : 0,
         "id" : "2",
         "parentId" : "0",
         "subscribedForSharedFolder" : false,
         "type" : "system",
         "revision" : 1,
         "bytes" : 0
      },
      {
         "revision" : 338,
         "bytes" : 4094,
         "parentId" : "0",
         "subscribedForSharedFolder" : false,
         "type" : "system",
         "messagesCount" : 5,
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "isThreadable" : true,
         "id" : "6",
         "symbol" : "draft",
         "recentMessagesCount" : 5,
         "createDate" : "2017-08-29T19:05:56+0300",
         "name" : "Drafts"
      },
      {
         "subscribedForSharedFolder" : false,
         "type" : "system",
         "parentId" : "0",
         "revision" : 1,
         "bytes" : 0,
         "name" : "Outbox",
         "symbol" : "outbox",
         "createDate" : "2017-08-29T19:05:56+0300",
         "recentMessagesCount" : 0,
         "id" : "5",
         "messagesCount" : 0,
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "isThreadable" : true
      }
   ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /folders_tree

### POST /folders_tree

```POST https://{host}/v2/folders_tree```

### GET /folders_tree

Get sorted tree of user folders

```GET https://{host}/v2/folders_tree```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **sort**: *(required)  one of [date, lang, position]*

  тип сортировки

* **lang**: *one of [az, be, en, hy, ka, kk, ro, ru, tr, tt, uk]*

  идентификтаор языка (ISO 639-1) для сортировки по алфавиту. Обязателен для типа сортировки "lang"

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "folders_tree.schema.json",
    "title": "Folders tree",
    "description": "Tree of user folders",
    "type":"object",
    "properties": {
        "folders_tree" : {"type": "array","items": { "$ref": "folder_with_subfolders.schema.json"}}
    },
    "required": ["folders_tree"],
    "additionalProperties": false
}

```

**Example**

```json

{
   "folders_tree" : [
      {
         "recentMessagesCount" : 141,
         "parentId" : "0",
         "isThreadable" : true,
         "type" : "system",
         "bytes" : 659727,
         "name" : "Inbox",
         "symbol" : "inbox",
         "unreadMessagesCount" : 88,
         "messagesCount" : 141,
         "createDate" : "2017-08-29T19:05:56+0300",
         "id" : "1",
         "isSubscribedForSharedFolder" : false,
         "subfolders" : [],
         "isUnvisited" : false,
         "revision" : 342
      },
      {
         "revision" : 382,
         "isSubscribedForSharedFolder" : false,
         "isUnvisited" : false,
         "subfolders" : [],
         "createDate" : "2018-09-17T21:06:37+0300",
         "id" : "45",
         "unreadMessagesCount" : 0,
         "symbol" : "",
         "messagesCount" : 0,
         "name" : "AA",
         "type" : "user",
         "bytes" : 0,
         "parentId" : "0",
         "recentMessagesCount" : 0,
         "isThreadable" : true
      },
      {
         "revision" : 317,
         "isSubscribedForSharedFolder" : false,
         "subfolders" : [
            {
               "revision" : 318,
               "isUnvisited" : false,
               "subfolders" : [
                  {
                     "isThreadable" : true,
                     "parentId" : "14",
                     "recentMessagesCount" : 0,
                     "bytes" : 0,
                     "type" : "user",
                     "name" : "abacaba",
                     "messagesCount" : 0,
                     "symbol" : "",
                     "unreadMessagesCount" : 0,
                     "createDate" : "2018-09-25T14:11:33+0300",
                     "id" : "49",
                     "subfolders" : [],
                     "isUnvisited" : false,
                     "isSubscribedForSharedFolder" : false,
                     "revision" : 388
                  }
               ],
               "isSubscribedForSharedFolder" : false,
               "createDate" : "2018-08-20T15:36:09+0300",
               "id" : "14",
               "messagesCount" : 0,
               "unreadMessagesCount" : 0,
               "symbol" : "",
               "name" : "algo",
               "bytes" : 0,
               "type" : "user",
               "isThreadable" : true,
               "parentId" : "13",
               "recentMessagesCount" : 0
            },
            {
               "recentMessagesCount" : 0,
               "parentId" : "13",
               "isThreadable" : true,
               "type" : "user",
               "bytes" : 0,
               "name" : "qwerty",
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "messagesCount" : 0,
               "createDate" : "2018-08-20T15:36:36+0300",
               "id" : "16",
               "isSubscribedForSharedFolder" : false,
               "subfolders" : [],
               "isUnvisited" : false,
               "revision" : 321
            },
            {
               "name" : "web",
               "type" : "user",
               "bytes" : 0,
               "recentMessagesCount" : 0,
               "parentId" : "13",
               "isThreadable" : true,
               "revision" : 320,
               "isSubscribedForSharedFolder" : false,
               "isUnvisited" : false,
               "subfolders" : [],
               "createDate" : "2018-08-20T15:36:21+0300",
               "id" : "15",
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "messagesCount" : 0
            }
         ],
         "isUnvisited" : false,
         "createDate" : "2018-08-20T15:35:40+0300",
         "id" : "13",
         "unreadMessagesCount" : 0,
         "symbol" : "",
         "messagesCount" : 0,
         "name" : "english",
         "type" : "user",
         "bytes" : 0,
         "parentId" : "0",
         "recentMessagesCount" : 0,
         "isThreadable" : true
      },
      {
         "revision" : 384,
         "subfolders" : [],
         "isUnvisited" : false,
         "isSubscribedForSharedFolder" : false,
         "createDate" : "2018-09-17T21:06:50+0300",
         "id" : "47",
         "messagesCount" : 0,
         "symbol" : "",
         "unreadMessagesCount" : 0,
         "name" : "hh",
         "bytes" : 0,
         "type" : "user",
         "isThreadable" : true,
         "parentId" : "0",
         "recentMessagesCount" : 0
      },
      {
         "createDate" : "2018-08-20T15:34:01+0300",
         "id" : "8",
         "messagesCount" : 0,
         "symbol" : "",
         "unreadMessagesCount" : 0,
         "revision" : 312,
         "isUnvisited" : false,
         "subfolders" : [
            {
               "createDate" : "2018-09-12T15:58:13+0300",
               "id" : "37",
               "messagesCount" : 0,
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "revision" : 374,
               "subfolders" : [],
               "isUnvisited" : false,
               "isSubscribedForSharedFolder" : false,
               "bytes" : 0,
               "type" : "user",
               "isThreadable" : true,
               "parentId" : "8",
               "recentMessagesCount" : 0,
               "name" : "аа"
            },
            {
               "name" : "бб",
               "isThreadable" : true,
               "recentMessagesCount" : 0,
               "parentId" : "8",
               "bytes" : 0,
               "type" : "user",
               "subfolders" : [],
               "isUnvisited" : false,
               "isSubscribedForSharedFolder" : false,
               "revision" : 376,
               "messagesCount" : 0,
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "createDate" : "2018-09-12T15:58:24+0300",
               "id" : "39"
            },
            {
               "subfolders" : [],
               "isUnvisited" : false,
               "isSubscribedForSharedFolder" : false,
               "revision" : 377,
               "messagesCount" : 0,
               "unreadMessagesCount" : 0,
               "symbol" : "",
               "createDate" : "2018-09-12T15:58:33+0300",
               "id" : "40",
               "name" : "ёё",
               "isThreadable" : true,
               "recentMessagesCount" : 0,
               "parentId" : "8",
               "bytes" : 0,
               "type" : "user"
            },
            {
               "isThreadable" : true,
               "recentMessagesCount" : 0,
               "parentId" : "8",
               "bytes" : 0,
               "type" : "user",
               "name" : "яя",
               "messagesCount" : 0,
               "unreadMessagesCount" : 0,
               "symbol" : "",
               "createDate" : "2018-09-12T15:58:21+0300",
               "id" : "38",
               "isUnvisited" : false,
               "subfolders" : [],
               "isSubscribedForSharedFolder" : false,
               "revision" : 375
            }
         ],
         "isSubscribedForSharedFolder" : false,
         "bytes" : 0,
         "type" : "user",
         "isThreadable" : true,
         "recentMessagesCount" : 0,
         "parentId" : "0",
         "name" : "russian"
      },
      {
         "recentMessagesCount" : 0,
         "parentId" : "0",
         "isThreadable" : true,
         "type" : "user",
         "bytes" : 0,
         "name" : "test",
         "symbol" : "",
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "createDate" : "2018-09-17T20:43:14+0300",
         "id" : "41",
         "isSubscribedForSharedFolder" : false,
         "isUnvisited" : false,
         "subfolders" : [
            {
               "name" : "аа",
               "parentId" : "41",
               "recentMessagesCount" : 0,
               "isThreadable" : true,
               "type" : "user",
               "bytes" : 0,
               "isSubscribedForSharedFolder" : false,
               "isUnvisited" : false,
               "subfolders" : [],
               "revision" : 379,
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "messagesCount" : 0,
               "id" : "42",
               "createDate" : "2018-09-17T20:43:21+0300"
            },
            {
               "revision" : 381,
               "isSubscribedForSharedFolder" : false,
               "isUnvisited" : false,
               "subfolders" : [],
               "createDate" : "2018-09-17T20:43:29+0300",
               "id" : "44",
               "unreadMessagesCount" : 0,
               "symbol" : "",
               "messagesCount" : 0,
               "name" : "бб",
               "type" : "user",
               "bytes" : 0,
               "recentMessagesCount" : 0,
               "parentId" : "41",
               "isThreadable" : true
            },
            {
               "name" : "яя",
               "type" : "user",
               "bytes" : 0,
               "recentMessagesCount" : 0,
               "parentId" : "41",
               "isThreadable" : true,
               "revision" : 380,
               "isSubscribedForSharedFolder" : false,
               "subfolders" : [],
               "isUnvisited" : false,
               "createDate" : "2018-09-17T20:43:25+0300",
               "id" : "43",
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "messagesCount" : 0
            }
         ],
         "revision" : 378
      },
      {
         "isUnvisited" : false,
         "subfolders" : [
            {
               "revision" : 323,
               "subfolders" : [],
               "isUnvisited" : false,
               "isSubscribedForSharedFolder" : false,
               "createDate" : "2018-08-20T15:38:14+0300",
               "id" : "18",
               "messagesCount" : 0,
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "name" : "Arnavutluk",
               "bytes" : 0,
               "type" : "user",
               "isThreadable" : true,
               "parentId" : "17",
               "recentMessagesCount" : 0
            },
            {
               "createDate" : "2018-08-20T15:39:34+0300",
               "id" : "20",
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "messagesCount" : 0,
               "revision" : 325,
               "isSubscribedForSharedFolder" : false,
               "subfolders" : [],
               "isUnvisited" : false,
               "type" : "user",
               "bytes" : 0,
               "recentMessagesCount" : 0,
               "parentId" : "17",
               "isThreadable" : true,
               "name" : "geyik"
            }
         ],
         "isSubscribedForSharedFolder" : false,
         "revision" : 322,
         "messagesCount" : 0,
         "symbol" : "",
         "unreadMessagesCount" : 0,
         "createDate" : "2018-08-20T15:37:17+0300",
         "id" : "17",
         "name" : "Türk",
         "isThreadable" : true,
         "parentId" : "0",
         "recentMessagesCount" : 0,
         "bytes" : 0,
         "type" : "user"
      },
      {
         "isSubscribedForSharedFolder" : false,
         "isUnvisited" : false,
         "subfolders" : [],
         "revision" : 383,
         "unreadMessagesCount" : 0,
         "symbol" : "",
         "messagesCount" : 0,
         "createDate" : "2018-09-17T21:06:43+0300",
         "id" : "46",
         "name" : "ZZ",
         "parentId" : "0",
         "recentMessagesCount" : 0,
         "isThreadable" : true,
         "type" : "user",
         "bytes" : 0
      },
      {
         "isUnvisited" : false,
         "subfolders" : [
            {
               "revision" : 327,
               "isUnvisited" : false,
               "subfolders" : [],
               "isSubscribedForSharedFolder" : false,
               "createDate" : "2018-08-20T15:40:19+0300",
               "id" : "22",
               "messagesCount" : 0,
               "symbol" : "",
               "unreadMessagesCount" : 0,
               "name" : "Абетка",
               "bytes" : 0,
               "type" : "user",
               "isThreadable" : true,
               "recentMessagesCount" : 0,
               "parentId" : "21"
            },
            {
               "name" : "яблуко",
               "bytes" : 0,
               "type" : "user",
               "isThreadable" : true,
               "parentId" : "21",
               "recentMessagesCount" : 0,
               "revision" : 328,
               "isUnvisited" : false,
               "subfolders" : [],
               "isSubscribedForSharedFolder" : false,
               "createDate" : "2018-08-20T15:40:29+0300",
               "id" : "23",
               "messagesCount" : 0,
               "unreadMessagesCount" : 0,
               "symbol" : ""
            }
         ],
         "isSubscribedForSharedFolder" : false,
         "revision" : 326,
         "messagesCount" : 0,
         "symbol" : "",
         "unreadMessagesCount" : 0,
         "createDate" : "2018-08-20T15:40:07+0300",
         "id" : "21",
         "name" : "український",
         "isThreadable" : true,
         "recentMessagesCount" : 0,
         "parentId" : "0",
         "bytes" : 0,
         "type" : "user"
      },
      {
         "messagesCount" : 0,
         "symbol" : "archive",
         "unreadMessagesCount" : 0,
         "createDate" : "2018-02-15T15:38:36+0300",
         "id" : "7",
         "subfolders" : [],
         "isUnvisited" : false,
         "isSubscribedForSharedFolder" : false,
         "revision" : 32,
         "isThreadable" : true,
         "recentMessagesCount" : 0,
         "parentId" : "0",
         "bytes" : 0,
         "type" : "system",
         "name" : "არქივი"
      },
      {
         "createDate" : "2017-08-29T19:05:56+0300",
         "id" : "4",
         "messagesCount" : 95,
         "symbol" : "sent",
         "unreadMessagesCount" : 0,
         "revision" : 332,
         "subfolders" : [],
         "isUnvisited" : false,
         "isSubscribedForSharedFolder" : false,
         "bytes" : 622763,
         "type" : "system",
         "isThreadable" : true,
         "parentId" : "0",
         "recentMessagesCount" : 95,
         "name" : "Sent"
      },
      {
         "createDate" : "2017-08-29T19:05:56+0300",
         "id" : "3",
         "unreadMessagesCount" : 0,
         "symbol" : "trash",
         "messagesCount" : 0,
         "revision" : 26,
         "isSubscribedForSharedFolder" : false,
         "subfolders" : [],
         "isUnvisited" : false,
         "type" : "system",
         "bytes" : 0,
         "recentMessagesCount" : 0,
         "parentId" : "0",
         "isThreadable" : false,
         "name" : "Trash"
      },
      {
         "subfolders" : [],
         "isUnvisited" : false,
         "isSubscribedForSharedFolder" : false,
         "revision" : 1,
         "messagesCount" : 0,
         "unreadMessagesCount" : 0,
         "symbol" : "spam",
         "id" : "2",
         "createDate" : "2017-08-29T19:05:56+0300",
         "name" : "Spam",
         "isThreadable" : false,
         "parentId" : "0",
         "recentMessagesCount" : 0,
         "bytes" : 0,
         "type" : "system"
      },
      {
         "subfolders" : [
            {
               "name" : "template",
               "parentId" : "6",
               "recentMessagesCount" : 1,
               "isThreadable" : true,
               "type" : "system",
               "bytes" : 625,
               "isSubscribedForSharedFolder" : false,
               "isUnvisited" : false,
               "subfolders" : [],
               "revision" : 387,
               "unreadMessagesCount" : 0,
               "symbol" : "template",
               "messagesCount" : 1,
               "id" : "48",
               "createDate" : "2018-09-21T16:06:16+0300"
            }
         ],
         "isUnvisited" : false,
         "isSubscribedForSharedFolder" : false,
         "revision" : 338,
         "messagesCount" : 5,
         "unreadMessagesCount" : 0,
         "symbol" : "draft",
         "createDate" : "2017-08-29T19:05:56+0300",
         "id" : "6",
         "name" : "Drafts",
         "isThreadable" : true,
         "parentId" : "0",
         "recentMessagesCount" : 5,
         "bytes" : 4094,
         "type" : "system"
      },
      {
         "bytes" : 0,
         "type" : "system",
         "isThreadable" : true,
         "recentMessagesCount" : 0,
         "parentId" : "0",
         "name" : "Outbox",
         "createDate" : "2017-08-29T19:05:56+0300",
         "id" : "5",
         "messagesCount" : 0,
         "symbol" : "outbox",
         "unreadMessagesCount" : 0,
         "revision" : 1,
         "isUnvisited" : false,
         "subfolders" : [],
         "isSubscribedForSharedFolder" : false
      }
   ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /mids_by_tids_and_lids

### POST /mids_by_tids_and_lids

```POST https://{host}/v2/mids_by_tids_and_lids```

### GET /mids_by_tids_and_lids

Get MIDs of letters in the threads given by TIDs with labels given by LIDs

```GET https://{host}/v2/mids_by_tids_and_lids```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tid**: *(required)  array of integer*

  TIDs to search MIDs in

* **lid**: *(required)  array of integer*

  LIDs in messages to be searched for

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "mids.schema.json",
    "title": "mids",
    "description": "Sequence of message IDs",
    "type":"object",
    "properties": {
        "mids" : {"type": "array","items": { "$ref": "mid.schema.json"}}
    },
    "required": ["mids"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "mids" : ["156741567024836541","156787562023236542"]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /changelog

### GET /changelog

Get user changelog with specified types from specified revision.

```GET https://{host}/v2/changelog```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **revision**: *(required)  integer*

  Start revision for changes to select. Unsigned.

* **max_count**: *(required)  integer*

  Maximum number of changes allowed to return. Can not be more than 1000.

* **changelog_types**: *array of [store, update, delete, copy, move, quick-save, threads-join, label-create, label-delete, label-modify, folder-create, folder-delete, folder-modify]*

  List of changes to search

* **check_revision_policy**: *one of [loyal, strict]*

  If strict, checks that a record with specified revision exists. Return error if revision not found. Default loyal

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

Return data delta events with specified type in the response body. If check_revision_policy is strong, revision was found in user changelog

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "changes.schema.json",
    "title": "Changes",
    "description": "List of changes sorted by revision",
    "type":"object",
    "properties": {
        "changes" : {"type": "array","items": { "$ref": "change.schema.json"}}
    },
    "required": ["changes"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "changes": [
        {
            "revision": 861,
            "type": "store",
            "value": [
                {
                    "attachments": [],
                    "attachmentsCount": 0,
                    "attachmentsFullSize": 0,
                    "bcc": [],
                    "cc": [],
                    "date": 1533560112,
                    "fid": "1",
                    "firstline": "asdfasdf asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdf",
                    "from": [
                        {
                            "displayName": "Abdul Akhmed",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "imapId": "164",
                    "inReplyTo": "",
                    "labels": [
                        "103",
                        "24",
                        "FAKE_MULCA_SHARED_LBL",
                        "FAKE_RECENT_LBL"
                    ],
                    "mid": "166351711235998026",
                    "newCount": 0,
                    "receiveDate": 1533560112,
                    "references": "",
                    "replyTo": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "revision": 861,
                    "rfcId": "&lt;1281533560112@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                    "size": 1826,
                    "stid": "320.mail:0.E3960:3118342638140744549041442953089",
                    "subject": "asdf",
                    "subjectInfo": {
                        "isSplitted": true,
                        "postfix": "",
                        "prefix": "",
                        "subject": "asdf",
                        "type": ""
                    },
                    "threadCount": 0,
                    "threadId": "164944336352444719",
                    "to": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "types": [
                        4,
                        55
                    ],
                    "uidl": ""
                }
            ]
        },
        {
            "revision": 866,
            "type": "delete",
            "value": [
                "166351711235998027"
            ]
        },
        {
            "revision": 867,
            "type": "store",
            "value": [
                {
                    "attachments": [],
                    "attachmentsCount": 0,
                    "attachmentsFullSize": 0,
                    "bcc": [],
                    "cc": [],
                    "date": 1533560269,
                    "fid": "4",
                    "firstline": "asdfasdfsdf asdf",
                    "from": [
                        {
                            "displayName": "Abdul Akhmed",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "imapId": "64",
                    "inReplyTo": "",
                    "labels": [
                        "103",
                        "24",
                        "FAKE_MULCA_SHARED_LBL",
                        "FAKE_RECENT_LBL",
                        "FAKE_SEEN_LBL"
                    ],
                    "mid": "166351711235998028",
                    "newCount": 0,
                    "receiveDate": 1533560269,
                    "references": "",
                    "replyTo": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "revision": 867,
                    "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                    "size": 3175,
                    "stid": "320.mail:0.E4192:3118342638107170542233819674492",
                    "subject": "No subject",
                    "subjectInfo": {
                        "isSplitted": true,
                        "postfix": "",
                        "prefix": "",
                        "subject": "No subject",
                        "type": ""
                    },
                    "threadCount": 0,
                    "threadId": "166351711235998028",
                    "to": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "types": [
                        4,
                        55
                    ],
                    "uidl": ""
                }
            ]
        },
        {
            "revision": 868,
            "type": "store",
            "value": [
                {
                    "attachments": [],
                    "attachmentsCount": 0,
                    "attachmentsFullSize": 0,
                    "bcc": [],
                    "cc": [],
                    "date": 1533560269,
                    "fid": "1",
                    "firstline": "asdfasdfsdf asdf",
                    "from": [
                        {
                            "displayName": "Abdul Akhmed",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "imapId": "165",
                    "inReplyTo": "",
                    "labels": [
                        "103",
                        "24",
                        "FAKE_MULCA_SHARED_LBL",
                        "FAKE_RECENT_LBL",
                        "FAKE_SEEN_LBL"
                    ],
                    "mid": "166351711235998029",
                    "newCount": 0,
                    "receiveDate": 1533560269,
                    "references": "",
                    "replyTo": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "revision": 871,
                    "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                    "size": 3175,
                    "stid": "320.mail:0.E4192:3118342638107170542233819674492",
                    "subject": "No subject",
                    "subjectInfo": {
                        "isSplitted": true,
                        "postfix": "",
                        "prefix": "",
                        "subject": "No subject",
                        "type": ""
                    },
                    "threadCount": 0,
                    "threadId": "166351711235998028",
                    "to": [
                        {
                            "displayName": "abdul@yandex.ru",
                            "domain": "yandex.ru",
                            "local": "abdul"
                        }
                    ],
                    "types": [
                        4,
                        55
                    ],
                    "uidl": ""
                }
            ]
        },
        {
            "revision": 871,
            "type": "update",
            "value": [
                {
                    "labels": [
                        "FAKE_SEEN_LBL",
                        "FAKE_RECENT_LBL",
                        "24",
                        "103"
                    ],
                    "mid": "166351711235998029"
                }
            ]
        }
    ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /tabs

### GET /tabs

Get list of user tabs

```GET https://{host}/v2/tabs```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "tabs.schema.json",
    "title": "Tabs",
    "description": "Sequence of user tabs",
    "type":"object",
    "properties": {
        "tabs" : {"type": "array","items": { "$ref": "tab.schema.json"}}
    },
    "required": ["tabs"],
    "additionalProperties": false
}

```

**Example**

```json

{
   "tabs" : [
      {
         "type" : "relevant",
         "unreadMessagesCount" : 88,
         "isUnvisited" : true,
         "messagesCount" : 141,
         "createDate" : "2017-08-29T19:05:56+0300",
         "revision" : 342,
         "bytes" : 659727,
         "freshMessagesCount" : 10
      },
      {
         "bytes" : 0,
         "revision" : 382,
         "type" : "social",
         "isUnvisited" : false,
         "unreadMessagesCount" : 0,
         "messagesCount" : 0,
         "createDate" : "2018-09-17T21:06:37+0300",
         "freshMessagesCount" : 0
      },
      {
         "type" : "news",
         "revision" : 317,
         "bytes" : 0,
         "createDate" : "2018-08-20T15:35:40+0300",
         "unreadMessagesCount" : 0,
         "isUnvisited" : false,
         "messagesCount" : 0,
         "freshMessagesCount" : 0
      }
   ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Examples**
* **cannot work with tabs**:

```json

{
    "error":{
        "code":5020,
        "message":"user cannot work with tabs yet",
        "reason":""
    }
}

```

* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /messages_by_tab

### GET /messages_by_tab

Get list of messages in tab (sorted by received_date)

```GET https://{host}/v2/messages_by_tab```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tab**: *(required)  one of [relevant, news, social]*

  A tab to select messages from

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

* **count**: *(required)  integer*

  Amount of messages in response (if requested with [page] will response [count+1] messages)

* **first**: *integer*

  Offset for messages selection (starts with 0) - either [first] or [page] is required

* **page**: *integer*

  Offset for messages selection (starts with 1, [first = count * (page - 1)]) - either [first] or [page] is required

* **since**: *integer*

  Left bound of [since; till) range (default is 0)

* **till**: *integer*

  Right bound of [since; till) range (default is now)

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "messages.schema.json",
    "title": "Messages",
    "description": "User messages metadata",
    "type":"object",
    "properties": {
        "envelopes" : {"type": "array","items": { "$ref": "envelope.schema.json"}}
    },
    "required": ["envelopes"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "envelopes": [
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560112,
            "fid": "1",
            "tab": "relevant",
            "firstline": "asdfasdf asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdf",
            "from": [
                {
                   "displayName": "Abdul Akhmed",
                   "domain": "yandex.ru",
                   "local": "abdul"
                }
            ],
            "imapId": "164",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL"
            ],
            "mid": "166351711235998026",
            "newCount": 0,
            "receiveDate": 1533560112,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 861,
            "rfcId": "&lt;1281533560112@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 1826,
            "stid": "320.mail:0.E3960:3118342638140744549041442953089",
            "subject": "asdf",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "asdf",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "164944336352444719",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        },
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560269,
            "fid": "4",
            "tab": "",
            "firstline": "asdfasdfsdf asdf",
            "from": [
                {
                    "displayName": "Abdul Akhmed",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "imapId": "64",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL",
                "FAKE_SEEN_LBL"
            ],
            "mid": "166351711235998028",
            "newCount": 0,
            "receiveDate": 1533560269,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 867,
            "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 3175,
            "stid": "320.mail:0.E4192:3118342638107170542233819674492",
            "subject": "No subject",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "No subject",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "166351711235998028",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                        "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        },
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560269,
            "fid": "1",
            "tab": "news",
            "firstline": "asdfasdfsdf asdf",
            "from": [
                {
                    "displayName": "Abdul Akhmed",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "imapId": "165",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL",
                "FAKE_SEEN_LBL"
            ],
            "mid": "166351711235998029",
            "newCount": 0,
            "receiveDate": 1533560269,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 871,
            "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 3175,
            "stid": "320.mail:0.E4192:3118342638107170542233819674492",
            "subject": "No subject",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "No subject",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "166351711235998028",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        }
    ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /messages_unread_by_tab

### GET /messages_unread_by_tab

Get list of unread messages in tab (sorted by received_date)

```GET https://{host}/v2/messages_unread_by_tab```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tab**: *(required)  one of [relevant, news, social]*

  A tab to select messages from

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

* **count**: *(required)  integer*

  Amount of messages in response (if requested with [page] will response [count+1] messages)

* **first**: *integer*

  Offset for messages selection (starts with 0) - either [first] or [page] is required

* **page**: *integer*

  Offset for messages selection (starts with 1, [first = count * (page - 1)]) - either [first] or [page] is required

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "messages.schema.json",
    "title": "Messages",
    "description": "User messages metadata",
    "type":"object",
    "properties": {
        "envelopes" : {"type": "array","items": { "$ref": "envelope.schema.json"}}
    },
    "required": ["envelopes"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "envelopes": [
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560112,
            "fid": "1",
            "tab": "relevant",
            "firstline": "asdfasdf asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdf",
            "from": [
                {
                   "displayName": "Abdul Akhmed",
                   "domain": "yandex.ru",
                   "local": "abdul"
                }
            ],
            "imapId": "164",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL"
            ],
            "mid": "166351711235998026",
            "newCount": 0,
            "receiveDate": 1533560112,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 861,
            "rfcId": "&lt;1281533560112@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 1826,
            "stid": "320.mail:0.E3960:3118342638140744549041442953089",
            "subject": "asdf",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "asdf",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "164944336352444719",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        },
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560269,
            "fid": "4",
            "tab": "",
            "firstline": "asdfasdfsdf asdf",
            "from": [
                {
                    "displayName": "Abdul Akhmed",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "imapId": "64",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL",
                "FAKE_SEEN_LBL"
            ],
            "mid": "166351711235998028",
            "newCount": 0,
            "receiveDate": 1533560269,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 867,
            "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 3175,
            "stid": "320.mail:0.E4192:3118342638107170542233819674492",
            "subject": "No subject",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "No subject",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "166351711235998028",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                        "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        },
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560269,
            "fid": "1",
            "tab": "news",
            "firstline": "asdfasdfsdf asdf",
            "from": [
                {
                    "displayName": "Abdul Akhmed",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "imapId": "165",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL",
                "FAKE_SEEN_LBL"
            ],
            "mid": "166351711235998029",
            "newCount": 0,
            "receiveDate": 1533560269,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 871,
            "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 3175,
            "stid": "320.mail:0.E4192:3118342638107170542233819674492",
            "subject": "No subject",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "No subject",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "166351711235998028",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        }
    ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /messages_in_tab_with_pins

### GET /messages_in_tab_with_pins

Get pinned messages first and then list of messages in tab (sorted by received_date)

```GET https://{host}/v2/messages_in_tab_with_pins```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tab**: *(required)  one of [relevant, news, social]*

  A tab to select messages from

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

* **count**: *(required)  integer*

  Amount of messages in response (if requested with [page] will response [count+1] messages)

* **first**: *integer*

  Offset for messages selection (starts with 0) - either [first] or [page] is required

* **page**: *integer*

  Offset for messages selection (starts with 1, [first = count * (page - 1)]) - either [first] or [page] is required

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "messages.schema.json",
    "title": "Messages",
    "description": "User messages metadata",
    "type":"object",
    "properties": {
        "envelopes" : {"type": "array","items": { "$ref": "envelope.schema.json"}}
    },
    "required": ["envelopes"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "envelopes": [
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560112,
            "fid": "1",
            "tab": "relevant",
            "firstline": "asdfasdf asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdf",
            "from": [
                {
                   "displayName": "Abdul Akhmed",
                   "domain": "yandex.ru",
                   "local": "abdul"
                }
            ],
            "imapId": "164",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL"
            ],
            "mid": "166351711235998026",
            "newCount": 0,
            "receiveDate": 1533560112,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 861,
            "rfcId": "&lt;1281533560112@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 1826,
            "stid": "320.mail:0.E3960:3118342638140744549041442953089",
            "subject": "asdf",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "asdf",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "164944336352444719",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        },
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560269,
            "fid": "4",
            "tab": "",
            "firstline": "asdfasdfsdf asdf",
            "from": [
                {
                    "displayName": "Abdul Akhmed",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "imapId": "64",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL",
                "FAKE_SEEN_LBL"
            ],
            "mid": "166351711235998028",
            "newCount": 0,
            "receiveDate": 1533560269,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 867,
            "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 3175,
            "stid": "320.mail:0.E4192:3118342638107170542233819674492",
            "subject": "No subject",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "No subject",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "166351711235998028",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                        "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        },
        {
            "attachments": [],
            "attachmentsCount": 0,
            "attachmentsFullSize": 0,
            "bcc": [],
            "cc": [],
            "date": 1533560269,
            "fid": "1",
            "tab": "news",
            "firstline": "asdfasdfsdf asdf",
            "from": [
                {
                    "displayName": "Abdul Akhmed",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "imapId": "165",
            "inReplyTo": "",
            "labels": [
                "103",
                "24",
                "FAKE_MULCA_SHARED_LBL",
                "FAKE_RECENT_LBL",
                "FAKE_SEEN_LBL"
            ],
            "mid": "166351711235998029",
            "newCount": 0,
            "receiveDate": 1533560269,
            "references": "",
            "replyTo": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "revision": 871,
            "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
            "size": 3175,
            "stid": "320.mail:0.E4192:3118342638107170542233819674492",
            "subject": "No subject",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "No subject",
                "type": ""
            },
            "threadCount": 0,
            "threadId": "166351711235998028",
            "to": [
                {
                    "displayName": "abdul@yandex.ru",
                    "domain": "yandex.ru",
                    "local": "abdul"
                }
            ],
            "types": [
                4,
                55
            ],
            "uidl": ""
        }
    ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /threads_by_tab

### GET /threads_by_tab

Get list of threads in tab (sorted by received_date)

```GET https://{host}/v2/threads_by_tab```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tab**: *(required)  one of [relevant, news, social]*

  A tab to select messages from

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

* **count**: *(required)  integer*

  Amount of messages in response (if requested with [page] will response [count+1] messages)

* **first**: *integer*

  Offset for messages selection (starts with 0) - either [first] or [page] is required

* **page**: *integer*

  Offset for messages selection (starts with 1, [first = count * (page - 1)]) - either [first] or [page] is required

* **since**: *integer*

  Left bound of [since; till) range (default is 0)

* **till**: *integer*

  Right bound of [since; till) range (default is now)

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "threads.schema.json",
    "title": "Threads",
    "description": "User messages metadata",
    "type":"object",
    "properties": {
        "threads_by_folder": {
            "type": "object",
            "properties": {
                "envelopes" : {
                    "type": "array",
                    "items": {
                        "$ref": "envelope.schema.json"
                    }
                },
                "threadLabels": {
                    "type": "array",
                    "items": {
                        "$ref": "thread-labels.schema.json"
                    }
                }
            },
            "required": ["envelopes", "threadLabels"],
            "additionalProperties": false
        }
    },
    "required": ["threads_by_folder"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "threads_by_folder": {
        "envelopes": [
            {
                "attachments": [],
                "attachmentsCount": 0,
                "attachmentsFullSize": 0,
                "bcc": [],
                "cc": [],
                "date": 1533560112,
                "fid": "1",
                "tab": "relevant",
                "firstline": "asdfasdf asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdf",
                "from": [
                    {
                        "displayName": "Abdul Akhmed",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "imapId": "164",
                "inReplyTo": "",
                "labels": [
                    "103",
                    "24",
                    "FAKE_MULCA_SHARED_LBL",
                    "FAKE_RECENT_LBL"
                ],
                "mid": "166351711235998026",
                "newCount": 0,
                "receiveDate": 1533560112,
                "references": "",
                "replyTo": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "revision": 861,
                "rfcId": "&lt;1281533560112@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                "size": 1826,
                "stid": "320.mail:0.E3960:3118342638140744549041442953089",
                "subject": "asdf",
                "subjectInfo": {
                    "isSplitted": true,
                    "postfix": "",
                    "prefix": "",
                    "subject": "asdf",
                    "type": ""
                },
                "threadCount": 0,
                "threadId": "164944336352444719",
                "to": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "types": [
                    4,
                    55
                ],
                "uidl": ""
            },
            {
                "attachments": [],
                "attachmentsCount": 0,
                "attachmentsFullSize": 0,
                "bcc": [],
                "cc": [],
                "date": 1533560269,
                "fid": "1",
                "tab": "news",
                "firstline": "asdfasdfsdf asdf",
                "from": [
                    {
                        "displayName": "Abdul Akhmed",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "imapId": "165",
                "inReplyTo": "",
                "labels": [
                    "103",
                    "24",
                    "FAKE_MULCA_SHARED_LBL",
                    "FAKE_RECENT_LBL",
                    "FAKE_SEEN_LBL"
                ],
                "mid": "166351711235998029",
                "newCount": 0,
                "receiveDate": 1533560269,
                "references": "",
                "replyTo": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "revision": 871,
                "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                "size": 3175,
                "stid": "320.mail:0.E4192:3118342638107170542233819674492",
                "subject": "No subject",
                "subjectInfo": {
                    "isSplitted": true,
                    "postfix": "",
                    "prefix": "",
                    "subject": "No subject",
                    "type": ""
                },
                "threadCount": 0,
                "threadId": "166351711235998028",
                "to": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "types": [
                    4,
                    55
                ],
                "uidl": ""
            }
        ],
        "threadLabels" : [
            {
                "tid" : "164944336352444719",
                "tscn" : "828871084968",
                "labels" : [
                    {
                        "lid" : "103",
                        "cnt" : "1"
                    },
                    {
                        "lid" : "24",
                        "cnt" : "1"
                    }
                ]
            },
            {
                "tid" : "166351711235998028",
                "tscn" : "828871084969",
                "labels" : [
                    {
                        "lid" : "103",
                        "cnt" : "2"
                    },
                    {
                        "lid" : "24",
                        "cnt" : "2"
                    }
                ]
            }
        ]
    }
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /threads_in_tab_with_pins

### GET /threads_in_tab_with_pins

Get threads with pinned messages first and then list of threads in tab (sorted by received_date)

```GET https://{host}/v2/threads_in_tab_with_pins```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tab**: *(required)  one of [relevant, news, social]*

  A tab to select messages from

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

* **count**: *(required)  integer*

  Amount of messages in response (if requested with [page] will response [count+1] messages)

* **first**: *integer*

  Offset for messages selection (starts with 0) - either [first] or [page] is required

* **page**: *integer*

  Offset for messages selection (starts with 1, [first = count * (page - 1)]) - either [first] or [page] is required

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "threads.schema.json",
    "title": "Threads",
    "description": "User messages metadata",
    "type":"object",
    "properties": {
        "threads_by_folder": {
            "type": "object",
            "properties": {
                "envelopes" : {
                    "type": "array",
                    "items": {
                        "$ref": "envelope.schema.json"
                    }
                },
                "threadLabels": {
                    "type": "array",
                    "items": {
                        "$ref": "thread-labels.schema.json"
                    }
                }
            },
            "required": ["envelopes", "threadLabels"],
            "additionalProperties": false
        }
    },
    "required": ["threads_by_folder"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "threads_by_folder": {
        "envelopes": [
            {
                "attachments": [],
                "attachmentsCount": 0,
                "attachmentsFullSize": 0,
                "bcc": [],
                "cc": [],
                "date": 1533560112,
                "fid": "1",
                "tab": "relevant",
                "firstline": "asdfasdf asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdf",
                "from": [
                    {
                        "displayName": "Abdul Akhmed",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "imapId": "164",
                "inReplyTo": "",
                "labels": [
                    "103",
                    "24",
                    "FAKE_MULCA_SHARED_LBL",
                    "FAKE_RECENT_LBL"
                ],
                "mid": "166351711235998026",
                "newCount": 0,
                "receiveDate": 1533560112,
                "references": "",
                "replyTo": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "revision": 861,
                "rfcId": "&lt;1281533560112@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                "size": 1826,
                "stid": "320.mail:0.E3960:3118342638140744549041442953089",
                "subject": "asdf",
                "subjectInfo": {
                    "isSplitted": true,
                    "postfix": "",
                    "prefix": "",
                    "subject": "asdf",
                    "type": ""
                },
                "threadCount": 0,
                "threadId": "164944336352444719",
                "to": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "types": [
                    4,
                    55
                ],
                "uidl": ""
            },
            {
                "attachments": [],
                "attachmentsCount": 0,
                "attachmentsFullSize": 0,
                "bcc": [],
                "cc": [],
                "date": 1533560269,
                "fid": "1",
                "tab": "news",
                "firstline": "asdfasdfsdf asdf",
                "from": [
                    {
                        "displayName": "Abdul Akhmed",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "imapId": "165",
                "inReplyTo": "",
                "labels": [
                    "103",
                    "24",
                    "FAKE_MULCA_SHARED_LBL",
                    "FAKE_RECENT_LBL",
                    "FAKE_SEEN_LBL"
                ],
                "mid": "166351711235998029",
                "newCount": 0,
                "receiveDate": 1533560269,
                "references": "",
                "replyTo": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "revision": 871,
                "rfcId": "&lt;1331533560269@myt4-da42643ad020.qloud-c.yandex.net&gt;",
                "size": 3175,
                "stid": "320.mail:0.E4192:3118342638107170542233819674492",
                "subject": "No subject",
                "subjectInfo": {
                    "isSplitted": true,
                    "postfix": "",
                    "prefix": "",
                    "subject": "No subject",
                    "type": ""
                },
                "threadCount": 0,
                "threadId": "166351711235998028",
                "to": [
                    {
                        "displayName": "abdul@yandex.ru",
                        "domain": "yandex.ru",
                        "local": "abdul"
                    }
                ],
                "types": [
                    4,
                    55
                ],
                "uidl": ""
            }
        ],
        "threadLabels" : [
            {
                "tid" : "164944336352444719",
                "tscn" : "828871084968",
                "labels" : [
                    {
                        "lid" : "103",
                        "cnt" : "1"
                    },
                    {
                        "lid" : "24",
                        "cnt" : "1"
                    }
                ]
            },
            {
                "tid" : "166351711235998028",
                "tscn" : "828871084969",
                "labels" : [
                    {
                        "lid" : "103",
                        "cnt" : "2"
                    },
                    {
                        "lid" : "24",
                        "cnt" : "2"
                    }
                ]
            }
        ]
    }
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /reset_tab_unvisited

### GET /reset_tab_unvisited

Reset unvisted flag for tab

```GET https://{host}/v2/reset_tab_unvisited```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tab**: *(required)  one of [relevant, news, social]*

  A tab to reset unvisited flag

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: any

**Example**

```any

{}
```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /with_attaches_counters

### GET /with_attaches_counters

Get count of all messages with attaches and count of new messages with attaches

```GET https://{host}/v2/with_attaches_counters```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "with_attaches_counters.schema.json",
    "title": "with_attaches_counters",
    "description": "Two counters of messages with attaches",
    "type":"object",
    "properties": {
        "messagesCount" : {"type": "integer"},
        "newMessagesCount" : {"type": "integer"}
    },
    "additionalProperties": false
}

```

**Example**

```json

{
    "messagesCount" : 2,
    "newMessagesCount" : 0
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /from_favorite_user_counter

### GET /from_favorite_user_counter

Get count of new messages from favorite users

```GET https://{host}/v2/from_favorite_user_counter```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **counter_limit**: *integer*

  Max count messages in response. Can't be more then 100. Default 100. Unsigned.

* **mailbox_limit**: *integer*

  Max count messages in mailbox. Otherwise throw error. Can't be more then 5000. Default 5000. Unsigned.

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "from_favorite_user_counter.schema.json",
    "title": "from_favorite_user_counter",
    "description": "Counter of new messages from favorite users",
    "type":"object",
    "properties": {
        "newMessagesCount" : {"type": "integer"}
    },
    "additionalProperties": false
}

```

**Example**

```json

{
    "newMessagesCount" : 12
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /short_fresh_message

### GET /short_fresh_message

Get new unread message in tab 'relevant'

```GET https://{host}/v2/short_fresh_message```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: short_fresh_message

**Example**

```short_fresh_message

{
    "messages": [
        {
            "from": [
                {
                   "displayName": "Abdul Akhmed",
                   "domain": "yandex.ru",
                   "local": "abdul"
                }
            ],
            "mid": "166351711235998026",
            "receiveDate": 1533560112,
            "subject": "asdf",
            "subjectInfo": {
                "isSplitted": true,
                "postfix": "",
                "prefix": "",
                "subject": "asdf",
                "type": ""
            }
        }
    ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /freezing_info

### GET /freezing_info

Get freezing-related user info

```GET https://{host}/v2/freezing_info```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "freezing.schema.json",
    "title": "freezing",
    "description": "user freezing-related info",
    "type": "object",
    "properties": {
        "notifiesCount": {
            "type": "integer",
            "description": "how many times the user was notified about changing his state"
        },
        "state": {
            "$ref": "user_state.schema.json"
        },
        "lastStateUpdateEpoch": {
            "type": "integer",
            "description": "epoch time in UTC when the last state change happened"
        }
    },
    "required": ["notifiesCount", "state", "lastStateUpdateEpoch"],
    "additionalProperties": false
}

```

**Example**

```json

{
    "notifiesCount": 3,
    "state": "active",
    "lastStateUpdateEpoch": 1602968400
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /unfreeze_user

### POST /unfreeze_user

```POST https://{host}/v2/unfreeze_user```

### GET /unfreeze_user

Unfreeze user

```GET https://{host}/v2/unfreeze_user```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: any

**Example**

```any

{}
```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /archive_status

### GET /archive_status

Get user's archive info

```GET https://{host}/v2/archive_status```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: any

**Example**

```any

{
    "user_state": "archived",
    "archive_state": "archivation_complete",
    "message_count": 123,
    "restored_message_count": 42
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /stickers

### GET /stickers

Get list of user's stickers

```GET https://{host}/v2/stickers```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **type**: *(required)  reply_later*

  Type of stickers

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "stickers.schema.json",
    "title": "Stickers",
    "description": "Sequence of user stickers",
    "type":"object",
    "properties": {
        "stickers" : {"type": "array","items": { "$ref": "sticker.schema.json"}}
    },
    "required": ["stickers"],
    "additionalProperties": false
}

```

**Example**

```json

{
   "stickers" : [
      {
         "tid" : "177892185281134593",
         "mid" : "177892185281134593",
         "fid" : "1",
         "created" : 1640002113,
         "date" : 1640005113,
         "type" : "reply_later"
      }
   ]
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /first_envelope_date

### GET /first_envelope_date

Get date of the first message in folder

```GET https://{host}/v2/first_envelope_date```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **fid**: *(required)  json*

  A fid to select date from

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "first_envelope_date.schema.json",
    "title": "first_envelope_date",
    "description": "date of the first message in the particular folder",
    "type": "object",
    "properties": {
      "first_envelope_date": {
        "type": "integer",
        "description": "unixtime of the first message",
        "required": false
      }
    },
    "additionalProperties": false
}

```

**Example**

```json

{
    "first_envelope_date":1640251803
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

## /first_envelope_date_in_tab

### GET /first_envelope_date_in_tab

Get date of the first message in tab

```GET https://{host}/v2/first_envelope_date_in_tab```

#### Request

##### Headers

* **X-Request-Id**: *string*

  Request identifier. Allow to trace request.

* **X-Real-Ip**: *string*

  User IP or request source IP. Required to pass to other services to trace user activity.

##### Query Parameters

* **tab**: *(required)  one of [relevant, news, social]*

  A tab to select date from

* **uid**: *(required)  integer*

  User identifier

* **dbtype**: *one of [master, replica]*

  Database access strategy - master or replica will be tried first

* **caller**: *string*

  User to access database from behalf of

* **connection_id**: *string*

#### HTTP status code [200](https://httpstatuses.com/200)

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "$id": "first_envelope_date_in_tab.schema.json",
    "title": "first_envelope_date_in_tab",
    "description": "date of the first message in the particular tab",
    "type": "object",
    "properties": {
      "first_envelope_date_in_tab": {
        "type": "integer",
        "description": "unixtime of the first message",
        "required": false
      }
    },
    "additionalProperties": false
}

```

**Example**

```json

{
    "first_envelope_date_in_tab":1640251803
}

```

</p></details>

#### HTTP status code [400](https://httpstatuses.com/400)

Invalid request - request-related error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":2001,
        "message":"not authenticated",
        "reason":""
    }
}

```

</p></details>

#### HTTP status code [500](https://httpstatuses.com/500)

Internal error - internal server error occurred

<details><summary><b>Body</b></summary><p>

* **Media type**: application/json

* **Type**: json

* **Content**:

```json

{
    "title": "Error",
    "$id": "error.schema.json",
    "description": "Method execution error information",
    "type": "object",
    "properties": {
        "code": {
            "description": "error code",
            "type": "integer"
        },
        "message": {
            "description": "error message",
            "type": "string"
        },
        "reason": {
            "description": "extended error message",
            "type": "string"
        }
    },
    "required": ["code", "message", "reason"],
    "additionalProperties": false
}

```

**Example**
* **common**:

```json

{
    "error":{
        "code":1,
        "message":"unknown error",
        "reason":"unknown error on server-side"
    }
}

```

</p></details>

---
