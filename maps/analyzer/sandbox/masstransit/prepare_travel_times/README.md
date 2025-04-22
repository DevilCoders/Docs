prepare_travel_times: создание travel times из привязанных сигналов ОТ (bound_signals, matched_singals).
---

Создает две таблички на день по одной на сигналы привязанные старым байндером и новым матчером.
Промежуточный процесс, который для набора GPS сигналов создает трек, который состоит из последовательных сегментов ниток с временем проезда, временем заезда на сегмент (enter_time) и временем выезда из него (leave_time).

### Результаты

Testing:<br>
[//home/maps/jams/testing/masstransit/travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/travel_times)<br>
[//home/maps/jams/testing/masstransit/matched_travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/matched_travel_times)<br>
Production:<br>
[//home/maps/jams/production/masstransit/travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/travel_times)<br>
[//home/maps/jams/production/masstransit/matched_travel_times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/matched_travel_times)
