# match_signals_online

Sandbox задача, которая матчит gps сигналы от транспорта на нитки маршрутов, запуская [матчер](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/pylibs/match_signals) на YT в качестве редьюсера.

Задача запускается регулярно в scheduler: [testing](https://sandbox.yandex-team.ru/scheduler/712248/view), [stable](https://sandbox.yandex-team.ru/scheduler/712324/view).

По-умолчанию [исходные сигналы](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/masstransit/yatransport-prod/production/signals) берутся за последние 14 дней.

Результат складывается в папку на YT: [testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/matched_signals_online), [stable](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/matched_signals_online).
