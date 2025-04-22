Регулярные процессы сервиса предсказания пробочных баллов
===

Способ организации регулярного запуска процессов описан в [`README на уроверь выше`](../README.md)

| Процесс | Описание | Ссылки |
--- | --- | ---
[`evaluate_quality`](evaluate_quality) | Оценка качества предсказания пробочных баллов | [Таблица на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/quality)
[`prepare_history_storage`](prepare_history_storage) | Подготовка датасета с историей пробочных баллов | Файлы на yt: [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/history_storage), [продакшен](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/history_storage); датасет в ecstatic: yandex-maps-jams-level-history-storage
[`prepare_history`](prepare_history) | Подготовка истории пробочных баллов | Результаты на YT: полная история – [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/levels_month), [продакшен](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/levels_month); почасовая история – [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/levels_hourly_month), [продакшен](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/levels_hourly_month)
[`prepare_training_pool`](prepare_training_pool) | Подготовка трейн-пула для обучения модели предсказания пробочных баллов | Результаты в [тестинге](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/training_pool_month), [продакшне](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/training_pool_month)
[`train_model`](train_model) | Обучение модели предсказания пробочных баллов | Файлы на yt: [тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/jams-level-prediction/models), [продакшен](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/models); датасет в ecstatic: yandex-maps-jams-level-prediction-model

## Архивные данные

[Логи прогнозов](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/jams-level-prediction/production_log/log) старого предиктора из Поиска. Процесс сбора логов удалён в [MAPSJAMS-4300](https://st.yandex-team.ru/MAPSJAMS-4300)
