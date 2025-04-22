# Копирование базы данных из продакшена

Основная статья про бекапы:
https://ydb.yandex-team.ru/docs/maintenance/backup_and_recovery

Здесь будет приведена краткая версия на примере переливки бонсая в тестинг

## Подготовка
Эти шаги надо сделать один раз

1. Положить в файл `~/.ydb/token` OAuth токен от ydb.
Получить его можно на странице https://ydb.yandex-team.ru:
 - нажать на шестеренку в правом верхнем углу
 - перейти на вкладку auth
 - нажать на кнопку `Give me my token`
 
2. Установить ya
https://wiki.yandex-team.ru/arcadia/Arcadia-Starter-Guide/

## Бекап из прода
```bash
ya ydb -e ydb-ru.yandex.net:2135 -d /ru/verticals/production/general tools dump -p general/bonsai
```
После окончания в текущей папке появится папка с именем `backup_<current_datetime>`.

## Восстановление в тестинг
Если бекап разворачивается в существующее место, то необходимо удалить все существующие таблицы, которые создадутся бекапом.
Для тестинга бонсая можно использовать этот запрос:
https://yql.yandex-team.ru/Operations/X6lwTC--PEfV1QPtP7zZQju6CJL8Y6_buqvA-sj3Omk=

```bash
ya ydb -e ydb-ru-prestable.yandex.net:2135 -d /ru-prestable/verticals/testing/common tools restore -p general/bonsai -i <backup_dicrectory>
```
последним параметром надо указать папку с бекапом, полученную на предыдущем этапе.