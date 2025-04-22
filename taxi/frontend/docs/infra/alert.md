# Алерты и мониторинги сервиса

Данный раздел рассматривает системы диагностики и мониторинга работоспособности сервиса.

- [Чат группы диагностики](https://nda.ya.ru/t/ePhVLReX4jWesx)
- [wiki](https://wiki.yandex-team.ru/taxi/backend/hejmdal/alert-manager/unified-recipients/)

## Дефолтные мониторинги

По дефолту у сервиса в RTC есть набор мониторингов и алерты на 500 ошибки от балансера или например на превышение ресурсов CPU/MEM/DISK.
Наиболее полезная для нас и чаще всего встречающаяся это именно проверка на 5** `vhost500`.

Найти проверки можно в разделе "[Диагностика сервисов](https://tariff-editor.taxi.yandex-team.ru/hejmdal-diagnostics/)"

## Проверки от juggler

В дефолтный мониторинг на 500 попадают лишь результаты на которые есть трафик. Представим, что у вас есть раздел в сервисе, на котором почти не бывает трафика, но он критичный для бизнеса (например всякие юридические документы).

Есть возможность настроить мониторинг, который будет по cron таскам опрашивать эти страницы и проверять ответы (хоть код ответа, хоть тело ответа).

Есть два типа проверок: 
- **Пассивные** – ваш cкрипт мониторинга на хосте вычисляет статус и посылает его (сырые события) системе мониторинга; 
- **Активные** – система мониторинга самостоятельно предпринимает какие-то действия для мониторинга (посылает ping, опрашивает graphite, проверяет доступность http и т.п.).

Удобней использовать пассивную проверку, т.к. скрипт проверки можно хранить и генерировать непосредственно в коде вашего проекта.

1. Пишем скрипт, который будет опрашивать нужные вам урлы сервиса
2. Пишем конфиг для juggler-client aka monrun
3. Описываем правила агрегации

[Подробней](https://wiki.yandex-team.ru/taxi-ito/juggler-generator/#kakdobavitpassivnyjjmonitoring)

Пример реализации в сервисе:
1. Скрипт проверки [тут](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/libs/monitoring/check-taxi-frontend.js?rev=r9303241)
2. Конфиг для juggler-client [тут](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend/libs/monitoring/check-taxi-frontend-yandex.conf?rev=r9303241) 
3. Правила агрегации [тут](https://a.yandex-team.ru/arcadia/taxi/infra/infra-cfg-juggler/checks/taxi.front.prod/rtc_taxi_taxi-frontend-yandex_stable?rev=r9789474#L14)
4. Настройка деплоя [конфига](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend-taxi-frontend-yandex/docker/Dockerfile?rev=r9303241#L17) и [скрипта](https://a.yandex-team.ru/svn/trunk/arcadia/taxi/frontend/services/taxifrontend-taxi-frontend-yandex/docker/Dockerfile?rev=r9303241#L49)

## Произвольные алерты

Есть возможность настроить алерты по данным от соломона, например вы хотите считать uptime вашего сервиса и получать алерты, если он ниже порогового значения. 

[Теория](https://wiki.yandex-team.ru/taxi-ito/solomonalerts/).

Для этого есть удобный инструмент [в админке](https://tariff-editor.taxi.yandex-team.ru/custom-checks/).

1. Выбираем ваш сервис
2. Добавляем новую проверку
3. Указываем данные для проверок.

[Подробней](https://wiki.yandex-team.ru/taxi/backend/hejmdal/customchecks/).

Пример проверки на uptime сервиса истории заказов - [здесь](https://tariff-editor.taxi.yandex-team.ru/custom-checks/show/12)

## Алерты на клиентские ошибки

Если у вас подключен error-counter для клиентских ошибок, то он позволяет настроить алерты через juggler.

1. Идём в раздел Alerts в настройках вашего сервиса
2. Добавляем новые алерт: существует 4 вида алерта. 
Подробней [здесь](https://docs.yandex-team.ru/error-booster/alerts/)

так же удобно создать фильтр именно на продакшен + исключая теги muted
`environment == production AND errorTags notIn muted`

Пример алерта [здесь](https://error.yandex-team.ru/projects/supchat-frontend/settings/alerts)