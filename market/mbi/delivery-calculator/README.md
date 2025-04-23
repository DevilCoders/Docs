# delivery-calculator :dizzy:

## Cборка

Проект собирается через `ya make`

Сгенерировать проект в локальную папку (из корня директории с КД):
```
cd $MBI/delivery-calculator
ya ide idea --yt-store --iml-in-project-root -l  -r ~/IdeaProjects/delivery-calculator
```

Запуск тестов:
```
cd $MBI/delivery-calculator && ya make -A [<module_name>]
```

Вывести дерево зависимостей модуля:
```
cd $MBI/delivery-calculator/<module_name> && ya java dependency-tree
```

Для тестовых зависимостей - аналогично, но из директории `src/test`:
```
cd $MBI/delivery-calculator/<module_name> && ya java dependency-tree src/test
```

Также можно вывести classpath при помощи команды `ya java classpath`.

##  Релизы

Релизная машина КД в ЦУМ: [ссылка](https://tsum.yandex-team.ru/pipe/projects/mbi/delivery-dashboard/delivery-calculator-arcadia-cd-pipeline)

Библиотека `delivery-calculator-indexer-client` теперь тоже релизится через релизный пайплайн

## Запуск личного приложения калькулятора

### База данных для калькулятора

#### Вариант 1. дев база данных с общей схемой

В этом случае будет использоваться дев база данных, на которой уже есть предсозданная схема с таблицами и данными.
Актуальность этих данных никто не поддерживает, поэтому там могут быть битые или устаревшие записи.

Для запуска на dev-базе можно использовать уже готовый файл <br>`src/main/properties.d/local/delivery-calculator-indexer-local.properties`

#### Вариант 2. дев база данных с собственной выделенной схемой

Также используется дев база данных, но в этом случае схема будет в эксклюзивном использовании.
В этом случае потребуется чуть больше работы на старте, а также за заполнение схемы отвечать будет сам разработчик.

* создать пользователя через [db API](https://api.db.yandex-team.ru) или [yc CLI](https://wiki.yandex-team.ru/mdb/quickstart/)
Для этого нужно сгенерировать токен по инструкции https://wiki.yandex-team.ru/MDB/api/#autentifikacijaiavtorizacija
Идентификатор нашей организации и проекта можно найти по ссылке https://iam.cloud.yandex.net:14222/v1/mapping/abc/services/2316

Команда для создания пользователя через `yc`:
```
yc mdb cluster AddUser --clusterId 266467a2-b7d3-4846-9cbc-8d5d9c43370c --name <login> --options '{"password":"<password>", "conn_limit":10}'
```

* пользователем `delivery_indexer`, у которого есть расширенные права на БД - дать права новому пользователю на создание схемы
```
grant create on database delivery_indexer_dev to <login>;
```

* залогиниться новым пользователем и создать отдельную схему
```
CREATE SCHEMA <schema_name> AUTHORIZATION <login>;
```
 
* обновить проперти в файле `src/main/properties.d/local/delivery-calculator-indexer-local.properties`:
 * `market.mbi.deliverycalculator.dbSchema` указать `<schema_name>`
 * `db.user` указать `<login>`
 * `db.password` указать `<password>`

В результате должно получиться примерно так:
```
db.name=delivery_indexer_dev
db.user=delivery_indexer_sergey_fed
db.password=delivery_indexer_sergey_fed
market.mbi.deliverycalculator.dbSchema=delivery_indexer_sergey_fed
```

### Запуск liquibase скриптов

```
./liquibaseDev.sh [update]
```

Данный скрипт предназначен только для накатки на dev-базу. Для других сред достаточно поменять в скрипте переменные с url-ами и credential-ами.<br>
Информацию о поддерживаемых командах можно найти в [документации liquibase](https://www.liquibase.org/documentation/command_line.html#database-update-commands).

## Запуск delivery-calculator-indexer

* Для локального запуска индексера (для инициализации TVM2) нужна библиотека проверки тикетов ticket_parser2 (https://wiki.yandex-team.ru/passport/tvm2/library/#java).
Ее нужно собрать (см. инструкцию под катом _Собрать под Mac или Windows x64 можно так_).
* Из идеи запускать `IndexerApplication`, при этом так же указав переменную окружения `PROPERTIES_DIR=<repo>/delivery-calculator-indexer/src/main/properties.d` 
и VM Options: `-Djava.library.path=/Users/kotov-anton/arcadia/bin` (укажите здесь путь до папки bin в аркадии, в которой вы собирали библиотеку ticket_parser2; 
в этой папке должна быть сишная часть библиотеки - `libticket_parser2_java.dylib`).
**Важно:** используйте полный путь до папки `bin` (должен начинаться с `/`) - _не_ используйте символ домашней директории (`~`).

## Запуск delivery-calculator-search-engine

* Создать файл  `delivery-calculator-search-engine/src/main/properties.d/local/delivery-calculator-search-engine-local.properties` (см. пример `*-etalon`).

* Из идеи запускать `SearchEngineApplication`, при этом указав переменную окружения `PROPERTIES_DIR=<repo>/delivery-calculator-search-engine/src/main/properties.d`.


## Ссылки
Документация на вики: https://wiki.yandex-team.ru/MBI/NewDesign/components/delivery-calculator/

Сервисы в Nanny:
https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_delivery_calculator_indexer/
https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_delivery_calculator_search_engine/

