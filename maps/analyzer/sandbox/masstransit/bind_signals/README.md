Привязка GPS сигналов движения ОТ к тредам
---

Создает две таблички на день.
Для создания таблички за день использует GPS сигналы ОТ за тот же день, regions-config (партнерский конфиг) и MtDataMms.
* **bound_signals** - привязывается кодом из [текущей оффлайн привязки ОТ](/arc/trunk/arcadia/maps/masstransit/statistics/info/gt_based_metrics/tools/offline_binder/lib).
* **matched_signals** - привязывается кодом из [новой привязки ОТ](/arc/trunk/arcadia/maps/masstransit/libs/matching) с использованием [оффлайн конфига](/arc/trunk/arcadia/maps/masstransit/libs/matching/configs/offline.json).

### Результаты

Testing:<br>
[//home/maps/jams/testing/masstransit/bound_signals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/bound_signals)<br>
[//home/maps/jams/testing/masstransit/matched_signals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/matched_signals)<br>
Production:<br>
[//home/maps/jams/production/masstransit/bound_signals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/bound_signals)<br>
[//home/maps/jams/production/masstransit/matched_signals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/matched_signals)
