# Логи nginx

## Логирование nginx
Можно смотреть логи на машинках сервиса.
1. Идём в [nanny](https://nanny.yandex-team.ru/ui/#/services) вашего сервиса
2. Копируем ssh урл пода
3. Заходим на машинку
4. Логи пишутся в /var/log/nginx/

{% cut "screen" %}

![](https://jing.yandex-team.ru/files/twin/nanny.png)

{% endcut %}

Access логи nginx так же пишутся в YT таблицу [taxi-access-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi-access-log) и хранятся 90 дней.

## Логи сервиса

### Клиентские логи
Для лога ошибок используем [error-counter](https://a.yandex-team.ru/arcadia/velocity/error-booster/error-counter).
Там же есть возможность создать алерты в juggler, например на всплеск новых ошибок. **Важно**: не следует использовать логер ошибок для логирования продуктовых метрик, для этого можно пользоваться Яндекс.Метрикой или [events](https://events.chv.yandex-team.ru) или выгрузкой в solomon.

Пример подключения error-counter в наших проектах:
* [init script](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/hiring-mass-frontend/src/client/index.html?rev=r9608626#L11), [logger](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/hiring-mass-frontend/src/client/shared/libs/error-logger.ts?rev=r9608626)
* [server](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/txf-family-frontend/server/middleware/render/rum/init.ts?rev=r9608626), [logger](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/txf-family-frontend/src/lib/logger.ts?rev=r9608626)

### Серверные логи

{% note warning %}

Всегда помни, что персональные данные (телефоны/авторизационные куки/токены) и секреты никогда не должны оседать в логах сервиса

{% endnote %}

#### в Кибану
_Срок хранение около 2х дней_

1. Складываем логи в формате tskv на файловую систему.
   Для логирование на сервере мы используем библиотеку [yandex-logger](https://a.yandex-team.ru/svn/trunk/arcadia/frontend/packages/yandex-logger), с кастомным [стримом](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/packages/frontend-common-server/src/utils/logger/index.js). Писать лог нужно в парку `/var/log/yandex/taxi-{service}/taxi.log`. **Важно** иметь в названии папки и файле слово taxi.
   Так же рекомендуется соблюдать единообразие в название полей лога
2. Настраиваем logrotate. Складываем конфиг в `/etc/logrotate.d/`
3. Смотрим логи в интерфейсы кибаны

Окружение | Хост
:--- | :---
testing | https://kibana.taxi.tst.yandex-team.ru
production |  https://kibana.taxi.yandex-team.ru

**Примеры в проектах**
taxifrontend:
* [Настройка логгера](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/utils/logger.js) + [syslog](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/common/server/utils/syslogStream.js)
* [конфиг syslog](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/yandex/etc/syslog-ng/conf-enabled/taxifrontend-taxi-frontend-yandex.conf)
* [конфиг logrotate](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/projects/yandex/etc/logrotate.d/taxifrontend-taxi-frontend-yandex)

mass-frontend
* [логгер](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/hiring-mass-frontend/src/server/shared/lib/logger.ts)

#### в YT
_Долгий срок хранение_

Если коротко, то схема выглядит так:
1. Создать топик в logbroker
2. Настроить логфеллер
3. Настроить push client сервиса

Подробно описано [здесь](https://wiki.yandex-team.ru/taxi-ito/logs-to-yt-dev/)

## Настройка логирования произвольных метрик/событий
### Лог метрик в Solomon
Для сбора произвольных событий отлично подходит [Solomon](https://solomon.yandex-team.ru). В дальнейшем можно, на основании этих данных, строить графики в сервисе [Яндекс.Мониториг](https://monitoring.yandex-team.ru/).

Пример:
[настройка в market-bo](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/market-bo/server/src/common/loggers/solomon.ts), [результат](https://monitoring.yandex-team.ru/projects/market-bo/dashboards/mon57m048eo58mt7u153?from=now-1w&to=now&refresh=60000)

### Выгрузка клиентских событий в events
Используется тот же [error-counter](https://a.yandex-team.ru/arcadia/velocity/error-booster/error-counter#otpravka-sobytiya).
Графики будут здесь: https://events.chv.yandex-team.ru