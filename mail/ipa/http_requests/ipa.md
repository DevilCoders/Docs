В примерах используются креды специальной организации, созданной в тестинге для наших импортов. Домен `pdd-ipa.test`, `org_id` 103356, `admin_uid` 4033943768

#### Залить csv

```
curl -H 'content-type: text/csv; charset=utf-8' 'http://localhost:8002/import/103356/?admin_uid=4033943768&user_ip=127.0.0.1&mark_archive_read=1&imap=1&ssl=1&delete_msgs=1&server=imap.yandex.ru&port=993&name=example.csv' --data-binary @./example.csv
```

#### Узнать статус импорта организации

```
curl 'http://localhost:8002/import/103356/stat/'
```

#### Создать импорт из JSON
```
curl -H 'content-type: application/json; charset=utf-8' 'http://localhost:8002/import/103356/?admin_uid=4033943768&user_ip=127.0.0.1&mark_archive_read=1&imap=1&ssl=1&delete_msgs=1&server=imap.yandex.ru&port=993' --data-binary '{"users": [{"src_login": "rpop-test1@hmnid.ru", "login": "rpoptest100", "password": "mamaamakriminal"}]}'
```

#### Саппорт: Список сборщиков
```
curl 'http://localhost:8002/support/103356/collectors/'
```

#### Саппорт: Список статусов сборщиков
```
curl 'http://localhost:8002/support/103356/collectors-statuses/'
```

#### Саппорт: Подробная информация по сборщику
```
curl 'http://localhost:8002/support/103356/collectors/1/'
```

#### Саппорт: Удалить сборщик
```
curl -XDELETE 'http://localhost:8002/support/103356/collectors/1/'
```

#### Саппорт: Сборщик старт/стоп
```
curl -XPUT -H 'content-type: application/json; charset=utf-8' -d '{"enabled":true}' 'http://localhost:8002/support/103356/collectors/1/'
```

#### Саппорт: Список событий
```
curl 'http://localhost:8002/support/103356/events/'
```

#### Саппорт: Список юзеров
```
curl 'http://localhost:8002/support/103356/users/'
```
