# Yandex Direct API v5

Для того чтобы запустить сервис необходимо запустить метод `main` класса `YandexDirectApiV5Application`.

Для того, чтобы запустить сервис в заданном environment-е необходимо передать environment с помощью параметра `-Dyandex.environment.type=<environment>`
или переменной среды `YANDEX_ENVIRONMENT`. Список допустимых значений для environment-а можно посмотреть в классе `EnvironmentType`

Настройки сервиса расположены в `direct/libs-internal/config/src/main/resources`. Конфигурационный файл определяется environment-ом с которым запускается сервис

Для работы с сервисом AgencyClients с рабочего ноутбука возможно потребуется прокинуть порты до тестового паспорта и баланса.
Это можно сделать с помощью команды:

`ssh -fNTA -L 8001:passport-internal.yandex.ru:80 -L 8002:xmlrpc.balance.greed-ts.paysys.yandex-team.ru:8002 ppcdev5`

Также в таком случае необходимо запускать сервис с параметрами:

```
-Dpassport.internal.api.serviceUrl=http://localhost:8001
-Dbalance.serviceUrl=http://localhost:8002/xmlrpc
```

SOAP запросы посылать на http://localhost:8091/v5/

WSDL http://localhost:8091/v5/retargetinglists.wsdl

Можно сделать пробный запрос, с помощью `examples/send-test-request.sh`.

Oauth токен можно получить по ссылке https://oauth.yandex.ru/authorize?response_type=token&client_id=ae99016820074f809e5c268e564bebad
