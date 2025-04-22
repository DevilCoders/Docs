# Система интеграционного тестирования биллинга

Фреймворк предназначается для проведения интеграциооного и регрессионного тестирования сервисов биллинга.

## Настройки ОС

* поставить git-lfs перед началом работы с проектом.
* в качестве шелла использовать bash

## Quick start

```bash
$ git clone git@github.yandex-team.ru:taxi/billing-docker.git
$ git clone git@github.yandex-team.ru:taxi/backend-py3.git
$ git clone git@github.yandex-team.ru:taxi/billing-test-data.git
$ git clone git@github.yandex-team.ru:taxi/billing-testing.git
$ cd billing-testing
$ ./run.sh examples/billing-accounts-extended
```

## Конфигурация тестов

```json
{
    "alias": "string[optional]",
    "url": "string",
    "query": "query_object",
    "method": "get|post",
    "result": "result_object",
    "require": "string|optional",
    "before": "string[optional]",
    "after": "string[optional]",
    "dump": "object[optional]"
}
```

## Описание параметров

* `url` - Адрес сервиса. 
  Может быть как полным урлом, так и подстановкой: 
  `http://billing-accounts.taxi.dev.yandex.net/ping` или `@billing-accounts/ping`
* `query` - массив запросов или путь к файлу с массивом запросов
* `result` - Структура ответа, с которым надо будет сравнить ответ сервиса
* `alias` - название теста (если указано, то последующие тесты смогут ссылаться на запросы через подстановку)
* `before` - обработчик из класса sibilla.test.Suite.
  Принимет на вход request. Выполняется до запроса к серверу
* `after` - обработчик из класса sibilla.test.Suite.
  Принимает на вход пару request-response. Выполняется после успешного завершения запроса.
* `dump` - Описание, по которому будут сформированы запросы при выполнении бутстрапинга тестов.
  Если не задан, то тест будет использовать пару запрос-ответ из описания.

### Response - стрктура валидатора ответа

```json
{
    "json": "mixed[optional]",
    "data": "string[optional]",
    "status": "int[optional]
}
```

Описание полей:
* `json` - По этой структуре будет выполняться валидация ответа в формате json (если есть).
  Подерживает подстановки вида `@response`.
  В рамках подстановки можно обращаться к конкретному полю: `@response.json.0` или `@response.data`.
* `data` - Тело ответа в виде текста
* `status` - Код ответа

### Query - структура запроса

1. Массив запросов

```json
[
    {
        "json": "mixed[optional]",
        "data": "string[optional]",
        "response": "response_validator[optional]"
    }
]
```

* `json` - тело запроса в виде json
* `data` - тело запроса в виде текста
* `response` - валидатор конкретного запроса (см. выше). 
  Используется в случае если в рамках одного теста исполняется множество разнотипных запросов ответы которых невозможно проверить одним шаблоном.

Так же `query` может представлять из себя не только массив из отдельных запросов, но и путь к файлу, который содержит в себе массив запросов в формате, который описан выше (см examples).

### Dump - формируем кастомный пары запрос-ответ

Для примера:

```json
{
    "request": "@json",
    "response": {
      "json": [
        {
          "account": {
            "entity_external_id": "@json.0.account.entity_external_id",
            "agreement_id": "@json.0.account.agreement_id",
            "currency": "@json.0.account.currency",
            "sub_account": "@json.0.account.sub_account",
            "opened": "@json.0.account.opened",
            "expired": "@json.0.account.expired"
          },
          "balances": "@json.0.balances"
        }
      ],
      "status": 200
    }
}
```

Внутри описания доступны подстановки вида `@data` и `@json`, которые соответственно представляют из себя поля data и json ответа сервера на текущий запрос в рамках сессии.

Объект, который получен при использовании генератора будет использоваться как один из элементов массива query.

## Структура директории с тестами

Базовый набор каталогов (см. examples/billing-accounts-extended): 
```
/
|-suite.py (отнаследованные от sibilla.test.Suite класс, с методами для before- и after-действий)
|-/tests (директория, которая содержит шаблон тестов для генерации итогового кода
|-/generated (сгенерированный набор)
```

## Пишем первые тесты

* В соответсвии с описанием теста создаем json и располагаем его в каталоге tests
* Запускаем `./bootstrap.sh -v <path_to_test_folder>` (-v позволит увидеть больше подробностей исполнения)

Для ускорения отладки (и только для неё! финальные тесты делайте на полном цикле) можно пользовать дополнительные опции:

* -q | --no-rebuild -- Не производит полную перегенерацию системы docker-образов. 
* -n | --no-stop-vms -- Не производит убиение системы docker-контейнеров после работы. Может быть полезно при анализе логов и прочего.

Этих этапов достаточно. Тесты будут скомпилированы на релизной версии проекта и исполнены на исходникках.

Последующие запуски нужно осуществлять без бутстраппинга.

```shell
$ ./run.sh <path_to_test_folder>
```

## Запуск

```bash
$ ./run.sh
```

Будут исполнены тесты billing-test-data/billing-accounts-0min

```bash
$./run.sh [--no-restart] [--make] [--s|service=service_name] \
  [--billing-py3=billing-py3-path]
  [--billing-docker=billing-docker-path]
  [--billing-test-data=billing-test-data-path]
  path_or_subset_name
```

* `--make` - принудительная пересборка образов если они не созданы
* `-s|--service=` - указать сервис, который тестируется (billing-accounts, billing-docs). Можем быть несколько. Умолчание: billing-accounts.
* `path_or_subset_name` - путь к тестам. Умолчание 0min

### Вычисление пути к тестам

* Если `path_or_subset_name` является путем к папке с тестами, то он и будет использован.
* Если `path_or_subset_name` является строкой, то будет выполнен поиск тестов в папках по следующему алгоритму:
  i* Формируем имя `<путь к billing-test-data>/<service>-<path_or_subset_name>`
   * Если данный путь существует, то он будет добавлен к списку тестов
   * проверяем для следующего в списке сервиса
  
```bash
$ ./run.sh -s billing-accounts 4min /path-to-other-tests
```

Будут исполнены тесты из папок:
* billing-test-data/billing-accounts-4min
* /path-to-other-tests

## Запуск в TaxiVMs

Подготовить окружение и включить ipv6 согласно [статье](https://wiki.yandex-team.ru/taxi/backend/docker-integration-tests/#nastrojjkaokruzhenijadljaintegracionnogotestirovanija).


## Замечания

* Если вы хотите использовать before- и after- обработчики, то потребуется определить их в sibilla/decorators/billing_accounts.py (Подробнее можно глянуть в примерах billing-accounts-extended)


## Конфигурация для автоматического запуска в teamcity

Тесты поддерживают автозапуск при сборке релизных проектов. Для этого в сборку встроен запуск check_for_release.sh после каждой сборки.

Необходимые для запуска тесты указываются в файле check_for_release.list.

## Я ничего не делал, но все сломалось

* Возможны проблемы с firewalld. Нужно руками добавить созданную подсеть в зону trusted. Иначе ipv6 трафик ходить не будет.
