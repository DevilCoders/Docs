Здесь собраны различные инструменты, так или иначе связанные с метрикой mtinfo. Многие из них предполагают ручной запуск и анализ результатов.
Рассмотрим основные сценарии использования.

### Собрали новые треки, хотим пересчитать качество PGT
1) Сначала нужно загрузить треки из Startek на YT. Для этого делаем
    ```
    ./transfer_gt --dst //home/yatransport/mtinfo-metrics/gt/raw --close-issues
    ```
1)  Затем собираем треки, которые хотим проанализировать, в одну таблицу.
    Например, обычно имеет смысл взять треки только из одного города, т.к. в разных городах разное качество сигналов.\
    Если нужно, переименовываем колонку `gtid` в `vehicle_id`.
    ```
    yt merge //home/yatransport/mtinfo-metrics/gt/raw/MTGPSTRACKS-{63,64,65,67,68,69,70,72,73} --dst '//home/yatransport/mtinfo-metrics/gt/processed/2019-08-12/moscow'
    ```
1)  На этом этапе можно нарисовать все треки в easyview и убедиться, что нет неправильных точек (например, в океане).
    ```
    ./format_for_easyview -i //home/yatransport/mtinfo-metrics/gt/processed/2019-08-12/moscow -g vehicle_id --static | ~/bin/easyview
    ```
    Здесь `~/bin/easyview` - результат сборки [maps/tools/easyview/bin](https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/easyview/bin/ya.make). См. также [readme для format_for_easyview](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/statistics/info/gt_based_metrics/tools/format_for_easyview#%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5).\
    Если необходимо, правим некоторые треки вручную и переделываем предыдущий пункт.
1)  Далее для экономии ресурсов нужно отобрать из всех сигналов только те, которые действительно могут соответствовать трекам. Например, отфильтровать по `clid`.\
    Удобнее всего это делать с помощью YQL.
    ```SQL
    PRAGMA yt.InferSchema;
    USE hahn;

    INSERT INTO `//home/yatransport/mtinfo-metrics/signals/raw/2019-08-12` WITH TRUNCATE
    FROM RANGE(`home/yatransport-prod/production/signals`, `2019-08-12`, `2019-08-13`)
    SELECT
        `clid`, `uuid`,
        `time` as `timestamp`,
        `lon`, `lat`,
        `route`, `vehicle_type`
    WHERE
        clid IN ("codd_new", "avtoline")
    ORDER BY
        `clid`, `uuid`, `timestamp`;
    ```
    Обратите внимание, что колонку `time` нужно переименовать в `timestamp`.
1)  Теперь нужно для каждого трека найти, какой паре `clid`, `uuid` он соответствует. Для этого есть скрипт `grep_signals_for_gt`.\
    Важно понимать, что сложность работы алгоритма пропорциональна произведению количества треков и размера таблицы с сигналами.
    Поэтому, если треки покрывают большое количество дней, то, возможно, лучше найти соответствие для каждого дня отдельно,
    а уже потом слить результаты за разные дни в одну табличку.
    ```
    ./grep_signals_for_gt -g //home/yatransport/mtinfo-metrics/gt/processed/2019-08-12/moscow -s //home/yatransport/mtinfo-metrics/signals/raw/2019-08-12 -m //home/yatransport/mtinfo-metrics/gt/matched_gt/2019-08-12 -o //home/yatransport/mtinfo-metrics/gt/signals/2019-08-12/moscow
    ```
    На выходе получаем две таблицы - matched_gt и полученные сигналы.
    На первую достаточно взглянуть глазами и убедиться, что нет слишком больших значений `score`.
    Если есть, это может означать, что для трека не было метки ТС, и он заматчился на совсем другое ТС.
1)  Далее для полученных сигналов строим PGT. Сейчас это делается в 2 этапа:
    ```
    ./offline_binder -i //home/yatransport/mtinfo-metrics/gt/signals/2019-08-12 -o //home/yatransport/mtinfo-metrics/pgt/1d/moscow/2019-08-12 --data-mms ~/edata/yandex-maps-mtgpsmodel-production:v6_19.08-11-0/data.mms
    ```
    ```
    ./expand_trajectory -i //home/yatransport/mtinfo-metrics/pgt/1d/moscow/2019-08-12 -t //home/yatransport/mtinfo-metrics/pgt/2d/moscow/2019-08-12 -s //home/yatransport/mtinfo-metrics/pgt/arrivals/moscow/2019-08-12 --data-mms ~/edata/yandex-maps-mtgpsmodel-production:v6_19.08.11-0/data.mms
    ```
1)  Теперь можно вычислить качество построенного PGT.
    ```
    ./compare_pgt_gt -m ~/edata/yandex-maps-mtgpsmodel-production:v6_19.08.11-0/data.mms -p //home/yatransport/mtinfo-metrics/pgt/2d/moscow/2019-08-12 -g //home/yatransport/mtinfo-metrics/gt/processed/2019-08-12/moscow -o //home/yatransport/mtinfo-metrics/analyzer/pgt-gt/moscow/2019-08-12
    ```
    Получаем таблицу `//home/yatransport/mtinfo-metrics/analyzer/pgt-gt/moscow/2019-08-12` с несколькими величинами, описывающими отклонение PGT от GT.
1)  Сохраняем `data.mms`, а также полученные таблицы `gt/processed/2019-08-12/moscow`, `gt/signals/2019-08-12` и `analyzer/pgt-gt/moscow/2019-08-12`.
![PGT-GT comparison scheme](https://jing.yandex-team.ru/files/kalabukdima/pgt_gt_flow.png)
(схема в xlsx [здесь](https://jing.yandex-team.ru/files/kalabukdima/pgt_gt_flow.xlsx))

### Изменили алгоритм генерации PGT, хотим пересчитать его качество
1) Находим таблицу с собранными GT. Например, после выполнения предыдущего пункта это `//home/yatransport/mtinfo-metrics/gt/processed/2019-08-12/moscow`.
1) Находим таблицу с сигналами, выбранными для этого GT. В предыдущем пункте это `//home/yatransport/mtinfo-metrics/gt/signals/2019-08-12`.
1) Находим `data.mms` за подходящую дату.
1)  Строим PGT.
    ```
    ./offline_binder -i //home/yatransport/mtinfo-metrics/gt/signals/2019-08-12 -o //home/yatransport/mtinfo-metrics/pgt/1d/moscow/2019-08-12 --data-mms ~/edata/yandex-maps-mtgpsmodel-production:v6_19.08-11-0/data.mms
    ```
    ```
    ./expand_trajectory -i //home/yatransport/mtinfo-metrics/pgt/1d/moscow/2019-08-12 -t //home/yatransport/mtinfo-metrics/pgt/2d/moscow/2019-08-12 -s //home/yatransport/mtinfo-metrics/pgt/arrivals/moscow/2019-08-12 --data-mms ~/edata/yandex-maps-mtgpsmodel-production:v6_19.08.11-0/data.mms
    ```
1)  Сравниваем с GT.
    ```
    ./compare_pgt_gt -p //home/yatransport/mtinfo-metrics/pgt/2d/moscow/2019-08-12 -g //home/yatransport/mtinfo-metrics/gt/processed/2019-08-12/moscow -o //home/yatransport/mtinfo-metrics/analyzer/pgt-gt/moscow/2019-08-12_new
    ```
    Получаем таблицу `//home/yatransport/mtinfo-metrics/analyzer/pgt-gt/moscow/2019-08-12_new` с новой оценкой PGT.

### Изменили алгоритм построения прогнозов. Хотим сравнить с PGT до выкатки в testing.
Сейчас нет простой возможности это сделать. Можно посмотреть [код регулярной задачи сравнения FC и PGT](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitMtinfoMetrics/__init__.py?rev=6084303#L157),
а также [`tools/quality`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/tools/quality?rev=3864770).