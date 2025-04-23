# auto.ru catalog-api #

Сервис для работы с каталогом автору
По всем вопросам писать в чат https://t.me/joinchat/BKuv7xbGFRLaoe4nhGL5Yg

## Адреса ##

Девелопмент: http://dev-autoru-catalog-api-int.vrts-slb.test.vertis.yandex.net

Тестинг: http://autoru-catalog-api-int.vrts-slb.test.vertis.yandex.net

Тестинг из бранчи: http://pull-???.autoru-catalog-api-int.vrts-slb.test.vertis.yandex.net

Продакшн: TBD

### Локальный запуск

Запустить в IDEA класс `ru.auto.api.Main`
Либо в консоли: `make start`

### Деплой на dev сервер

Вписать адрес dev-машины в `upload.properties` в параметр `ssh.host`.
Пример: `ssh.host=my-dev-host.net`

Команда `make deploy` компилирует проект, заливает на сервер и перезапускает приложение.

Следы работы приложения можно найти в папке `~/dist/catalog-api/`на dev машине.

### Деплой в тестинг 

Запускаем ТС джобу для ветки мастер [тут]( https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_AutoruCatalog_Release)

Сборка для тестинга в дженкинсе запустится автоматически

### Деплой в прод

В дженкисе находим последний успешный тестовый билд ([например](https://j.vertis.yandex-team.ru/job/Deploys/job/Autoru/job/testing/job/autoru-catalog-api/78/promotion/))  и жмем на кнопку force to promotion 
