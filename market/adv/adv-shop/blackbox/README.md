## Библиотека для подключения сервиса blackbox

1. ```BlackboxAutoconfiguration``` - автоконфигурация для подключения к сервису blackbox
   через ```ru.yandex.common.services.auth.blackbox.BlackboxService```.

## Подключение сервиса blackbox

1. Сделать в puncher дырки для прода и тестинга
   [(инструкция)](https://docs.yandex-team.ru/blackbox/concepts/getting-access#section_puncher)
2. Получить гранты [(инструкция)](https://docs.yandex-team.ru/blackbox/concepts/getting-access#section_grants)

3. Прописать в настройках приложения ```blackbox.url```. Для тестинга обычно
   это ```https://blackbox-test.yandex.net/blackbox```, для прода ```https://blackbox.yandex.net/blackbox```.

Весь перечень настроек проекта:
1. ```blackbox.url``` - ссылка на blackbox
2. ```blackbox.connectionTimeout``` - таймаут на соединение в мс, по умолчанию 2500.
3. ```blackbox.maxConnectionsPerRoute``` - максимальное число коннектов на маршрут, по умолчанию 200.
4. ```blackbox.maxConnectionsTotal``` - максимальное общее число коннектов, по умолчанию 400.
5. ```blackbox.connectionRequestTimeout``` - таймаут на ожидание свободного соединения из пула http-клиента в мс, по умолчанию 1500.
6. ```blackbox.socketTimeout``` - таймаут на ожидание ответа от сервера в мс, по умолчанию 20000.
7. ```blackbox.serviceUnavailableRetryCount``` - количество повторных попыток коннекта при недоступности сервиса, по умолчанию 2.
8. ```blackbox.serviceUnavailableRetryTimeout``` - таймаут повторных попыток коннекта при недоступности сервиса в мс, по умолчанию 5000.
9. ```blackbox.tvm.serverId``` - tvm id сервера. Если не задано, запрос будет без tvm-токена.
10. ```blackbox.tvm.clientId``` - tvm id клиента (blackbox). Если не задано, запрос будет без tvm-токена.
11. ```blackbox.tvm.secret``` - tvm секрет для создания токена. Если не задано, запрос будет без tvm-токена.
