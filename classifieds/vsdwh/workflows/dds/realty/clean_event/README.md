## Очищенный event-лог Яндекс Недвижимости

Лог представляет из себя набор view над таблицами event-лога Яндекс Недвижимости - [//home/verticals/broker/prod/warehouse/realty/event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/realty/event/1d), в которых реализована логика очистки фрода.

##### Описание таблиц
Путь в YT [//home/verticals/vertis-bi/dds/realty/clean_event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/vertis-bi/dds/realty/clean_event/)
- `clean` - очищенные события
- `fraud` - фрод, роботы и стафф

##### Артефакты
- [/verticals/vertis-bi/dds/realty/clean_event/a_dds_realty_clean_event_clean_1d](https://reactor.yandex-team.ru/browse/resolve?path=/verticals/vertis-bi/dds/realty/clean_event/a_dds_realty_clean_event_clean_1d)
- [/verticals/vertis-bi/dds/realty/clean_event/a_dds_realty_clean_event_fraud_1d](https://reactor.yandex-team.ru/browse/resolve?path=/verticals/vertis-bi/dds/realty/clean_event/a_dds_realty_clean_event_fraud_1d)

##### Правила очистки
1) Роботы и стафф:
   ```sql
   WHERE NOT user_info.user_is_in_yandex
     AND NOT user_info.antirobot_degradation
2) Общий антифрод - [VSANALYTICS-4544](https://st.yandex-team.ru/VSANALYTICS-4544)

   Для фильтрации используются выжимки `yandexuid`-ов из таблицы [//home/antifraud/export/uid_types/daily](https://yt.yandex-team.ru/hahn/navigation?path=//home/antifraud/export/uid_types/daily/) по сервисам Вертикалей. Выжимки лежат в -
  [dds/common/fraud_lists](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/verticals/vertis-bi/dds/common/fraud_lists)

3) Новая оффлайн очистка антифрода для Вертикалей - [VSML-1132](https://st.yandex-team.ru/VSML-1132)

   Для фильтрации используется таблица [//home/antifraud/xurma/afraudita/prod/analytics/verdicts/1d/vertis-realty-event-verdicts-log](https://yt.yandex-team.ru/hahn/navigation?path=//home/antifraud/xurma/afraudita/prod/analytics/verdicts/1d/vertis-realty-event-verdicts-log). Доступ можно запросить [тут](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&navmode=acl&path=//home/antifraud/xurma/afraudita/prod/analytics/verdicts/1d/vertis-realty-event-verdicts-log).

Актуальные правила очистки в папке `yql`.

##### Особенности работы с логом

1) Функция `TableName()` не работает при селекте из *view* (результат всегда будет `NULL`), поэтому для того чтобы достать текущую дату лучше использовать ```CAST(`timestamp` AS Date) AS day```
2) *View* не работают с операцией [Get MR Table](https://nirvana.yandex-team.ru/alias/operation/get-mr-table_by_robot-nirvana)

##### Мониторинг
Сводный дашборд в Juggler: [vertis-razladki/antifraud-realty-summary](https://juggler.yandex-team.ru/dashboards/antifraud-realty-summary?project=vertis-razladki)

На текущий момент заведены проверки на падение графа создающего *view* и задержку в поставке - загорается если *view* не было создано до 10 часов дня.

Для мониторинга качества антифрода заведены алерты в разладких  - [classifieds/vsdwh/workflows/dq/razladki/realty/antifraud](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/workflows/dq/razladki/realty/antifraud).
