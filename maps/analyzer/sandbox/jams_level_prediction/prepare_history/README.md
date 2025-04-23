Подготовка истории пробочных баллов
---

История пробочных баллов используется для предсказания баллов

Регулярный процесс обрабатывает два типа исходных таблиц с логами:
- Старые: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jamsarchive/jamsarchive)
- Новые: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/maps-core-jams-info-production-levels/1d)

В процессе работы создаются таблицы с обработанной историей пробочных баллов:
- Development: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/dev/jams_level_prediction/levels)
- Testing: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams_level_prediction/levels)
- Production: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams_level_prediction/levels)

Во время обработки записи приводятся к единому формату, фильтруются некорректные записи и удаляются дубли.

Далее из таблиц с полной историей создаются почасовые таблицы с баллами:
- Development: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/dev/jams_level_prediction/levels_hourly)
- Testing: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams_level_prediction/levels_hourly)
- Production: [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams_level_prediction/levels_hourly)

Таблицы с полной историей используются в качестве элементов обучающей выборки, а почасовые таблички – для формирования таргета при тренировке модели предсказания.
