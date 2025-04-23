# Выгрузка для аналитиков
Кроновый процесс для построения выгрузок хранилища для mstat. Задача запускаются раз в час по всему стейту хранилища, в истории хранятся по 5 таблиц за сегодняшний день и по одной таблице за последние 5 дней. Выгрузка готовится на arnold и hahn.      

## CPA offers
В данную выгрузку попадают все оффера с типом CPA. В рамках одной выгрузки готовятся таблицы `basic`, `service`, `actual`, которые являются отфильтрованной копией динамических таблиц хранилища, и контрактная таблицы. Формат первых трех таблиц нигде не задокументирован, и вопросы "где лежит поле X" лучше направлять чат офферного хранилища.     

Кластер | Testing | Stable |
--- | --- | ---
Arnold | [//home/market/testing/indexer/datacamp/export/filtered](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/testing/indexer/datacamp/export/filtered) | [//home/market/production/indexer/datacamp/export/filtered](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/indexer/datacamp/export/filtered)
Hahn | - | [//home/market/production/indexer/datacamp/export/filtered](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/indexer/datacamp/export/filtered)

### Схема контрактной таблицы
{% code '/market/idx/datacamp/routines/tasks/mstat_dumper/proto/schemas.proto' lang='proto' lines='[BEGIN contract format]-[END contract format]' keep-indents='false' %}
