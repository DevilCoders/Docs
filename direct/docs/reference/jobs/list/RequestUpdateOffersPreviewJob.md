### Продукт/подсистема

Товарная реклама(Смарты, ДО, Фиды в ТГО).

### Роль в работе продукта/подсистемы

Запрашивает в Самоваре обновление офферных превью. Нужно для актуализации превью товаров для еком-доменов.

### Датафлоу

Джоба раз в сутки берет хосты из таблички `ppcdict.ecom_domains` c устаревшим превью, у которых `last_modified_preview`
уже старше, чем заданное время (время берётся в часах из property `offers_preview_expiration_hours`)
и отправляет запрос на перепрокачку в LB топик самовара в формате
[внешнего фида](https://wiki.yandex-team.ru/robot/samovar/feedsext/).


### Способы наблюдения за текущим состоянием

- [Логи](https://direct.yandex.ru/logviewer/short/vFt7ru6a4hDH59)
- Количество доменов с актуальными превью можно отследить на [графике](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs-push&service=push-monitoring&l.flow=EcomDomainStatusesMonitoringJob&l.env=production&l.host=CLUSTER&graph=auto&stack=false&downsamplingFill=none&secondaryGraphMode=bars&b=36d&e=)
- [График запросов на перепрокачку](https://solomon.yandex-team.ru/?project=samovar&cluster=primary-arnold&service=samovar_combustor_url&l.host=cluster&l.path=%2FCombustorPublicCounters%2FFeedsPushed%2FCount&l.Feed=check-host-for-smart-preview-ext&graph=auto&b=8d&e=)


### Какая функциональность пострадает от отказа джобы

У клиентов не будут обновляться превью офферов на сайте.

### Как пользователи (или команда) заметят проблему и через какое время

Возможны жалобы на устаревшие данные там, где используются превью (например, в мастере кампаний).

### Контакты разработчиков и менеджеров

Разработчики: [kozobrodov](https://staff.yandex-team.ru/kozobrodov) <br/>
Менеджеры: [ulyashevda](https://staff.yandex-team.ru/ulyashevda)


### Желательное время исправления в случае поломки

В течение суток.

### Способы регулирования работы джобы

Через свойства можно:
- Включить или выключить джоб (свойство `update_offers_preview_job_enabled`)
- Отрегулировать время устаревания превью (свойство `offers_preview_expiration_hours`)
- Отрегулировать интенсивность отправки сообщений в LB топик Самовара:
  - Свойство `update_offers_preview_sending_chunk_size` позволяет выставить размер чанка отправки
  - Свойство `update_offers_preview_sleep_coef` указывает коэффициент времени сна при отправке

В коде можно изменить размер чанка выборки доменов из YT (см. константу `DOMAINS_CHUNK_SIZE`).
