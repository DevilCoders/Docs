# Карта знаков. Форматы вспомогательных файлов

## Таблица с изображеняими
Изображения хранятся в виде точного дампа таблицы из базы данных (все поля сохранены) на YT.
Для создания такой таблицы есть [утилита](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/eye/tool/upload_mrc_feature).

## Файл с объектами на изображении

```json
{
    'features_objects': [
        {
            'feature_id': 1030676,
            'orientation': 1,
            'objects': [
                {
                    'type': 'priority_priority_road',
                    'bbox': [
                        [
                            652,
                            355
                        ],
                        [
                            685,
                            390
                        ]
                    ],
                    'object_id': 0
                },
                {
                    'type': 'prohibitory_no_parking_or_stopping',
                    'bbox': [
                        [
                            337,
                            379
                        ],
                        [
                            356,
                            396
                        ]
                    ],
                    'object_id': 1
                },
                ...
            ],
            ...
        }
    ]
}
```

**feature_id** – уникален и соответствует feature_id в таблицe с изображениями
**object_id** – уникален внутри одной фотографии
**orientation** – должен совпадать со значением для feature
**bbox** – всегда хранится в начальной ориентации (ориентация 1)

## Соответствия объектов на фотографиях

```json
{
    'features_pairs': [
        {
            'feature_id_1': 1,
            'feature_id_2': 2,
            'matches': [
                {
                    'object_id_1': 8,
                    'object_id_2': 1,
                    'confidence': 0
                },
                ...
        },
        {
            'feature_id_1': 2,
            'feature_id_2': 3,
            'matches': [
                {
                    'object_id_1': 8,
                    'object_id_2': 8,
                    'confidence': 0
                },
                ...
            ]
        },
        ...
    ]
}
```

**feature_id** – уникален и соответствует feature_id таблице с изображениями
**object_id** – уникален внутри одной фотографии
**confidence** – уверенность алгоритма в матче (пока без ограничений!)

## Кластера объектов на фотографиях
Каждый кластер представляет один физический объект собранный на разных фотографиях

```json
{
    'clusters': [
        {
            'cluster_id': 0,
            'objects' : [
                {'feature_id': 1, 'object_id': 3},

                ...

                {'feature_id': 5, 'object_id': 8}
            ]
        },

            ...

        {
            'cluster_id' : 100,
            'objects' : [
                {'feature_id': 222,'object_id': 0},

                ...

                {'feature_id': 333,'object_id': 7}
            ]
        }
    ]
}
```

**feature_id** – уникален и соответствует feature_id таблице с изображениями
**object_id** – уникален внутри одной фотографии
