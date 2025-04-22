## building_info

Утилита геокодирует таблицы dom_mingkh_ru, reformagkh_ru_all, geocoded_gasification и формирует сниппеты согласно [json-схеме](https://a.yandex-team.ru/arc/trunk/arcadia/search/geo/tools/task_manager/schemas/building_info_experimental/1.x/building_info_experimental.json)

Приведенная утилита запускается в рамках процесса в Nirvana [Prepare snippet building_info/1.x data](https://nirvana.yandex-team.ru/flow/aaba5491-61d2-470b-bf96-aedcb6e034c8/)

### Параметры CLI

- `--input-dom-mingkh-ru` - путь к таблице dom_mingkh_ru
- `--input-reformagkh-ru-all` - путь к таблице reformagkh_ru_all
- `--input-geocoded-gasification` - путь к таблице geocoded_gasification (по умолчанию: [//home/maps/geoapp/snippets/building_info/gasification/latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/geoapp/snippets/building_info/gasification/latest))
- `--intermediate-table-prefix` - префикс для промежуточных таблиц
- `--error-table-prefix` - префикс для таблиц с ошибками
- `--output-table` - итоговая таблица
- `--cluster` - YT-кластер (по умолчанию `hahn`)

#### Параметры для ограничения нагрузки на геокодер

- `--mapper-slots-limit` - максимальное число одновременно запущенных YT-джобов
- `--mapper-data-size-per-job` - рекомендованный объём данных на входе у одного YT-джоба
