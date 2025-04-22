# Отслеживание состояния приложения

<!-- toc -->

-   [Логи приложения](#%D0%BB%D0%BE%D0%B3%D0%B8-%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F)
    -   [Логи в интерфейсе Deploy](#%D0%BB%D0%BE%D0%B3%D0%B8-%D0%B2-%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81%D0%B5-deploy)
    -   [Логи Deploy в YT](#%D0%BB%D0%BE%D0%B3%D0%B8-deploy-%D0%B2-yt)

*   [Логи awacs балансировщика](#%D0%BB%D0%BE%D0%B3%D0%B8-awacs-%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B8%D1%80%D0%BE%D0%B2%D1%89%D0%B8%D0%BA%D0%B0)
    -   [Логи в ErrorBooster](#%D0%BB%D0%BE%D0%B3%D0%B8-%D0%B2-errorbooster)
    -   [Логи в CSP](#%D0%BB%D0%BE%D0%B3%D0%B8-%D0%B2-csp)
        -   [Сопоставление с Метрикой](#%D1%81%D0%BE%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D1%81-%D0%BC%D0%B5%D1%82%D1%80%D0%B8%D0%BA%D0%BE%D0%B9)
    *   [Мониторинги приложения](#%D0%BC%D0%BE%D0%BD%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%BD%D0%B3%D0%B8-%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F)
        -   [Telegram](#telegram)
        -   [Ping health](#ping-health)
        -   [Yasm Dashboard](#yasm-dashboard)
        -   [Основной Dashboard [WIP]](#%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D0%BE%D0%B9-dashboard-wip)
        -   [Yasm Frontend Static](#yasm-frontend-static)
        -   [Rum](#rum)
        -   [Логи на стендах (ферме)](#%D0%BB%D0%BE%D0%B3%D0%B8-%D0%BD%D0%B0-%D1%81%D1%82%D0%B5%D0%BD%D0%B4%D0%B0%D1%85-%D1%84%D0%B5%D1%80%D0%BC%D0%B5)
    *   [Алерты](#%D0%B0%D0%BB%D0%B5%D1%80%D1%82%D1%8B)

<!-- tocstop -->

## Логи приложения

Логи приложения на серверной стороне мы пишем при помощи [data-ui-logger](https://ui.yandex-team.ru/core/telemetry/logging).

Все логи приложения попадают в [Deploy](https://deploy.yandex-team.ru/stages/travel-frontend-portal-production/logs) и [поставляются](https://deploy.yandex-team.ru/docs/concepts/pod/sidecars/logs/logs#topic) в несколько кластеров YT:

1. YT-кластер [Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//logs/deploy-logs&:) (20 дней хранения)
2. YT-кластер [Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//logs/deploy-logs&:) (180 дней хранения)

Логи awacs балансировщика поставляются в YT

1. YT-кластер [Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/travel-production-awacs-access-logs) (30 дней хранения)

### Логи в интерфейсе Deploy

Логи приложения доступны в интерфейсе Y.Deploy (срок хранения 3 дня) на [вкладке "Logs"](https://deploy.yandex-team.ru/stages/travel-frontend-portal-production/logs) на странице стэйджа.
Доступны фильтры по уровню сообщения (DEBUG, INFO, WARNING, ERROR).
А также можно указать интервал времени для поиска.
В запросе можно указывать точное совпадение поля со значением, либо включение значения во множество.
Поиск по подстроке не доступен для всех полей кроме message, будет добавлен в Deploy в [тикете](https://st.yandex-team.ru/DEPLOY-4449).

Примеры запросов на разные жизненные ситуации:

1. Все запросы со статусом искать так (для api): `context.extra.status = 500, 502, 504`
2. Все запросы с конкретным url: `context.req.url=/hotels/permalink/1019041759/`
3. Все упавшие запросы: `message="request failure"`
4. Поиск по конкретному requestId: `context.req.id=5d0e37af0a489dc73e8e3983638e4b07`
5. Все запросы конкретного контроллера (AviaController): `context.extra.controller=AviaController; `
6. Все запросы конкретного метода(getSuggests) контроллера: `context.extra.action=getSuggests`

### Логи Deploy в YT

В [Yql](https://yql.yandex-team.ru/Operations/YW7UKBJKfRhUxrvlsCdOcMrumgb46bTVH5a4S9OYdNA=) также доступны логи приложения.

Пример запроса в Yql со следующими особенностями:

1. Используется кластер hahn, может быть arnold (отличия в сроке хранения)
2. Приведен пример парсинга Yson в строковые значения (requestUrl, requestId) и в числовые statusCode
3. Таблица взята с событиями за 2021-10-13, подставляйте нужную дату для поиска
4. Рассмотрен production stage портала travel-frontend-portal-production
5. События взяты за интервал от 2021-10-13 10:22:40 до 2021-10-13 10:32:40
6. Фильтр по результирующим полям из подзапроса по statusCode от 500 до 599 включительно

```
USE hahn;

SELECT * FROM
    (SELECT
        iso_eventtime,
        log_level,
        message,
        Yson::ConvertToString(Yson::YPath(Yson::Parse(context), "/req/url")) as requestUrl,
        Yson::ConvertToString(Yson::YPath(Yson::Parse(context), "/req/id")) as requestId,
        Yson::ConvertToInt64(Yson::YPath(Yson::Parse(context), "/extra/status")) as statusCode,
    FROM
        `logs/deploy-logs/1d/2021-10-13`
    WHERE
        stage='travel-frontend-portal-production' AND
        log_level = 'ERROR' AND
        iso_eventtime >= '2021-10-13 10:22:40' AND
        iso_eventtime <= '2021-10-13 10:32:40'
    )
WHERE statusCode >= 500 AND statusCode <= 599
```

Больше информации по составлению запросов можно найти в разделе [Tutorial](https://yql.yandex-team.ru).

# Логи awacs балансировщика

Для балансеров travel [настроена](https://testing.docs.yandex-team.ru/travel/ops/tools/awacs_logs) доставка логов до YT и ClickHouse.

Ссылка на Click House Viewer есть на [Дашборде][travel-health-dashboard] на вкладке "Сервер".

[Таблица в YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/travel-production-awacs-access-logs/1d)

Для поиска событий можно использовать [UI в ClickHouse Viewer](https://travel-production-awacs-access-log.chv.yandex-team.ru/items?filter=upstream%20%3D%3D%20portal-production%20AND%20status%20%3D%3D%20500&from=2021-10-19%2015%3A46%3A02&to=2021-10-19%2017%3A46%3A02)

Можно использовать [YQL](https://yql.yandex-team.ru/Operations/YW7eMtjKS6X7qzTcP5TS1SEcO5JlBZx_-5VdwznZwVg=) (new query in ClickHouse), для поиска в ClickHouse

```
USE travel_prod_log;

SELECT iso_eventtime, domain, request, headers, workflow, upstream, status from default.awacs_access_log
WHERE upstream = 'portal-production' AND status = 500
LIMIT 5;
```

[Описание полей](https://wiki.yandex-team.ru/users/nikshel/awacs-balancer-logs/#parserlogov)

### Логи в ErrorBooster

Все ошибочные состояния клиентского приложения доступны в [ErrorBooster](https://error.yandex-team.ru/projects/travel/projectDashboard).
Интерфейс позволяет устанавливать фильтры на определенные браузеры, домены, reqId и т.д.

#### Сопоставление с Метрикой

Периодически может возникать потребность сопоставить какие-то данные из [ErrorBooster](https://error.yandex-team.ru/projects/travel/projectDashboard)
с данными из [Яндекс Метрики](https://metrika.yandex.ru/dashboard?id=50912507). Например, в релизе возникает ошибка, и нужно
понять путь ее воспроизведения через просмотр сессий Вебвизора.

Для этого нужно:

1. Перейти на страницу ошибки в EB
2. Далее на вкладку `Users`
3. Вытаскиваем список `Yandexuid` пользователей.

    Если их много, можно воспользоваться хаком и скопировать всю таблицу
    в любой табличный редактор, например Google Sheets. После чего скопировать только данные из первого столбца.

4. Переходим в [Метрику](https://metrika.yandex.ru/stat/visor?period=month&id=50912507), например, на страницу Вебвизора
5. Ищем пользователей, которые нам интересны:

    В шапке добавляем условие `Визиты, в которых` → `Только для Яндекса` → `Идентификатор посетителя (uid)`
    и в textarea копируем `Yandexuid` из EB (по одному на строке). Жмем "Применить".

    [Скриншот](https://jing.yandex-team.ru/files/losyear/Screenshot%202022-02-15%20at%2016.29.28.png) для наглядности.

Аналогичным образом можно отфильтровать любой другой отчет в Метрике.

> N.B.: Подробнее о запросе доступа к метрике:
>
> -   Гайд на [Wiki](https://wiki.yandex-team.ru/jandexmetrika/managerdostup/#kakpoluchitdostupdljavneshnegologinanaschjotchikservisajandeksa)
> -   Пример роли на [IDM](https://idm.yandex-team.ru/system/metrika/roles#f-status=active,f-role=metrika,sort-by=-updated,role=46920837)

### Логи в CSP

CSP ошибки можно смотреть на https://csp.yandex-team.ru/projects/ya-travel/projectDashboard.
Например: можно смотреть ошибки загрузки фрейма траста - [график](https://csp.yandex-team.ru/projects/ya-travel/projectDashboard?filter=violatedDirective%20%3D%3D%20frame-src%20AND%20blockedUriHost%20%21%3D%20travel.farm.yandex-team.ru&period=week)

## Мониторинги приложения

### Telegram

В Telegram есть [канал](https://t.me/travel_frontend_alerts), куда приходят WARN и CRIT мониторингов. Клик на "График" отобразит текущий фон ошибок.

### Ping health

В Qloud настроен [JugglerCheck](https://platform.yandex-team.ru/projects/travel/front-next/production?tab=juggler) на проверку работоспособности приложения.
В Juggler на основе данных из Qloud настроено [уведомление](https://juggler.yandex-team.ru/notification_rules/?query=rule_id=5c1a35e8ef16250078986ad2), на основе которого при смене статусов приложения идут оповещения.

### Yasm Dashboard

В Голован вынесены основные [панели](https://yasm.yandex-team.ru/panel/_SL8zXL) из Qloud для быстрой оценки состояния приложения.

### Основной Dashboard [WIP]

Цель сделать один дэшборд на котором можно смотреть все наши приборы одновременно, не только графики Qloud, но и в том числе ErrorBooster, информацию из ClickHouse и так далее.

Для этого используется [дэшборд](https://dash.yandex-team.ru/huurcsd89uwse?state=6423dac5667) в сервисе Dash. Туда уже частино перенесены необходимые графики, и он будет дорабатываться в [задаче](https://st.yandex-team.ru/TRAVELFRONT-1558).

### Yasm Frontend Static

В Голован вынесены основные показатели по раздаче файлов статики S3: [S3Client](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=travel-frontend;owner=3513/), [S3Mds](https://yasm.yandex-team.ru/template/panel/s3_mds_nginx/bucket=travel-frontend).

### Rum

В Яндекс Статистике доступна [панель](https://stat.yandex-team.ru/Dashboard/Velocity/General?state=w8V8NfKiWddA) c временем загрузки сервиса. В выпадающем списке проектов необходимо выбрать Travel.

### Логи на стендах (ферме)

1. Заходим по ssh на фермовую тачку (сейчас `travel-farm2.sas.yp-c.yandex.net`)
2. Ищем процесс нужного стенда `sudo pm2 list`, запоминаем его id (второй столбик)
3. Смотрим `sudo pm2 logs <id>`

## Алерты

Информация об алертах можно посмотреть в документации [по алертам](./log-and-monitorings/alerts.md).

[travel-health-dashboard]: https://dash.yandex-team.ru/huurcsd89uwse
