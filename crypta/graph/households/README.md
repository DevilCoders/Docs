Домохозяйства
=============

1. Сбор данных `/data_import`
    - Парсятся пятиминутные таблицы логов `bs-watch-log`, выбираются связки `(yuid, ip, dt)`
    - Санбокс шедулеры [`tag:households`, `tag:data_import`](https://sandbox.yandex-team.ru/schedulers/?tags=HOUSEHOLDS%2CDATA_IMPORT&page=1&order=-id&pageCapacity=20&all_tags=true)
    - Инкрементально собираются таблицы за 30 дней [[//home/crypta/production/state/households_new/storage/{date}]](https://yt.yandex-team.ru/hahn/navigation?path=//home/crypta/production/state/households_new/storage&sort[asc]=false&sort[field]=name)
    - Удаляются автоматически, через атрибут `@expiration_time`

2. Построение домохозяйств
    ...
