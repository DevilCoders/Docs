# Сборка param_values

param_values -- таблица, которая используется на бэке для отображения всевозможных параметров моделей. Параметры берём из таблицы [parameters](//home/market/production/mbo/export/recent/parameters). Дополнительно джойним на таблицу [all_models](//home/market/production/mbo/export/recent/models/all_models), чтобы оставить только те параметры, которые есть хотя бы у одной модели.

Таблицу обновляем её раз в месяц.
