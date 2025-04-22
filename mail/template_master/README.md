# Template Master
Сервис для выделения общих паттернов(шаблонов) на потоке входящих email'ов, с онлайн построением 
новых шаблонов и применением уже постоенных ранее.

## Текущее состояние

[Документация лежит в вики](https://wiki.yandex-team.ru/ps/so/templatemaster/)

Сейчас используется только содержимое папок
- backend
- queue

Остальное оставлено на случай, если надо откатить.
Если настал 2023, скорее всего откатывать не придётся.

# Устаревшая документация

<!-- code_chunk_output -->

- [Project Struture](#project-structure)
- [Qloud](#qloud)
- [Graphs](#graphs)
- [Database](#database)
- [Logs](#logs)

<!-- /code_chunk_output -->

## Project Struture

- [bin/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/bin) Сборка бинарного файла с запуском yplatform;
- [lib/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/lib) Модули которые используются в сервисе
  * [db](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/lib/db) Модуль инкапсулирующий логику работы с БД
  * [router](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/lib/router) Модуль отвечающий за выбор нужного инстанса и отправки туда http-запроса для кластеризации email'a
  * [template_pool](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/lib/template_pool) Модуль осуществляющий кластеризацию сообщений и сохранение готовых шаблонов
  * [types](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/lib/types) Основные типы использующиеся в сервисе
  * [template_master](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/lib/template_master) Модуль осуществляющий преобразование входящего запроса во внутреннее представление 
  и реализующий api
  * [http](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/lib/http) Http handlers
- [migrations](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/migrations) Миграции БД
- [ut](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/ut) Unit тесты
- [package](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/package) Все что нужно для сборки и дальнейшей выкладки в Qloud
- [docs](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/docs) Документация

## QLoud
- **[Production environment](https://platform.yandex-team.ru/projects/mail/template-master/production)**
- **[Testing environment](https://platform.yandex-team.ru/projects/mail/template-master/testing)**

Каждое окружение состоит из двух компонентов 
- **sharpei-cloud** Этот компонент используется для получения информации
о шардах базы, где находятся тела шаблонов, статистики по ним, и т.д, для тестинга этот компонент настроен на тестовую
базу для production соответственно на production базу. Информацию по настройке **sharpei-cloud** находится [тут](https://wiki.yandex-team.ru/mail/pg/sharpei/cloud/)
- **template-master** Компонента где запущен сам сервис который непосредственно создает/находит шаблоны и прочее.
в production окружении настроен L3 balancer **template-master.mail.yandex.net**


## Graphs
- **[Graphs](https://yasm.yandex-team.ru/template/panel/Template-Master/)**
- **[Alerts](https://yasm.yandex-team.ru/template/alert/Template-Master-alerts/)**

Для отображения графиков, нужно ввести параметр **env**.
Код панелей находится в папке **yasm**.
Обновить графики можно следующей командой.

```    
curl --data-binary @template-master.j2 'https://yasm.yandex-team.ru/srvambry/tmpl/panels/update/content?key=Template-Master'
``` 

## Database
**[Yandex Cloud](https://yc.yandex-team.ru/folders/foou8sc4vrkglf9r23r6/managed-postgresql)**

Код находится миграций находится в папке **migrations**.
Запросы находятся в **package/deploy/etc/template_master/queries.sql**

#### Накатить миграцию

```
pgmigrate -c 'host=sas-k23q7wjehh85bsfe.db.yandex.net port=6432 user=sherlock password=<password> dbname=sherlockdb_pg sslmode=require' -t <version>  -vv migrate
```


#### Сдампить тела шаблонов шаблонов

```
pg_dump -d sherlockdb_pg -h sas-k23q7wjehh85bsfe.db.yandex.net -U sherlock -W <password> -p 6432 -t template_bodies > template_bodies.sql
```

#### Проиндексировать фичи шаблонов
```
insert into tasks (type, schedule, status, timeout, context) select 'index_template_features', now(), 'NEW'::task_status, interval '1m', json_build_object('stable_sign', stable_sign) as context from template_bodies ;
```

#### Обновить статистику по фичам
```
with features as (select unnest(array_agg(DISTINCT c)) as feature
from (
  select unnest(features)
  from template_meta
) as dt(c))
insert into tasks (type, schedule, status, timeout, context) select 'index_feature', now(), 'NEW'::task_status, interval '1m', json_build_object('feature', feature) as context from features ;
```

## Logs

* Конфиг **push-client** находится [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/package/deploy/etc/push-client/template_master.yaml)
* В **YT** логи находятся [здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/mail-template-master-log&)
* Код парсера находится [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/logfeller/configs/parsers/mail-template-master-log.json)
* Для логирования в сервисе используется библиотека [logdog](https://a.yandex-team.ru/arc/trunk/arcadia/mail/logdog)
* На машинках лог пишется в файлик **/var/log/template_master/template_master.log**

## Нагрузочное тестирование

[Тикет](MAILDLV-3925) на разработку.

[Load](https://platform.yandex-team.ru/projects/mail/template-master/load)-окружение в Qloud

[Sandbox](https://sandbox.yandex-team.ru/task/617988522/view)-джоба для ручки `/find_template`\
[Sandbox](https://sandbox.yandex-team.ru/task/618016229/view)-джоба для ручки `/force_detemple`\
[Sandbox](https://sandbox.yandex-team.ru/task/617989084/view)-джоба для ручки `/route`

[Страничка регрессии](https://lunapark.yandex-team.ru/regress/MAILDLV?service=template-master) в lunapark

Конфиги для джоб [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/load_testing/config)

* Как можно заметить, мы используем свой танк.
Если с ним возникают проблемы, возможно, нужно просто обновить образ
* База тоже [отдельная](https://yc.yandex-team.ru/folders/foou8sc4vrkglf9r23r6/managed-postgresql/cluster/mdb4nraqr3jsjddc2lif).
Поскольку в нее идут запросы только во время стрельб, имеет смысл ее периодически переналивать

Скрипты для генерации патронов: [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/template_master/load_testing/scripts)

**Процедура:**
1. Запускаем последовательно джобы. Все должны завершиться со статусом SUCCESS
2. Смотрим на страничку регрессии. Не должно быть заметно аномалий по сравнению с предыдущими релизами
3. Готово
