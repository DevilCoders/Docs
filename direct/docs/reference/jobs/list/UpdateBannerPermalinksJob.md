##  UpdateBannerPermalinksJob

### Продукт/подсистема

Реклама Организаций


### Роль в работе продукта/подсистемы

Подтягивает из Справочника организации для саджеста (так называемые "автопривязанные"). 


### Датафлоу

1. YQL'ем `update_banner_permalinks.yql` вычисляет дифф между уже сохранёнными в дииректе "автопривязанными" организациями и организациями в выгрузке Справочника (`//home/altay/y-direct/current-state/banners-to-permalink`)
2. Актуализирует записи в `banner_permalinks` с `permalink_assign_type=auto`

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateBannerPermalinksJob.working.production)
- [Логи](https://nda.ya.ru/t/_mibEZtM3rRWTh)


### Какая функциональность пострадает от отказа джобы

- (критично) Перестанем подсказывать организации для объявлений


### Как пользователи (или команда) заметят проблему и через какое время

- Пользователи заметят, что не работают подсказки организаций

### Контакты разработчиков и менеджеров

Разработчики: [Максим Логунов](https://staff.yandex-team.ru/maxlog), [Игорь Гердлер](https://staff.yandex-team.ru/gerdler)


### Желательное время исправления в случае поломки

Неделя


### Способы регулирования работы джобы

- property: `update_permalinks_job_in_java_enabled` -- включение джобы
- property: `allow_mass_add_remove_permalinks_in_sync_job` -- разово отключить ограничение на максимальное количество изменений, которые джоба обрабатывает. Если пропертя выключена и лимит превышен, джоба упадёт
