# Алерты в juggler

## Другие источники знаний о проверках

- ссылки в описании проверки (под "Детали проверки" в интерфейсе Juggler)
- ссылки в meta.url (кликабельные ссылки справа вверху на странице проверки в Juggler)
- описания в Соломоне, если проверка генерируется по Соломоновскому алерту

## Проверки { #checks }

{% note tip "Куда добавить новую проверку?" %}

1. Скопируйте шаблон описания [`example.md`](https://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/reference/alerts/example.md)
в новый файл в папке [reference/alerts](https://a.yandex-team.ru/arc/trunk/arcadia/direct/docs/reference/alerts)
   (если в имени нужно разделить несколько слов — используйте дефис, а не подчеркивание)
1. Заполните разделы страницы, удалите лишние, удалите шаблонный текст.
1. Поставьте ссылку на новую страницу в `toc.yaml`, в раздел **Справочник** → **Эксплуатация** → **Juggler проверки**.
1. Добавьте проверку в одну из подходящих по смыслу таблиц ниже. Если непонятно — добавляйте в [Разное](#unsorted). В таблице используйте максимально полное название проверки

{% endnote %}

### Общие проверки { #common }
Относятся ко многим и разным сущностям.
Обычно про наливку, настройку, дырки и другие подготовительные вещи.

Проверка | Описание
:--- | :---
[ready_for_operation](../../reference/alerts/ready-for-operation.md) | готовность машины к работе
[yandex-ansible-pull](../../reference/alerts/yandex-ansible-pull.md) | успешность работы нашей _преднастройки_

### Базы данных { #database }
Проверка | Описание
:--- | :---
[downtime-db.\*](../../reference/alerts/downtime-db.md) | мастер базы попадает под плановые регламентные работы
[threads_connected\*](../../reference/alerts/mysql-threads-connected.md) | утилизация пула подключений к базе
[threads_running\*](../../reference/alerts/mysql-threads-running.md) | количество активных тредов
[geo_position_master\*](../../reference/alerts/geo-position-master.md) | определение местоположения мастера
[mysql_slow_io](../../reference/alerts/mysql-slow-io.md) | деградация дискового IO
[mysql_trx_max_age](../../reference/alerts/mysql-trx-max-age.md) | наличие долгих транзакций
[can_failover.\*](https://st.yandex-team.ru/DIRECTADMIN-8963#5f994dc93316147cd4e3557e) | готовность к автофейловеру
[ppcdata](../../reference/alerts/ppcdata_availability.md) | доступность базы `ppc`
[ppcdict](../../reference/alerts/ppcdict_availability.md) | доступность базы `ppcdict`

### Ресурсы { #resources }
Проверка | Описание
:--- | :---
[logbroker-write-quota](../../reference/alerts/logbroker-write-quota.md) | использование квоты на запись (мб/с) в логброкер, продакшн процессы
[logbroker-write-quota-np](../../reference/alerts/logbroker-write-quota.md) | использование квоты на запись (мб/с) в логброкер, непродакшн

### Продуктовые { #product }
Мониторинги по продуктовой функциональности.

Проверка | Описание
:--- | :---
[balance-notifyOrder-2xx](../../reference/alerts/balance-notify-order-2xx.md) | наличие успешных нотификаций Баланса о зачислениях
[balance-notifyOrder-5xx](../../reference/alerts/balance-notify-order-5xx.md) | ошибки при приеме нотификаций Баланса
[dsp-creative-export-alive](../../reference/alerts/dsp-creative-export-alive.md) | транспорт креативов Директа в БК (выгрузка в YT)
[jobs.ActiveOrdersImportJob.working.production](../../reference/alerts/active-orders-import-job.md) | обновление в Директе сумм истраченного на заказах
[trending-errors-\*](../../reference/alerts/trending-errors.md) | всплески ошибок в бекендах

### Экспорт в БК, старый { #perl-bsexport }
Проверка | Описание
:--- | :---
[logbroker_request_fails](../../reference/alerts/bs-export-logbroker-request-fails.md) | проблемы при отправке в логброкер
[queue_std.delayed_clients_count](../../reference/alerts/bs-export-delayed-clients-std.md) | число клиентов с задержкой выше SLA
[queue_std.age_minutes](../../reference/alerts/bs-export-queue-age-std.md) | средний/максимальный возраст кампаний в очереди (относительно SLA)
[other_queues_age](../../reference/alerts/bs-export-other-queues-age.md) | возраст кампаний в других очередях
[queue_buggy.campaigns_count](../../reference/alerts/bs-export-buggy-campaigns-count.md) | число кампаний в buggy очереди

### Экспорт на модерацию, старый  { #perl-moderation }
Проверка | Описание
:--- | :---
[scripts.moderateExportMaster.working](../../reference/alerts/scripts-moderate-export-master-working.md) | постановка в очередь объектов готовых к отправке

### Экспорт на модерацию, новый  { #ess-moderation }

Проверка | Описание
:--- | :---
[send-ess-moderation-metrics](../../reference/alerts/send-ess-moderation-metrics.md) | ошибки отправки метрик модерации в соломон

### Взаимодействие с Метрикой { #metrika }
Проверка | Описание
:--- | :---
[metrika_requests_server_errors](../../reference/alerts/metrika-requests-server-errors.md) | ошибки при запросах в Метрику

### Фронтенд { #frontend }
Проверка | Описание
:--- | :---
[direct_DNA_uncaught](../../reference/alerts/direct-dna-uncaught.md) | исключения при работе фронта
[\*First](../../reference/alerts/frontend-timings-all-first-timings.md) | замедление рендеринга страниц
[frontend-errors-\*](../../reference/alerts/frontend-errors.md) | всплески ошибок на фронте
[lc-turbo-json-response-time](../../reference/alerts/lc-turbo-json-response-time.md) | время отдачи опубликованных страниц Турбо-конструктора
[lpc-direct-api-submissions-send-errors-count](../../reference/alerts/lpc-direct-api-submissions-send-errors-count.md) | проблемы с отправкой писем с заявками, которые клиенты оставляют на странице Турбо-сайтов

### Разное { #unsorted }

Алерты без обобщения и категоризации.
Проверка | Описание
:--- | :---
[slb-yp_consistency](../../reference/alerts/slb-yp-consistency.md) | конфигурация балансера указывает на актуальные IP-адреса YP-контейнеров
[шаблон описания](../../reference/alerts/example.md) | страничка — шаблон описания для проверки


## Специальные (синтетические) хосты { #special-synthetic-hosts }

### direct.prod_apps-health

Хост для агрегированных health-[проверок](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Ddirect.prod%26host%3Ddirect.prod_apps-health) по [приложениям Директа](../../glossary/glossary#apps-conf).


### direct.prod_subsystems

Хост для агрегированных health-[проверок](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Ddirect.prod%26host%3Ddirect.prod_subsystems) по [подсистемам Директа](../../glossary/glossary#subsistems-list).


### direct.prod_backing-services

Хост для агрегированных health-[проверок](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Ddirect.prod%26host%3Ddirect.prod_backing-services) по [смежным сервисам](../../glossary/glossary.md#backing-services-list).


### checks_auto_aggregation.direct.yandex.ru

Хост для промежуточных (например одного шарда), автоматически создаваемых мониторингов джобов и перловых скриптов.

Не предполагает уведомлений людям о срабатываниях.

### checks_auto.direct.yandex.ru

Хост для автоматически создаваемых (из кода) проверок на живость перловых скриптов и java-джобов.

