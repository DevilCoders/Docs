# Описание

## Подготовка событий
Подготовка треков:
```bash
python collect_stop_tracks.py --month-date 2018-01
```

Притягивание треков, выделение точек остановок:
```bash
python filter_project_tracks.py --month-date 2018-01
```

## Подготовка кандидатов
Создание кластеров:
```bash
python generate_clusters.py --start-month-date 2018-01 --end-month-date 2018-10
```

Подсчет весов (популярностей):
```bash
python calculate_weights.py --start-month-date 2018-01 --end-month-date 2018-10
```

Получение дополнительной информации о точках:
```bash
python extract_meta.py
```

Фильтрация и разреживание кластеров, получение финальных кандидатов:
```bash
python sparse_filter_candidates.py
```

Подготовка продакшн таблицы с финальными кандидатами (production или testing):
```bash
python dump_candidates_table.py
```

## Обучение модели
Сбор обучающей выборки:
```bash
python collect_learning_set.py --start-date 2018-11-01 --start-date 2018-11-30
```

Обучение:
```bash
python learn_model.py --validation-start-date 2018-11-20
```
