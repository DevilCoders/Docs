# review

## Сборка.  
Окружение https://deploy.yandex-team.ru/projects/review 

Домены описаны на вики https://wiki.yandex-team.ru/staff/pool/CIA/Revju-2.0/urls/#domeny

Для сборки нужен [ya](https://wiki.yandex-team.ru/yatool/).
Различные вариант команд:
  * выкатить локальный код в тестинг
  `ya tool releaser stand -s tools_review_testing`
  * выкатить локальный код в тестинг только в конкретные deploy units
  `ya tool releaser stand -s tools_review_testing --deploy-units backend:backend`
  * собрать версию и выкатить в анстейбл
  `ya tool releaser release`
  * выкатить собраную версию в тестинг
  `ya tool releaser deploy -e tools_review_testing`
  
Тикеты, упомянутые в коммитах и выкаченные в тестинг переведутся сами.

## Тесты
`docker-compose run backend pytest /src/tests`
Команда поддерживает все ключи запуска pytest, например выполнение тестов с совпадением по подстроке
`docker-compose run backend pytest /src/tests -k test_review`

В пуллреквестах тесты [запускаются на тимсити](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Tools_Applications_Review_ReviewBackendTests).

## Дырки и сети
https://deploy.yandex-team.ru/projects/review


Балансер
[облачный в deploy](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/review.yandex-team.ru/show/)  
[racktables](https://racktables.yandex-team.ru/index.php?page=ipvs&tab=default&vs_id=3348)  
[racktables:доступы](https://racktables.yandex-team.ru/index.php?page=services&tab=vperms#vs-3348) 


Продакшн `_REVIEW_PROD_NETS_`
  * blackbox.yandex-team.ru 80
  * oauth.yandex-team.ru 443
  * staff.yandex-team.ru 443
  * staff-api.yandex-team.ru 443
  * api.oebs.yandex.net 443
  * goals.yandex-team.ru 443
  * fb.yandex-team.ru 443
  * wf.yandex-team.ru 443
  * от `_C_VS_IDM_` 443 до tools-cia.stable.qloud-b.yandex.net
  * от `_CAB_PROD_NETS_` 443 до tools-cia.stable.qloud-b.yandex.net
  * от `_STAFF_PROD_NETS_` 443 до tools-cia.stable.qloud-b.yandex.net
  * до `_C_VS_LOGSTORAGE_` 2181
  * pgaas.mail.yandex.net 12000
  * Монга
    - `_PGAASINTERNALNETS_` 27018 

Тестинг `_REVIEW_TEST_NETS_`
  * blackbox.yandex-team.ru 80
  * oauth.yandex-team.ru 443
  * staff.test.yandex-team.ru 443
  * staff-api.test.yandex-team.ru 443
  * oebs-api-test.ps-oebs.yandex.net 443
  * goals.test.yandex-team.ru 443
  * fb.test.yandex-team.ru 443
  * wf.test.yandex-team.ru 443
  * от `_C_VS_IDM_` 443
  * от `_CAB_TEST_NETS_` 443
  * от `_STAFF_TEST_NETS_` 443
  * до `_C_VS_LOGSTORAGE_TESTING_` 2181
  * pgaas.mail.yandex.net 12000
  * Монга
    - `_PGAASINTERNALNETS_` 27018


[ssh-дырка до сети](https://puncher.yandex-team.ru/?id=590adc830d0795b000537a30)

## База
Созданные базы
```(json)
{
  "abc_service_id": 930,
  "abc_service_slug": "review",
  "yc_project_id": "095ff631-3f97-42b8-b021-8d9a4d54b368"
}
```
https://api.db.yandex-team.ru/api/v1.0/project/930/cluster

Графики  
[reviewdb_test (testing)](https://api.db.yandex-team.ru/api/v1.0/project/930/cluster/7a2094d7-a208-4a3d-9e61-cafa437b7e92/charts)  
[reviewdb (production)](https://api.db.yandex-team.ru/api/v1.0/project/930/cluster/22a22b66-313f-418c-a799-7128fd3497e4/charts)

Пользователи базы ограничены в коннектах — по умолчанию 10 коннектов от одного пользователя в каждом ДЦ, и всего 100 коннектов от всех пользователей в каждом ДЦ.
Я считал как 
```
[prestable] (1 [back] * 4 [workers] + 1 [api] * 4 [workers]) + 
[production] (3 [back] * 4 [workers] + 2 [api] * 4 [workers] + 2 [celery] * 4 [celery workers]) = 64 
```
— по 30 в каждом ДЦ должно хватать для нашего пользователя.

[yasm test db](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=7a2094d7-a208-4a3d-9e61-cafa437b7e92;dbname=reviewdb_test)  
[yasm prod db](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=22a22b66-313f-418c-a799-7128fd3497e4;dbname=reviewdb)


## Секреты
В [секретах qloud](https://platform.yandex-team.ru/secrets), 
доступ на команду разработки сервиса. 

## TVM
Для отладки tvm-аутентификации есть бинарник 
[tvmtool](https://wiki.yandex-team.ru/passport/tvm2/qloud/)
— ставим пакет по инструкции или
используем [докеризованный вариант](https://github.yandex-team.ru/tools/tvmtool-docker) 
```
cp .tvm.json{.example,}
# вписываем секреты из https://abc.yandex-team.ru/services/review/resources/
vim .tvm.json  

# запускаем руками или через докер по инструкции в репозитории
tvmtool -p 10001 -a TOKEN_WHICH_LENGTH_IS_32_SYMBOLS -c .tvm.json

дальше наш код обращается к тулзе на 10001 порту (в qloud на 1).
```
## Миграции
`docker-compose run backend review makemigrations -n (имя миграции) --settings=review.settings_test`


## Настройка мониторингов
Используется [Monitorado](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/monitorado/README.md#getting-started), конфиг для истории хранится в `.monitorado.yml`.

Порядок изменения такой:
1) Установить Monitorado и получить токен (в дальнейших примерах подразумевается, что токен лежит в файле `~/.monitorado/token`, можно делать и по-другому)
2) Отредактировать файл `.monitorado.yml`
3) Провалидировать и посмотреть дифф изменений:
```
    MONITORADO_OAUTH_TOKEN=$(cat ~/.monitorado/token) monitorado diff -v
```
4) Применить изменения:
```
    MONITORADO_OAUTH_TOKEN=$(cat ~/.monitorado/token) monitorado exec -v
```
