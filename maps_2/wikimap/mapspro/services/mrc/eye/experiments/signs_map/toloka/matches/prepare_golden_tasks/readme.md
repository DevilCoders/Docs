Инструмент для подготовки контрольных заданий в Толоке для матчинга знаков.

Ходит в базу данных mrc, получает дополнительную информацию о feature'ах и записывает их в формате,
который принимает на вход блок в Нирване - https://nirvana.yandex-team.ru/operation/72ff4bef-a2d5-4f0d-a02d-f429a021fc1b.

На вход принимаем:
1. ```--mrc-config``` - путь до xml файла с конфигурацией (https://a.yandex-team.ru/arc/history/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/config/cfg)

2. ```--secret-version``` - версия секрета с паролями (https://yav.yandex-team.ru/secret/sec-01cp2k8gbhycereqjrqg2va311).

3. ```--objects``` - путь до json файла с детекциями на feature'ах

4. ```--pairs``` - путь до текстового файла с парами айдишников feature'ей

5. ```--matches``` - путь до json файла с матчами объектов

5. ```--tasks``` - путь до json файла с заданиями для Толоки

Формат файла **objects**:
```json
{
    "features_objects": [
        {
            "feature_id": <feature_id>,
            "orientation": <orientation>,
            "objects": [
                {
                    "type": <type>,
                    "bbox": [[<x_min>, <y_min>], [<x_max>, <y_max>]],
                    "object_id": <object_id>
                },
                ...
            ]
        }
    ]
}
```

Формат файла **pairs**:
```
<feature_id> <feature_id>
<feature_id> <feature_id>
...
```

Формат файла **matches**:
```json
{
    'features_pairs': [
        {
            'feature_id_1': <feature_id>,
            'feature_id_2': <feature_id>,
            'matches': [
                {
                    'object_id_1': <object_id>,
                    'object_id_2': <object_id>
                },
                ...
            ]
        },
        ...
    ]
}
```

Формат файла **tasks**:
```json
[
   {
       "inputValues": {
           "features": [
               {
                   "feature_id": <feature_id>,
                   "url": <url>,
                   "heading": <heading>,
                   "position": [<lon>, <lat>],
                   "objects": [
                       {
                           "object_id": <object_id>,
                           "type": <type>,
                           "bbox":[[<x_min>, <y_min>], [<x_max>, <y_max>]]
                       },
                       ...
                   ]
               },
               {
                   "feature_id": <feature_id>,
                   "url": <url>,
                   "heading": <heading>,
                   "position": [<lon>, <lat>],
                   "objects": [
                       {
                           "object_id": <object_id>,
                           "type": <type>,
                           "bbox": [[<x_min>, <y_min>], [<x_max>, <y_max>]]
                       },
                       ...
                   ]
               }
            ]
        }
    },
    ...
]
```
