## remctl
Скрипт для генерации запросов, получает внутри себя сервисный тикет и делает [запрос](https://a.yandex-team.ru/arc/trunk/arcadia/mail/callmeback/callmeback/swagger/schema.yaml?rev=r9010153) к callmeback. Для работы обязателен работающий ```tvmknife get_service_ticket sshkey```
#### Аргументы
##### Опциональные
* **--reminder_id**:
    Часть основного запроса
* **--config**:
    Путь к основному конфигу сендбернара, откуда будет доставаться ```callmeback_url``` и ```tvm_id``` сендбернара, по умолчанию берет ```/etc/sendbernar/sendbernar.yml```
* **--tvm_file**:
    Путь к файлу с ```tvm_id сендбернара```, по умолчанию берет ```/tvm2_root_client_id```
* **--tvm_id**:
    Дает возможность задать изначальный ```tvm_id``` сендбернара без обращения в файл
* **--callmeback_cfg_path**:
    Принимает путь вида ```configuration.send.reminders``` для получения ```callmeback_url``` из конфига, позволяет модифицировать путь из [модуля сендбернара](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sendbernar/etc/sendbernar.yml?rev=r9072172#L440), по умолчанию берет ```configuration.send.reminders.client_configuration.add.url```
##### Обязательные
* **--action**:
    Часть основного запроса, при получении ```get``` генерируется ```GET``` запрос вида ```{callmeback_url}/v1/event/{uid}/{reminder_id}```, иначе ```POST``` запрос вида
    ```{callmeback_url}/v1/event/{action}/{uid}/{reminder_id}```
* **--uid**:
    Часть основного запроса
##### Примеры
* **Call**: ```./remctl --action get --uid 4083370853 --reminder_id 8```\
**Generated url**: ```https://callmeback-test.mail.yandex.net/v1/event/4083370853/8```
* **Call**: ```./remctl --action get --uid 4083370853 --callmeback_cfg_path configuration.send.reminders.client_configuration.cancel.url```\
**Generated url**: ```https://callmeback-test.mail.yandex.net/v1/event/4083370853```
* **Call**: ```./remctl --action delete --uid 4083370853 --reminder_id 8```\
**Generated url**: ```https://callmeback-test.mail.yandex.net/v1/event/delete/4083370853/8```
