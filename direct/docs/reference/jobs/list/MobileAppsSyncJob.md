## MobileAppsSyncJob

### Продукт/подсистема

Подсистема получения информации о мобильных приложениях, в основном для РМП кампаний (Реклама мобильных приложений).


### Роль в работе продукта/подсистемы

Выгрузка данных о мобильных приложениях из статических таблиц Авроры в динамические таблицы Директа, к которым уже обращаются процессы Директа.

В эти динамические таблицы ходят:
- [UpdateStoreContentJob](UpdateStoreContentJob.md) для обновления информации о мобильных приложениях в [ppc.mobile_content](https://direct-dev.yandex-team.ru/db/ppc/tables/mobile_content.html).
- `java-web` и `java-intapi` в процессе добавления приложений в интерфейсе.


### Датафлоу

- Аврора обходит, парсит сторы (Google Play, Apple Store), и создаёт набор статических таблиц с сырой информацией по приложению: [hahn.//home/extdata/mobile/google_play/latest/*](https://yt.yandex-team.ru/hahn/navigation?path=//home/extdata/mobile/google_play/latest), [hahn.//home/extdata/mobile/itunes/latest/*](https://yt.yandex-team.ru/hahn/navigation?path=//home/extdata/mobile/itunes/latest). Эти таблицы используются как входные данные для `MobileAppsSyncJob` и указаны в [app-production.conf приложения jobs](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) в секции `mobile_apps_data` для каждого стора - [MobileContentStoreType](https://a.yandex-team.ru/arc/trunk/arcadia/direct/common/src/main/java/ru/yandex/direct/common/mobilecontent/MobileContentStoreType.java])

- Джоба проверяет, требуется ли обновление данных, сравнивая атрибуты `modification_time` входных таблиц и `creation_time` выходных.
- Запускает YQL, которые записывают результат во временные таблицы в YT.
- Далее джоба с помощью API TransferManager генерирует динамические таблицы в нескольких кластерах. Актуальная информация о таблицах и кластерах находится в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf) в секции `mobile_content_data` для каждого стора - [MobileContentStoreType](https://a.yandex-team.ru/arc/trunk/arcadia/direct/common/src/main/java/ru/yandex/direct/common/mobilecontent/MobileContentStoreType.java]).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.MobileAppsSyncJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'mobileappssync.MobileAppsSyncJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Не будет обновляться информация о приложениях, доступная другим частям Директа.


### Как пользователи (или команда) заметят проблему и через какое время

- Жалобы пользователей на отсутствие информации при добавления новых (добавленных в сторы после поломки джобы) мобильных приложений.
- Показ объявлений приложений, которые уже удалены со сторов?
- Старые данные в объявлениях: рейтинг, иконка? (сейчас вроде строится прямой канал Аврора -> CaeSaR)


### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Игорь Гердлер](https://staff.yandex-team.ru/gerdler)


### Желательное время исправления в случае поломки

1-2 дня


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни
