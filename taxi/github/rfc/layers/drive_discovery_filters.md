Ссылочки:

* Эпик: https://st.yandex-team.ru/TAXIBACKEND-34682
* Дизайн: https://www.figma.com/file/h1AhBCW20n9biZMlg7dSUO/Filters-in-Go?node-id=11%3A25
* Главный скриншот: https://st.yandex-team.ru/TAXIBACKEND-34682/attachments/30233475

## Ручка с фильтрами

На стороне Драйва возвращается все из одной ручки /api/taxi/car/list
(пример ответа: https://paste.yandex-team.ru/4280121). Чтобы не лепить все в /v2/objects на нашей стороне, решили
сделать отдельную ручку. Предлагается новая ручка /4.0/layers/v1/drive-filters, которая будет принимать примерно то же
самое, что и v2/objects:

```json5
{
  "state": {
    "bbox": [
      49.1,
      55.7,
      49.2,
      55.8
    ],
    "known_orders": [
    ],
    "location": [
      30.4,
      59.9
    ],
    "mode": "discovery",
    "pin": [
      49.1,
      55.7
    ],
    "screen": "drive",
    "zoom": 16.7,
    "size_hint": 322
    // Для подбора подходящей картинки машины
  }
}
```

В ответе мы должны вернуть набор фильтров. На текущий момент фильтры из драйва возвращаются с некоторой древесной
архитектурой. У фильтов есть типы:

- metafilter_regular (обычные машины)
- metafilter_cargo_n_shuttle (груз и шаттл)

Далее есть наборы машин, относящиеся к одному из описанных выше типов, например:

- filter_shuttle (все шаттлы, наследуются от metafilter_cargo_n_shuttle)
- filter_everyday (каждый день, наследуются от metafilter_regular)

Далее по иерархии - фильтр по конкретным машинам, например:

- filter_model_audi_a3_spb (только Ауди А3, наследуется от filter_everyday_plus)
- filter_model_caravelle (Только каравелла, наследуется от filter_shuttle)

Помимо фильтров по предназначению машин есть фильтры-фичи, такие как бортовой компьютер или трап.

Ответ предлагается такой (пригодится для других фильтров):

```json5
{
  "categories": [
    {
      "type": "drive",
      "filter": {
        "icon": "",
        "id": 2826,
        "meta": true,
        "name": "metafilter_regular",
        "special_markers": "",
        "text": "Обычные машины",
        "children_objects": ["filter_everyday", "filter_everyday_plus", 
          "filter_model_audi_a3_spb", "filter_model_kaptur_spb"],
        "parent_objects": [],
      },
    },
    {
      "type": "drive",
      "filter": {
        "icon": "",
        "id": 2811,
        "meta": true,
        "name": "metafilter_cargo_n_shuttle",
        "special_markers": "",
        "text": "Груз и шаттл",
        "children_objects": [],
        "parent_objects": [],
      }
    },
    {
      "type": "drive",
      "filter": {
        "excludes": [
          // если выбран фильтр, указанные тут фильтры недоступны
          "filter_model_expert",
          "filter_model_jumpy",
          "filter_model_transit"
        ],
        "icon": "https://carsharing.s3.yandex.net/drive/filters/computer.png",
        "id": 148,
        "name": "filter_yaauto",
        "parent_objects": [
          "metafilter_cargo_n_shuttle",
          "metafilter_regular"
        ],
        "special_markers": "",
        "text": "Бортовой компьютер",
        "children_objects": []
      },
    },
    {
      "type": "drive",
      "filter": {
        "icon": "https://carsharing.s3.yandex.net/everyday-v1.png",
        "id": 100,
        "name": "filter_everyday",
        "parent_objects": [
          "metafilter_regular"
        ],
        "special_markers": "",
        "text": "На каждый день",
        "children_objects": []
      }
    },
    {
      "type": "drive",
      "filter": {
        "icon": "https://carsharing.s3.yandex.net/everyday-plus-v1.png",
        "id": 72,
        "name": "filter_everyday_plus",
        "parent_objects": [
          "metafilter_regular"
        ],
        "special_markers": "",
        "text": "На каждый день +",
        "children_objects": ["filter_model_audi_a3_spb"]
      }
    },
    {
      "type": "drive",
      "filter": {
        "icon": "https://carsharing.s3.yandex.net/filters/1audi_a3_v0",
        "id": 1286,
        "name": "filter_model_audi_a3_spb",
        "parent_objects": [
          "filter_everyday_plus",
          "metafilter_regular"
        ],
        "children_objects": [],
        "special_markers": "",
        "text": "A3"
      }
    },
    {
      "type": "drive",
      "filter": {
      "icon": "https://carsharing.s3.yandex.net/filters/renault-kaptur-spb_v0",
      "id": 1291,
      "name": "filter_model_kaptur_spb",
      "parent_objects": [
        "filter_everyday"
      ], 
        "children_objects": [],
      "special_markers": "",
      "text": "Kaptur"
    },
    }
  ]
}
```

Дергать ее надо точно в самом начале, а еще, возможно, при передергивании v2/objects (?) для актуализации списка
доступных машин.

## v2/objects

Ручку объектов предлагается расширить, передавая в нее также список выбранных фильтров в виде массива массивов.
  
ВАЖНО!
Фильтры с тегом meta=true не примутся бэком.

При переключении между фильтрами с тегом meta=true, клиентом сбрасываются все фильтры, которые не являются наследниками 
нового фильтра. То есть при выбранной А3 и борткомпьютере при переключении на Грузы сбросится А3, но сохранится борткомпьютер.

Кроме того, при выборах внутри вертикали надо учитывать excludes: выбрали filter_yaauto - не можем выбрать filter_model_expert,
т.к. этот фильтр есть в массиве excludes.

Если выбирается фильтр-родитель (например, filter_everyday), надо создать массив, состоящий из всех детей фильтра, то есть
`[["filter_model_kaptur_spb"],["filter_model_polo_spb"],["filter_model_x_line_spb"]]`

Например, выбрано еще и кресло:
`[ // или
   ["filter_model_kaptur_spb", "chair"], // и
   ["filter_model_polo_spb", "chair"], // и
   ["filter_model_x_line_spb", "chair"]  // и
]`

  
**Почему просим возвращать name фильтра?**

У драйва при добавлении новых или удалении старых фильтров идишники фильтров могут меняться. Мы не хотим от этого зависеть.

```json5
{
  "state": {
    "bbox": [
      49.1,
      55.7,
      49.2,
      55.8
    ],
    "known_orders": [
    ],
    "location": [
      30.4,
      59.9
    ],
    "mode": "discovery",
    "pin": [
      49.1,
      55.7
    ],
    "screen": "drive",
    "zoom": 16.7,
    "size_hint": 322,
    "drive": {
       "filters": {
          "version": "v1",
          "conditions": [
             ["filter_model_kaptur_spb", "chair"],
             ["filter_model_polo_spb", "chair"],
             ["filter_model_x_line_spb", "chair"]
          ]
       }
    }
  }
}
```

В ответе ручки ничего не меняется, кроме того, что отфильтровываются не соответствующие фильтрам машины.
