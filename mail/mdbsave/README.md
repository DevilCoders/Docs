## mdbsave
### Описание
Сервис для сохранения метаинформации в базу. Тут принимается решение, в какую папку попадет письмо пользователю, к какому треду подклеится, какие метки проставятся и табы и тд, а затем сохраняется в почтовую метабазу.

### Запросы
#### Запрос сохранения метаинформации
* Метод: ```POST```
* URI путь: ```/1/save```
* URI параметры: ```?service=<"service">&session_id=<"URL-encoded session_id">```
* Тело запроса - JSON вида:
```
{
  "rcpts": [{"id": "0", "rcpt": rcpt0}, {"id": "1", "rcpt": rcpt1}],
  "sync(required)": bool
}

rcpt
{
  "user(required)" : {
    "uid(required)": string,
    "suid(optional)": string
  },
  "message(required)": {
    "old_mid(optional)": string,
    "ext_imap_id(optional)": uint,
    "firstline(required)": string,
    "size(optional)": int,
    "lids(optional)": [string],
    "label_symbols(optional)": [string],
    "labels(optional)": [{
        "name(required)": string,
        "type(required)": string
    }],
    "tab(optional)": string,
    "storage(required)": {
      "stid(required)": string,
      "offset(optional)": uint
    }
    "headers(required)": {
      "recieved_date(required)": int,
      "date(optional)": int,
      "subject(required)": string,
      "msg_id(optional)": string,
      "reply_to(optional)": string,
      "in_reply_to(optional)": string,
      "from(required)": [{
        "local(required)": string,
        "domain(required)": string,
        "display_name(required)": string
      }],
      "to(required)": [{
        "local(required)": string,
        "domain(required)": string,
        "display_name(required)": string
      }],
      "cc(optional)": [{
        "local(required)": string,
        "domain(required)": string,
        "display_name(required)": string
      }],
      "bcc(optional)": [{
        "local(required)": string,
        "domain(required)": string,
        "display_name(required)": string
      }],
    },
    "attachments(optional)": [{
      "hid(required)": string,
      "name(required)": string,
      "type(required)": string,
      "size(required)": uint;
    }],
    "mime_parts(optional)": [{
      "hid(required)": string,
      "content_type(required)": string,
      "content_subtype(required)": string,
      "boundary(optional)(optional)": string,
      "name(optional)": string,
      "charset(optional)": string,
      "encoding(optional)": string,
      "content_disposition(optional)": string,
      "file_name(optional)": string,
      "content_id(optional)": string,
      "offset(optional)": uint,
      "length(optional)": uint,
      "data(optional)": string
    }],
    "thread_info(required)": {
      "hash(required)": {
        "namespace(required)": string,
        "value(required)": string
      },
      "limits(required)": {
        "days(required)": int,
        "count(required)": int
      },
      "rule(required)": string,
      "reference_hashes(required)": [string],
      "message_ids(required)": [string],
        "in_reply_to_hash(required)": string,
      "message_id_hash(required)": string
    },
  },
  "folders(required)": {
    "destination(optional)": {
      "fid(optional)": string,
      "path(optional)": {
        "path(optional)": string,
        "delimeter(optional)": string
      },
      "original(optional)": {
        "fid(optional)": string,
        "path(optional)": {
          "path(optional)": string,
          "delimeter(optional)": string
        }
      }
    }
  },
  "actions(required)": {
    "duplicates(required)": {
      "ignore(required)": bool,
      "remove(required)": bool
    },
    "use_filters(required)": bool,
    "disable_push(required)": bool,
    "original(required)": {
      "store_as_deleted(required)": bool,
      "no_such_folder(optional)": string // "fail", "fallback_to_inbox", "create"
    },
    "rules_applied(optional)": {
      "store_as_deleted(required)": bool,
      "no_such_folder(optional)": string // "fail", "fallback_to_inbox", "create"
    }
  }
  "added_lids(optional)": [string],
  "added_symbols(optional)": [string],
  "imap(required)": bool
}
```

### Ответы
#### Запрос обработан корректно
* Код результата: ```200```
* Тело ответа - JSON вида:
```
{
  "rcpts": [{"id": "0", "rcpt": "rcpt0"}, {"id": "1", "rcpt": "rcpt1"}]
}

rcpt
{
  "uid(required)": string,
  "status(required)": string //ok, perm error, temp error,
  "description(optional)": string,
  "mid(optional)": string,
  "imap_id(optional)": string,
  "tid(optional)": string,
  "duplicate(optional)": bool,
  "folder(optional)": {
    "fid(required)": string,
    "name(required)": string,
    "type(required)": string,
    "type_code(required)": int,
  },
  "labels(optional)": [{
    "lid(required)": string,
    "symbol(required)": string
  }]
}
```
#### Некорректный запрос
* Код результата: ```400```
* Тело ответа - JSON вида:
```
{
  "error": "string",
  "message": "string"
}
```
#### В результате обработки запроса произошла ошибка
* Код результата: ```500```
* Тело ответа - JSON вида:
```
{
  "error": "string",
  "message": "string"
}
```
