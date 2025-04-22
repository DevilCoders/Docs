# Пайплайн `alerts_statistics`

Пайплайн сделан для анализа ситуации с алертами. Каждый день берем [juggler логи](//home/logfeller/logs/juggler-banshee-log/1d)
отправок уведомлений и считаем из них выжимку наших алертов за новые дни.
Подразумевается, что по этой информации можно будет оценивать количество времени,
которое тратится на разбор алертов в группе geoq.

## Важные ссылки

| Что? | Где? |
| --- | --- |
| ABC | [maps-core-geoq](https://abc.yandex-team.ru/services/maps-core-geoq/) |
| Робот | [robot-geoq-core](https://staff.yandex-team.ru/robot-geoq-core) |
| Графики | [datalens](https://datalens.yandex-team.ru/1lwirktyqhvgu-statistika-alertov-v-geoq-chate) |
| YT | Stable: [//home/maps/poi/statistics/alerts_statistics](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/alerts_statistics) |
| Sandbox | Sedem-managed [GEOQ_CALCULATE_ALERTS_STATISTICS](https://sandbox.yandex-team.ru/scheduler/698323/view) |
| Логи Juggler на YT | [//home/logfeller/logs/juggler-banshee-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/juggler-banshee-log/1d) |
