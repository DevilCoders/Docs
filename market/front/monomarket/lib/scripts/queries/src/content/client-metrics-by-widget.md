# Клиентские метрики по виджетам на KPI-страницах

Было проведено исследование о том, как мы считаем наши TTR и TTI (https://st.yandex-team.ru/MARKETFRONTECH-2531).

Исходя из исследования, если взять top-1 строчку по каждой странице, это будет TTR/TTI страницы.

Наша агрегированная метрика: https://datalens.yandex-team.ru/4gcgvlxhzqnaz-need-for-speed-po-celevym-stranicam.

Табличка кликфита с данными: https://health.market.yandex-team.ru/projects/marketfrontend/clickphite/configs/front_speed_kpi_region_filtered/4/edit/json

Код в мандреле: https://github.yandex-team.ru/market/monomarket/blob/master/lib/lib/mandrel/src/launchClient/timers.js#L123.

Эта таблица -- попытка детализировать данные агрегированной метрики.

Теги: `агрегированная метрика`, `виджеты`, `ttr`, `tti`, `метрики скорости`, `первый экран`.

Ссылка: https://yql.yandex-team.ru/Operations/YLD34PMBw877WwUPyvsz_FfZdhw8RJhnXIAHflim4W8=

```sql
use marketclickhouse;

/* TTR и TTI в белом */
select
    service,
    page_id,
    widgetName,
    round(quantile(0.95)(TTI)) as TTI_p95,
    round(quantile(0.95)(TTR)) as TTR_p95,
    round(quantile(0.95)(hydrating)) as hydrating_p95,
    round(quantile(0.95)(stuffing)) as stuffing_p95,
    count(*) as hits
  from (
    select
        *,
        info_values[indexOf(info_keys, 'widgetName')] as widgetName,
        info_values[indexOf(info_keys, 'onFirstScreen')] as onFirstScreen,
        /*
            Страничный TTI считается по формуле
            timestamp_ms - start_time_ms + duration_ms (0.95)
            здесь timestamp -- firstScreen.arrived
                duration -- firstScreen.inited - firstScreen.arrived

            то есть страничный TTI = firstScreen.inited - start_time_ms
            firstScreen.inited = max(ProcessedWidgetReport.timings.inited)

            timings.inited не пишется, зато пишутся timings.arrived, timings.hydrated, timings.duration.stuffing, timings.duration.hydrating

            timings.inited = widgetType === 'static' ? timings.arrived : timings.hydrated;

            Пренебрежение: все виджеты с высокими таймингами не статические
            для грубой оценки можно использовать round(quantile(0.95)(duration_ms))
        */
        timestamp_ms + duration_ms as hydrated,
        hydrated - start_time_ms as TTI,

        /*
            Страничный TTR считается по формуле
            timestamp_ms - start_time_ms (0.95)
            здесь timestamp -- firstScreen.arrived
        */
        timestamp_ms - start_time_ms as TTR,

        /*
            Для полноты картины взглянем на новые метрики
        */
        toInt64(info_values[indexOf(info_keys, 'hydrating')]) as hydrating,
        toInt64(info_values[indexOf(info_keys, 'stuffing')]) as stuffing
      from `market`.`market_client_timers`
     where date = toDate('2021-05-17')
       and page_id in ('market:index', 'market:search', 'market:list', 'market:product', 'touch:index', 'touch:search', 'touch:list', 'touch:product')
       and service in ('market_front_desktop', 'market_front_touch')
       and name = 'widget'
  )
 where onFirstScreen = 'true'
 group by service, page_id, widgetName
 having hits > 7000
 order by page_id asc, TTI_p95 desc, TTR_p95 desc;
```
