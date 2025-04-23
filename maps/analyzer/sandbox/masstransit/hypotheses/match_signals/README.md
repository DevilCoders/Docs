Привязка GPS сигналов движения ОТ к ниткам для генерации гипотез изменений маршрутов
---

Создает одну табличку на день.
Для создания таблички за день использует GPS сигналы ОТ за тот же день, и MtDataMms.
В отличие от процесса [masstransit/bind_signals](/arc/trunk/arcadia/maps/masstransit/bind_signals) выполняет привязку без предварительной фильтрации сигналов по clid.

* **hypotheses/matched_signals** - привязывается кодом из [привязки ОТ](/arc/trunk/arcadia/maps/masstransit/libs/matching) с использованием [оффлайн конфига](/arc/trunk/arcadia/maps/masstransit/libs/matching/configs/offline.json).

### Результаты

Testing:<br>
[//home/maps/jams/testing/masstransit/hypotheses/matched_signals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/hypotheses/matched_signals)<br>
Production:<br>
<br>
[//home/maps/jams/production/masstransit/hypotheses/matched_signals](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/hypotheses/matched_signals)
