# Генератор конфигов для renderer

Этот пакет содержит в себе:
* типовые шаблоны nanny-сервисов (а в будущем и deploy-сервисов), в которых запускается renderer с кодом js-шаблонов
* список всех nanny-сервисов под управлением команды report-renderer и инструменты для их обновления

Incoming: типовые конфигурации для [компонентов в warden](https://st.yandex-team.ru/RENDERER-164) и [релизных flow](https://st.yandex-team.ru/RENDERER-688).

## Мотивация

Под нашим управлением находится уже более 50 nanny-сервисов, в которые регулярно нужно вносить изменения. До появления генератора эта работа делалась вручную. Такие изменения занимают много времени (на то, чтобы прокликать в nanny 50 сервисов, может уйти пара часов), высока вероятность допустить ошибку. При внесении сервис под генератор были замечены следующие ошибки:
* в сервисах новостей курьер был запущен на 94 порту, а is-ready вызывался на 90 (по этому адресу отвечал один из воркеров renderer)
* в сервисах pcode не был настроен stopGracePeriod
* в некоторых сервисах не был настроен сбор метрик с ahproxy
* на некоторых приёмках значение опции --ahproxy-threads было ниже, чем значение опции --workers - воркеры не могли использоваться

Генератор был задуман как инструмент, который позволит избавиться от ручного труда настолько, насколько это возможно.

## Структура

Исходный код хранится в папке src.

В `cmds` хранятся cli-команды.

В `services` хранятся описание всех сервисов под управлением команды report-renderer.
Сервисом называем команду, которая 

В `nanny` хранится код, который генерирует представление сервиса в терминах nanny.

В `nanny/options` хранятся типы, описывающие конфигурацию nanny-сервисов из папки services.

## Использование

### Запуск CLI

Конфигурации сервисов хранятся в виде кода, поэтому при каждом изменении нужно вызывать tsc. Чтобы этого не забывать, cli лучше запускать npm-скриптом:

```shell script
npm run --silent cli -- --help
cli.js <command>

Commands:
  cli.js compare   Compare existing service config and generated.
  cli.js fetch     Download JSON-encoded descripton of specified services and
                   write it to stdout
  cli.js generate  Write JSON-encoded descripton of specified services to stdout
  cli.js list      List services
  cli.js slots     Write JSON with yappy slots to stdout.
  cli.js update    Update JSON-encoded descripton of specified services

Options:
  --help     Show help                                                 [boolean]
  --version  Show version number                                       [boolean]
```

### Обновление конфига сервиса

После внесения изменений смотрим изменения, которые будут внесены в nanny:
```shell script
npm run --silent cli -- compare -o fetched.json -g generated.json
webstorm diff fetched.json generated.json
```

**Вливаем изменение в trunk.**

Из trunk коммитим изменения в сервисы:
```shell script
npm run --silent cli -- update -c "Added useful thing" -s service1 service2 ... # Эта команда делает commit в nanny
```

Коммиты, которые ничего не меняют, не появляются в nanny: update можно считать идемпотентной операцией.

Деплоим изменения в nanny.

### Обновление кода для генерации nanny-сервисов

Меняем код.

**Проверяем diff во всех сервисах**:
```shell script
npm run --silent cli -- compare -o fetched.json -g generated.json
webstorm diff fetched.json generated.json (code -d ./fetched.json -g ./generated.json)
```

К команде `compare` тоже можно добавить фильтрацию.

Есть планы [коммитить состояние всех сервисов](https://st.yandex-team.ru/FEI-25356).

Далее то же самое, что при обновлении конфига сервиса.

При изменении кода, скорее всего, будет задето много сервисов и коммитить их нужно будет по частям. Для этого можно использовать опцию `--filter`:

```shell script
# Сервисы, не обслуживающие продовые трафик
npm run --silent cli -- update -c "Made useful change" -f '"testing" in tags'
# Закоммитить продовые сервисы pcode
npm run --silent cli -- update -c "Made useful change" -f '"testing" not in tags and ("pcode" in tags)'
```

Проверить фильтр можно командой list:
```shell script
npm run --silent cli -- list -f '"testing" in tags'
```

Запросы в фильтре можно писать и по другим полям:
```shell script
# В нашем доме поселился пожирающий сосед
npm run --silent cli -- list -f 'ynode.maxOldSpaceSize > 2000'
```
но при отсутствии поля команда завершится с ошибкой. Изначально планировалось, что для фильтрации не-продовых сервисов можно будет использовать запрос `instances.tags.ctype not in ("prestable", "prod", "hamster")`, но часть сервисов находится в gencfg и теги для них в коде не заполнены.

### Обновить zerodiff

Zerodiff - специальный файл, который позволяет стриггерить изменения в сервисе в системе деплоя, в нашем случае - nanny. Содержимое этого файла неважно. Главное, что нужно от zerodiff - это получить в nanny состояние "сервис поменялся".

Внести изменение в zerodiff можно через интерфейс в nanny, либо с помощью опции --zerodiff (-z), важно, чтобы новый контент zerodiff отличался от старого.

```shell script
npm run --silent cli -- update -c "Made useful change" -f '"testing" in tags' -z ">_<"
```

Также можно указать опцию, не передавая контент, тогда в zerodiff будет записан текущий timestamp (например '3/22/2022, 8:28:50 PM').

```shell script
npm run --silent cli -- update -c "Made useful change" -f '"testing" in tags' -z
```

### Сгенерировать конфиги yappy-квот

По каждому конфиг-сервису беток в няне можно сгенерировать соответствующую конфигурацию квот:
```shell script
npm run --silent cli -- slots -s betas-configuration-serp > slots.json
```

В связи с репликацией слотов по паре квот для поддержки работоспособности при -1 ДЦ, каждому конфиг-сервису соответствует такая пара квот.

### Добавление нового шаблона

Делается так же, как и любые другие изменения.

В первую очередь генератор пытается получить параметры sandbox-ресурс из сервиса. Если такого ресурса не нашлось, то ищется последний ресурс указанного типа с `released=stable` в sandbox.

### Обновление секрета для контейнера

Обновить секрет вручную, затем внести изменения в генератор.

## Планы

Использовать генератор для создания [алертов report-renderer](https://a.yandex-team.ru/arc/trunk/arcadia/serp/report-renderer-yasm-templates): https://st.yandex-team.ru/FEI-16721.

Хранить настройки YP и уметь их менять: https://st.yandex-team.ru/FEI-16799.

Создавать и обновлять рецепты на дашбордах nanny: https://st.yandex-team.ru/FEI-17155.

## Известные проблемы

### Конфиг сервиса в коде renderer-service-generator хранит не все данные
Часть данных забирается из nanny-сервиса. Некоторые меняются автоматикой, которая не будет коммитить в этот пакет. Среди забираемых данных:
* все данные о ресурсах (в коде сервиса хранится только тип ресурса и тип таски)
* список PODов для варианта YP_POD_IDS в instances
* все настройки для варианта EXTENDED_GENCFG_GROUPS в instances
* delegation token для секретов
* секции из volumes (файлы, в которых делается подстановка переменных), кроме секции с имененм "configs-generated"; https://wiki.yandex-team.ru/runtime-cloud/nanny/template-volumes/

## Поддержка

Поддержкой пакета занимается [команда report-renderer](https://abc.yandex-team.ru/services/reportrenderer/).

[Задачи](https://st.yandex-team.ru/issues/?_q=queue%3A+FEI+Components%3A+%22%23+renderer-service-generator%22) в startrek: очередь FEI, компонент "# renderer-service-generator"

## Альтернативы

Nanny Services Poor Man's Processor: https://wiki.yandex-team.ru/mixailsamogljadov/nspmp/ - позволяет вносить однотипные изменения во множество nanny-сервисов.
