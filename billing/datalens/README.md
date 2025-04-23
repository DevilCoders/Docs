# datalens

Храним описание отчетов и утилиты для автоматизации

## TOC

* [Идея](#идея)
* [Сборка](#сборка)
* [Использование](#использование)
  * [Получить токен](#получить-токен)
  * [Сборка и запуск](#сборка-и-запуск)
* [Отчеты](#отчеты)
  * [Архитектура](#архитектура)
  * [По видам продаж](#по-видам-продаж)
  * [Клики](#клики)
* [Документация](#документация)



# Идея

Т.к. в DataLens нет средств деплоймента отчетов между окружениями dev → test → prod,
мы пишем своё.

Как оно должно работать:

- Разработчик делает отчет в `dev` окружении DataLens отчет
- После окончания работ, выполняет `./deploy/deploy  --id=aaf74i7me9jy5 --name="test_dash_report"`
- В результате чего:
  - отчет с указанным ID будет сохранён в `./reports/test_dash_reports/reports.json`
  - в `./reports/test_dash_reports/meta.json` будет сохранена информация об Id для данного отчета для каждой из сред. Для среды, куда еще ничего не выкладывалось, будет значение `0`. Так, для впервые сохраненного отчета из `dev` среды, будет `{"dev": "aaf74i7me9jy5", "test": 0, "prod": 0}`
- Полученные файлы надо закоммитить в Аркадию
- Далее, с помошью команд `./deploy/deploy test|prod --name"test_dash_report"` выполнить выкладку отчетов в test/prod среды. Если отчет в какую-то среду выкладывается впервые, то у него изменится значение Id в `meta.json`. Это изменение надо коммитить.

# Сборка

```shell
$ make build

# или

$ ya make
```

# Использование

## Получить токен

Идём сюда:

- https://oauth.yandex-team.ru/authorize?response_type=token&client_id=09cea1cc285845b7b4dc3f409fcacad9

Записываем токен:

```shell
$ export BILLING_CHART_OAUTH_TOKEN="AQAD-..."
```

## Сборка и запуск

```shell
$ make build
$ ./deploy/deploy --help
Usage: deploy [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  dev   Сохраняет указанный отчет из DataLens в JSON...
  prod  Указанный отчет из JSON загружает в prod...
  test  Указанный отчет из JSON загружает в test...
```

# Отчеты

## Архитектура

Каждый отчет делитя на 2 части:

- изменяемая (колонки, внешний вид, фильтры, и т.д.)
- неизменяемая (подключения)

Неизменяемая часть лежит у пользователя `robot-tom-sawyer`:

- https://datalens.yandex-team.ru/navigation/959gxqs7jsk44-robot-tom-sawyer

Изменяемая часть лежит в отдельной директории `balance-reports``:

- https://datalens.yandex-team.ru/navigation/ubkdm1xosuswq-balance-reports

## По видам продаж

Отчет:

- https://datalens.yandex-team.ru/bj7z9lpmpzbk6

Мета описание отчета:

- https://a.yandex-team.ru/arc/trunk/arcadia/billing/datalens/reports/type_sal_test
- https://datalens.yandex-team.ru/navigation/ema2b2mp8tpa9-type-sal-test

Коннектор:

- https://datalens.yandex-team.ru/connections/lik1imzasax0g-arnold-hahn-chyt

## Клики

Запущенную клику можно смотреть так:

- Hahn:
  - https://yt.yandex-team.ru/hahn/operations?pool=balance-chyt

- Arnold:
  - https://yt.yandex-team.ru/arnold/operations?pool=balance-chyt


# Документация

- Про токен:
  - https://datalens.yandex-team.ru/docs/api/auth/
- Про API чартов:
  - https://datalens.yandex-team.ru/docs/api/charts/
- Про API дашбордов:
  - https://datalens.yandex-team.ru/docs/api/dash/
