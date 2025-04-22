# How it works?
## Как устроен релизный цикл? {#release-cycle}
* Для **WEB** вертикали запущен [CI Flow](https://arcanum.yandex-team.ru/projects/upper/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast&id=fast-data-web-release). Собирает данные [BuildRearrangeDataFast](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/BuildRearrangeDataFast), тестирует их через [TestRearrangeDataFast](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/TestRearrangeDataFast) и YA_MAKE тесты, деплоит [DeployFastData](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/DeployFastData).
* Для **VIDEO** вертикали запущен [CI Flow](https://arcanum.yandex-team.ru/projects/noapache-video/ci/releases/timeline?dir=search%2Fweb%2Frearrs_upper%2Frearrange.fast%2Fci%2FVIDEO&id=fast-data-release). Цикл аналогичен вебовскому.

## Как быстрые данные тестируются перед релизом? {#release-tests}
* Тестирование производится задачей [TestRearrangeDataFast](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/TestRearrangeDataFast).
* Задача умеет запускать три типа тестов:
    * [аркадийные юнит-тесты](http://a.yandex-team.ru/arc/trunk/arcadia/search/web/rearrs_upper/tests/rearrange.fast)
    * поднятие ноапача с новыми данными, обстрел инстанса grpc_client-ом планом из 1000 запросов
    * выкладка данных на бету, обстрел инстансов беты grpc_client-ом планом из 1000 запросов

## Как происходит деплой? {#release-deploy}
* Процесс запускается задачей [DeployFastData](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/DeployFastData).
* Деплой работает в связке deployer+bstr push. Deployer руководит процессом развертывания данных на инстансах: он получает на вход конфиг со списком nanny-сервисов и rbtorrent с архивом быстрых данных, далее в рамках одного ДЦ (в порядке SAS, MAN, VLA) идет окошком по инстансам и отправляет им сигнал о релизе новых данных с помощью bstr push. Со стороны инстанса работает связка bstr pull+Callback. Первый из них получает сигнал о новых данных, скачивает их и передает на вход Callback'у, тот в свою очередь распаковывает, подкалыдывает данные ноапачу и сообщает ему о необходимости перезагрузить данные, а тот их перезагружает. Еще один демон в фоне периодически проверяет версию данных под ноапачем, опрашивая инстанс по ручке `/yandsearch?info=get_rearrange_version`, и пишет эту версию в документ на YT. Как только версия, записанная в документ в YT, совпала с выкладываемой версией, Deployer считает, что выкладка на этот инстанс произошла успешно.

## Где что лежит? {#where-is}
* Документы в YT, через которые происходит общение [locke://home/search-runtime/fast-data](https://yt.yandex-team.ru/locke/?page=navigation&path=//home/search-runtime/fast-data)
* Код быстрых данных: [search/web/core/fast_data](https://a.yandex-team.ru/arc/trunk/arcadia/search/web/core/fast_data)
* Директория с описанием CI релизов: [search/web/rearrs_upper/rearrange.fast/ci](https://arcanum.yandex-team.ru/arcadia/search/web/rearrs_upper/rearrange.fast/ci)
* Обновление данных во всех правилах: [TWebRearrange::LoadFastData](https://a.yandex-team.ru/arc//trunk/arcadia/search/web/core/rearrange.cpp)
* [Codesearch по (Re)LoadFastData](https://cs.yandex-team.ru/#!%5BLl%5DoadFastData,%5Esearch,,arcadia)
* bstr: [tools/bstr](https://a.yandex-team.ru/arc/trunk/arcadia/tools/bstr)
* Callback для bstr: [search/tools/fast_data_deployment/callback](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/fast_data_deployment/callback)
* Deployer: [search/tools/fast_data_deployment/deployer](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/fast_data_deployment/deployer)

## Sandbox задачи {#sandbox-tasks}
* Сборка: [sandbox/projects/websearch/upper/fast_data/BuildRearrangeDataFast](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/BuildRearrangeDataFast)
* Тестирование: [sandbox/projects/websearch/upper/fast_data/TestRearrangeDataFast](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/TestRearrangeDataFast)
* Деплой: [sandbox/projects/websearch/upper/fast_data/DeployFastData](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/DeployFastData)
* [для Sandbox шедулеров (deprecated)] Релиз: [sandbox/projects/websearch/upper/fast_data/ReleaseRearrangeDataFast](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/upper/fast_data/ReleaseRearrangeDataFast)
