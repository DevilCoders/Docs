# Бэкапилка YT таблиц проекта Bannerland

Это регулярный процесс, который запускается в виде sandbox таски, которая занимается бэкапом таблиц, указанных в конфиге на кластере markov.
* Бэкапы пишутся в папку [//home/bannerland/stable/backups](https://yt.yandex-team.ru/hahn/navigation?path=//home/bannerland/stable/backups), на каждом кластере где есть нужные таблички.
* В каждую табличку/папку пишутся атрибуты `backup_source_path` и `backup_source_object`, имеющие путь, показывающий источник бэкапа. `backup_source_object` показывает какой объект был выбран, если используется `backup_latest_regex`.
* Если вы хотите разрабатываться или тестироваться, то везде в этой инструкции и в коде нужно заменить `stable` на `testing`. А ещё для локального тестирования лучше пользоваться папкой `bin`, она работает аналогично `sandbox_task`.
* Конфиг лежит по адресу: [markov.//home/bannerland/stable/yt_tables_backup_config](https://yt.yandex-team.ru/markov/navigation?path=//home/bannerland/stable/yt_tables_backup_config).
    * Смысл колонок конфига:
        * `source_path` - путь к тому что нужно бэкапить, это может быть таблица или папка.
        * `backup_latest_regex` - опциональная переменная; `source_path` должно быть папкой; по этой регулярке отсеивает объекты, и бэкапит только последний из них. Может быть полезно, если в папке лежит что-то вроде: `1160000.diff`, `1160000.del`, `11550000.diff` итд, чтобы отдельно можно было бэкапить разные виды таблиц.
        * `backup_subdir` - подпапка в которую нужно бэкапить.
        * `src_cluster` - кластер откуда бэкапить.
        * `dst_cluster` - кластер куда бэкапить, пока что поддерживается только `src_cluster == dst_cluster`.
        * `backup_period` - период бэкапа [в формате ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Durations), примеры: `P1D` - раз в день, `PT1H` - раз в час, `P1MT1M` - раз в 1 месяц + 1 минута.
        * `max_tables` - опциональная переменная; если указано, то количество бэкапов ограничивается этим числом.
    * Добавить строку в конфиг:
        ```bash
        echo '{
            "source_path": "...",
            "backup_latest_regex": "...",
            "backup_subdir": "...",
            "src_cluster": "...",
            "dst_cluster": "...",
            "backup_period": "...",
            "max_tables": ...
        }' | ya tool yt insert-rows --format 'json' --proxy markov //home/bannerland/stable/yt_tables_backup_config
        ```
    * Удалить строку из конфига. Обязательно указывать оба поля, потому что по ним однозначно определяется строка конфига.
        ```bash
        echo '{
            "source_path": "...",
            "backup_latest_regex": "..."
        }' | ya tool yt delete-rows --format 'json' --proxy markov //home/bannerland/stable/yt_tables_backup_config
        ```
* [Дашборд с мониторингами](https://monitoring.yandex-team.ru/projects/bannerland/dashboards/monl8r4hgiaaap4lr837/view?range=1w&refresh=60)
    * Мониторится: 
        * Настоящее время между бэкапами.
        * Размер всех бэкапов.
        * Время копирования таблицы. 
        * Время удаления таблицы.
* [Шедулер, запускающий sandbox таску](https://sandbox.yandex-team.ru/scheduler/712125/view)
    * Запускается раз в 30 минут, поэтому если вам бэкап нужен чаще, поменяйте частоту его запуска.
