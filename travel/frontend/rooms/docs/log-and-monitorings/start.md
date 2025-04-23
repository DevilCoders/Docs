# Краткое руководство по настройке мониторингов и оповещений

В данном руководстве представлено краткое описание, последовательность действий и особенности
по настройке системы мониторинга, позволяющей отслеживать состояние сервиса и
отправлять нотификации при переходе количественных характеристик приложения за заданные пределы.

## Введение

Механизм смены статуса(OK, WARN, CRIT) проверки с последующей отправкой нотификаций можно представить примерно следующей цепочкой:

1. Источник данных отвечает за поставку предагрегированных метрик приложения за определенный временной промежуток.
2. Система количественного мониторинга отвечает за обработку сигналов и смену статуса проверки.
3. Система событийного мониторинга и оповещений отвечает за отправку нотификаций пользователям, подписанных на переходы статусов проверки в заданные состояния.

### Источники сигналов

При использовании [Solomon](https://wiki.yandex-team.ru/solomon/) или [Golovan](https://wiki.yandex-team.ru/golovan/) есть два способа доставки метрик:

-   Pull-схема сбора данных - агент собирает метрики приложения с определенной периодичностью.
-   Push-схема сбора данных - приложение самостоятельно отправляет метрики агенту.

Добавлять [stat-handle](https://wiki.yandex-team.ru/golovan/userdocs/stat-handle/?from=%2Fgolovan%2Fstat-handle%2F) в приложение стоит в том случае, если необходимо отслеживать специфические или рассчитываемые внутри сервиса показания.

Когда возникнает необходимость отправлять метрики приложения в особые моменты времени, то стоит воспользоваться [push api.](https://wiki.yandex-team.ru/golovan/userdocs/push-api/?from=%2Fgolovan%2Fpush-api%2F)

Инфраструктура Qloud за счет [qloud-init](https://wiki.yandex-team.ru/qloud/doc/qloud-init/), [yasmagent](https://wiki.yandex-team.ru/golovan/dev/components/yasmagent/subagent/?from=%2Fgolovan%2Fyasmagent%2Fsubagent%2F)
и других процессов платформы обеспечивает отправку всех основных метрик сервиса каждые 5 секунд как по qloud-router параметрам(rps, 5xx, 4xx, response time и другие), так и по [ресурсам внутри porto контейнера.](https://wiki.yandex-team.ru/porto/)

### Системы количественного мониторинга

`Solomon и Golovan — системы количественного мониторинга, позволяющие отслеживать программные и аппаратные характеристики сервисов в режиме реального времени и отвечающие за сбор, агрегацию, хранение и визуализация метрик с возможностью оповещения через Email, SMS, Telegram, Yandex.Messenger, Webhook и Juggler.`

Основные возможности Golovan:

-   [Различные способы агрегации сигналов.](https://wiki.yandex-team.ru/golovan/userdocs/aggregation-types/)
-   [Использование встроенных функций для работы с сигналами.](https://wiki.yandex-team.ru/golovan/userdocs/signal-functions/?from=%2Fgolovan%2Fsignal-functions%2F)
-   [Создание панелей и объединение их в дашборды.](https://wiki.yandex-team.ru/golovan/userdocs/panels/)
-   [Создание пороговых и трендовых алертов, настройка флаподава.](https://wiki.yandex-team.ru/golovan/userdocs/alerts/ui/?from=%2Fgolovan%2Falerts%2Fui%2F)

Основной информационной единицой Golovan является [`сигнал`](https://wiki.yandex-team.ru/golovan/userdocs/terminology/#xosty).

Ключевые характеристики сигнала:

-   Название сигнала(signal), например: `unistat-auto_disk_ephemeral_usage_bytes_axxx`, `push-http_400_summ`, `portoinst-net_mb_summ`.
-   Тип сигнала(itype), например: `qloudrouter`, `qloud`.
-   Проект источника(prj), например: `travel.front-next.production`, `travel.front-next.prestable`.
-   Хост источника(hosts), например: `qloud`.

Полезные ссылки:

-   [Веб интерфейс Solomon](https://solomon.yandex-team.ru/)
-   [Подробная документация Solomon](https://wiki.yandex-team.ru/solomon/)
-   [Веб интерфейс Golovan](https://yasm.yandex-team.ru/)
-   [Подробная документация Golovan](https://wiki.yandex-team.ru/golovan/)

### Система событийного мониторинга и отправки нотификаций

`Juggler - система событийного мониторинга, которая умеет принимать события с различных клиентов, агрегировать их по заданным правилам и отправлять результат через SMS, Email, Telegram или инициировать звонок ответственному дежурному.`

При настройке нотификаций удобно завести специальный alert telegram чат и пригласить туда [JugglerSearchBot](https://telegram.me/JugglerSearchBot).

Пример сообщений от JugglerSearchBot:

![juggler_search_bot](images/juggler_search_bot.png)

![juggler_search_bot_chart](images/juggler_search_bot_chart.png)

Если дежурства заведены через ABC, то стоит подписать дежурных на оповещения, например: `@svc_portalvteam:travel_portal_duty`, `@svc_portalvteam:travel_portal_duty_reserve`.

Для наиболее важных проверок стоит настроить [звонковую эскалацию.](https://docs.yandex-team.ru/juggler/notifications/escalations)

Для группировки оповещений нужно использовать теги и namespace вашего сервиса.

Полезные ссылки:

-   [Веб интерфейс Juggler](https://juggler.yandex-team.ru/)
-   [Нотификации Juggler](https://docs.yandex-team.ru/juggler/notifications/on_change)
-   [Подробная документация Juggler](https://docs.yandex-team.ru/juggler/)

## Базовые мониторинги

В данном разделе представлена настройка базовых мониторингов для отслеживания наиболее важных характеристик приложения.

### Health-check в Qloud

Проверка сервиса на предмет "живучести" путем постоянного пинга предварительно настроенного роута.

Последовательность действий по созданию проверки в интерфейсе Qloud можно найти в [документации.](https://wiki.yandex-team.ru/qloud/doc/environment/monitors/)

Подробный разбор параметров проверки можно найти в разделе [jugglerhelp.](https://wiki.yandex-team.ru/qloud/doc/environment/monitors/jugglerhelp/)

> Достаточно удобно заводить все настройки нотификаций в Juggler. В данном случае можно пропустить добавление нотификаций в табике "Juggler" в Qloud и воспользоваться интерфейсом Juggler. Это позволит добавлять и редактировать все оповещения сервиса в одном месте.

Панель нотификаций на табике "Juggler" в Qloud можно оставить пустой:

![health_check_qloud_notification](images/health_check_qloud_notification.png)

Пример конфигурации оповещений при смене статуса проверки "health-check" в Juggler:

![health_check_sms_telegram](images/health_check_sms_telegram.png)

Пример конфигурации звонковой эскалации при переходе в статус CRIT проверки "health-check" в Juggler:

![health_check_escalation](images/health_check_escalation.png)

### Qloud-router метрики

Проверка сервиса на предмет роста rps, 5xx, 4xx, response time и других показателей qloud-router.

Последовательность действий по созданию проверки в интерфейсе Golovan можно найти в [документации.](https://wiki.yandex-team.ru/golovan/userdocs/alerts/ui/?from=%2Fgolovan%2Falerts%2Fui%2F)

Перед созданием алерта необходимо сформировать основные параметры сигнала:

-   `hosts=QLOUD;`
-   `itype: qloudrouter;`
-   `signals=(push-response_xxx_summ или push-http_xxx_summ);`
-   `prj=(название проекта в Qloud);`

Для подготовки и преобразования сигналов можно использовать [встроенные функции.](https://wiki.yandex-team.ru/golovan/userdocs/signal-functions/?from=%2Fgolovan%2Fsignal-functions%2F)

Важно создать свой namespace и не пользоваться коммунальным!

> Достаточно удобно заводить все настройки нотификаций в Juggler. В данном случае можно пропустить добавление нотификаций на табике "Уведомления" в Golovan и воспользоваться интерфейсом Juggler. Это позволит добавлять и редактировать все оповещения сервиса в одном месте.

Панель нотификаций на табике "Уведомления" в Golovan можно оставить пустой:

![yasm_qloud_router_notification](images/yasm_qloud_router_notification.png)

Пример конфигурации оповещений при смене статуса проверки "push-http_400_summ" в Juggler:

![qloud_router_telegram](images/qloud_router_telegram.png)

### Porto-контейнер и qloud-init метрики

Проверка сервиса на предмет роста потребления ресурсов(CPU, Memory, Network и другие показатели).

Последовательность действий по созданию проверки в интерфейсе Golovan можно найти в [документации.](https://wiki.yandex-team.ru/golovan/userdocs/alerts/ui/?from=%2Fgolovan%2Falerts%2Fui%2F)

Подробнее о атрибутах Porto-контейнера можно ознакомиться в [документации.](https://wiki.yandex-team.ru/porto/)

Перед созданием алерта необходимо сформировать основные параметры сигнала:

-   `hosts=QLOUD;`
-   `itype: qloud;`
-   `signals=(conv(unistat-auto_disk_ephemeral_usage_bytes_axxx, Gi), portoinst-cpu_usage_cores_tmmv или portoinst-net_mb_summ и другие);`
-   `prj=(название проекта в Qloud);`

Панель нотификаций на табике "Уведомления" в Golovan можно оставить пустой:

![yasm_network_notification](images/yasm_network_notification.png)

Пример конфигурации оповещений при смене статуса проверки "network_usage" в Juggler:

![juggler_network](images/juggler_network.png)

## Дальнейшие шаги по улучшению

-   Примеры с Deploy и постепенный уход от Qloud.
-   Примеры с Solomon и постепенный уход от Golovan.
-   Проработка таймингов для health-check и звонковой эскалации.
-   Настройка оповещений на квоту s3 через диспенсер.
