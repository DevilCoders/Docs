Сервис использует технологии:
* [Nirvana](https://nirvana.yandex-team.ru/) для выполнения программного кода.
* [Reactor](https://reactor.yandex-team.ru) для регулярного запуска задач в Нирване.
* [Единый геолог](https://wiki.yandex-team.ru/geotargeting/geolocation-united-geolog/)
* [Lama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/) для управления реакциями
* [YDB](https://ydb.yandex-team.ru) (KiKiMR) для хранения посчитанных в Нирване данных.
* `YQL` over [RMTR](https://rtmr.yandex-team.ru) для чтения логов из потока.
* `S3` для сохранения полученных в Нирване данных и предоставления их сервисам-потребителям.

## What happens when service is down

* В интерфейсе Яндекс.Карт и в мобильном приложении будет отображаться заглушка "Считаем загруженность станции"
вместо пробочного балла.

## Nirvana

Все Workflow хранятся в проекте [maps-front](https://nirvana.yandex-team.ru/project/maps-front/flows/1/filter?@filterName=All&projectId=ExprStringEquals(18c82885-daf4-4b37-8121-f5e517930c9c)&@sorting=created%3Atrue)

`YQL`-содержимое блоков хранится в репозитории в папке [nirvana](nirvana) в виде sql-файлов. Имя файла соответствует
полю `Code` в Нирвана-блоке, в котором этот `YQL`-запрос выполняется. Значение поля `Code` уникально в пределах одного Нирвана-workflow и сохраняется при клонировании.

![name](code.png)

Подробнее воркфлоу описаны в [nirvana/README.md](nirvana/README.md)

## Reactor

Все реакции хранятся в [директории](https://reactor.yandex-team.ru/browse?selected=6864201&namespaceType=ns_folder)
Сейчас запущено три реакции, которые соответсвуют трём Нирвана-воркфлоу:
metro-jams-create - генерация пробочного балла
metro-jams-score-logs - логирование пробочного балла для аналитики
metro-jams-data-fullness - верификация количества сигналов

Конфиги, используемые Lama для генерирования реакций:
[metro-jams-data-fullness](./configs/lama/metro-jams-data-fullness/lama.yaml)
[metro-jams-score-logs](./configs/lama/metro-jams-score-logs/lama.yaml)
[metro-jams-create](./configs/lama/metro-jams-create/lama.yaml)

Подробнее воркфлоу описаны в [nirvana/README.md](nirvana/README.md)

## YDB (KiKiMR)

[База](https://ydb.yandex-team.ru/db/ydb-ru/maps-front-metro/production/metro-jams/browser)

Для приёма данных из `RTMR` и для дальнейших расчётов используются две таблицы, названия которых соответствуют кластерам, из которых в них пишутся данные:

| Name | URL |
|---|---|
| SAS | [YDB](https://ydb.yandex-team.ru/db/ydb-ru/maps-front-metro/production/metro-jams/browser/metro-people-count-analytics-sas) |
| VLA | [YDB](https://ydb.yandex-team.ru/db/ydb-ru/maps-front-metro/production/metro-jams/browser/metro-people-count-analytics-vla) |


## RTMR
Чтение данных производится из [Единого геолога](https://wiki.yandex-team.ru/geotargeting/geolocation-united-geolog/)

`YQL`-скрипты, которые выполняются на данных, полученных из `RTMR`, запускаются автоматически от пользователя
zomb-podrick@. Если нужно запустить их вручную, необходимо залогиниться под этим роботом.

Аккаунт, на который выделены ресурсы: `maps-front-metro`.

Как правило, график Delivery time должен выглядеть как можно более плавным. Количество дискардов
должно находиться в районе нескольких десятков (сотен), измеряется в байтах (это потерянные данные).

Главная страница `RTMR`

| Name | URL |
|---|---|
| SAS | [RTMR](https://rtmr.yandex-team.ru/production/accounts/maps-front-metro/overview?metricsFrom=1606167116465&location=sas) |
| VLA | [RTMR](https://rtmr.yandex-team.ru/production/accounts/maps-front-metro/overview?metricsFrom=1606167116465&locationFilter=vla&location=vla) |


## Solomon rtmr yf chart

Графики yf (https://wiki.yandex-team.ru/yf/).
Графики использования yf-фунций в YQL over RTMR.
Здесь можно увидеть потребление ресурсов, количество запущенных инстансов и статусы вызовов.
Call response error statuses должно быть в нуле.
`CPU`/`MEM`/`NET` usage должны быть ниже лимитов.

| Name | URL |
|---|---|
| SAS | [Solomon](https://solomon.yandex-team.ru/?project=yf&service=yf+functions&cluster=prod_sas&host=cluster&dashboard=yf-function-dashboard&l.version=Total&l.jobSetPath=yql_metro-jams&b=1h&e=) |
| VLA | [Solomon](https://solomon.yandex-team.ru/?project=yf&service=yf+functions&cluster=prod_vla&host=cluster&dashboard=yf-function-dashboard&l.version=Total&l.jobSetPath=yql_metro-jams&b=1h&e=) |

## S3
Файл с данными о пробках:
http://maps-front-static-int.s3.mds.yandex.net/maps/metro-jams/metro-jams.json
