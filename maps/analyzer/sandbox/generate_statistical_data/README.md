Генерация статистических данных для моделей предсказания ETA поездки и движения ОТ
---

Процесс использует дневные статистики для генерации датасета.

В процессе работы выполняет следующие действия:
- мержит таблицы с дневными статистиками, подготавливаемые процессами [eta_prediction/compute_daily_speed_stats](/arc/trunk/arcadia/maps/analyzer/sandbox/eta_prediction/compute_daily_speed_stats), [masstransit/compute_daily_speed_stats](/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit/compute_daily_speed_stats)
- фильтрует записи и сортирует результат
- подает записи на вход бинарнику для сериализации
- сохраняет данные на YT
- сохраняет данные в локальную директорию для последующей загрузки в ecstatic

### Результаты
Пробочные скорости:
[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams_statistical_data)</br>
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams_statistical_data)

Скорости движения ОТ:
[Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/statistical_data)</br>
[Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/statistical_data)
