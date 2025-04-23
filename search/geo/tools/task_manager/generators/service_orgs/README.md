## service_orgs

Варщик экспериментального сниппета для Обслуживающих организаций `service_orgs_experimental/1.x`.

Подклеивает к домам:
- МФЦ
- Налоговые
- Почтовые отделения
- Школы

#### Требуемые переменные окружения

- `SNIPPET_HOME` - рабочая YT-директория варщика
- `SCHEDULED_DATE` - сегодняшняя дата, из которой будет формироваться имя выходной таблицы
- `YT_PROXY` - используемый YT кластер
- `YT_TOKEN` - YT-токен
- `YQL_TOKEN` - YQL-токен

### links

[YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/geoapp/snippets/service_orgs)

[Reactor](https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/geosearch/schedulers/build-service-orgs)

### config

[`lib/common/config.py`](/arc/trunk/arcadia/search/geo/tools/task_manager/generators/service_orgs/lib/common/config.py)

#### Секции

- `yt.cluster` - используемый YT кластер
- `service_orgs.result_table` - YT-таблица со сниппетами
- `service_orgs.result_link` - ссылка на YT-таблицу, которая прорастает в [Task Manager](https://wiki.yandex-team.ru/users/karas-pv/snippetstaskmanager/)

- `aurora.nalogovaya_ru_table` - YT-таблица выгрузка с nalogovaya.ru - отсюда берем данные о налоговых
- `aurora.obrmos_ru_schools_table` - YT-таблица выгрузка с obrmos.ru - отсюда берем данные о московских школах
- `geosrc.dir` - YT-директория с экспортом Геокодера - отсюда берем дома России
- `sprav.company_export_table` - YT-таблица protobuf-экспорт компаний из Алтая
- `sprav.snapshot_dir` - YT-директория снапшот Алтая
- `ymapsdf.dir` - YT-директория с выгрузкой [ymapsdf](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/about.html?lang=ru) - отсюда берем почтовые индексы для домов

- `temp.*` - промежуточные YT-таблицы варки
- `feeds.*` - фиды с данными `geocoder_id -> permalinks`, из которых клеится сниппет

### sources

| Название            | Ссылка                                                                                            |
| ------------------- | ------------------------------------------------------------------------------------------------- |
| geosrc              | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/geocoder/geosrc/latest_state           |
| ymapsdf             | https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest                  |
| altay-prod-snapshot | https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/geosearch_snapshot         |
| altay-prod-export   | https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/export/exported            |
| nalogovaya.ru       | https://yt.yandex-team.ru/hahn/navigation?path=//home/aurora/release/maps/nalogovaya_ru           |
| obrmos.ru schools   | https://yt.yandex-team.ru/hahn/navigation?path=//home/aurora/release/maps/other/obrmos_ru_schools |
