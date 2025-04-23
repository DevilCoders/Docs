Детали, дизайн: https://st.yandex-team.ru/TAXIBACKEND-34819

В драйве существуют такие сущности, как кластеры.
В кластер попадают машины, которые [оказались внутри bbox-а соответствующего кластера](https://st.yandex-team.ru/TAXIBACKEND-34682#605e30afab81a32be45c351b).

Пример кластера (из https://paste.yandex-team.ru/4226897):
```json5
{
    "center": "37.53282341 55.75209191",
    "count": 19,
    "filters": [
        {
            "count": 1,
            "id": 72
        },
        {
            "count": 18,
            "id": 100
        },
        {
            "count": 18,
            "id": 148
        }
    ],
    "icon": "https://carsharing.s3.yandex.net/drive/city-parking.png",
    "id": 27406,
    "location": {
        "lat": 55.75209191,
        "lon": 37.53282341
    },
    "message": "Подземная парковка",
    "title": "Москва-Сити"
}
```

Машины, входящие в кластер, возвращаются как обычно, но помечаются как лежащие в кластере:
```json5
{
    "cluster": 27406, // id парковки в Сити
    "filters": [
        100,
        148
    ],
    "location": {
        "course": 184,
        // у машины есть собственная позиция, лежащая где-то внутри полигона:
        "lat": 55.75204308,
        "lon": 37.53306978
    },
    "model_id": "vw_polo",
    "number": "в919хт750",
    "parking_place": "oko_parking|240A", // также может прийти парковочное место
    "sf": [
        68,
        83
    ],
    "telematics": {
        "fuel_distance": 429,
        "fuel_level": 78
    },
    "view": 0
},
```

Проблема заключается в том, что при запросе машин по bbox-у вернутся только те, которые
попадают в него, без учета того, есть ли другие машины, попавшие в кластер.

Проще говоря, запрос по bbox-у может откусить только часть кластера, тогда как мы хотим
гарантировать, что пользователю вернутся все машины в карточке кластера (или списке
самокатов с парковки).

В тикете https://st.yandex-team.ru/TAXIBACKEND-34813#605b02bfc600871661d8676d предлагался
такой формат для объекта кластера:

```json5
{
  "id": "3264102698",
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [
      30.404316,
      59.958842
    ]
  },
  "properties": {
    "type": "scooter_parking",
    "style": {
      "image": {
        "name": "image_stop",
        "type": "tag",
        "anchor": [
          0.5,
          0.69
        ]
      },
      "selected_image": {
        "name": "image_stop",
        "type": "tag",
        "anchor": [
          0.5,
          0.69
        ]
      }
    },
    "options": [
      {
        "on": "tap",
        "actions": [
          {
            "type": "pick_scooter_parking",
            "car_numbers": [
              "б515вг357",
              "a324fd123",
              "g543вa777",
              "ф151ка178"
            ]
          }
        ]
      },
      {
        "on": "tap",
        "actions": [
          {
            "dst": {
              "position": [
                30.404316,
                59.958842
              ]
            },
            "type": "walk_route"
          }
        ]
      }
    ],
    "display_settings": {
      "zooms": [
        15,
        21
      ],
      "z_index": 110
    }
  }
}
```

Предлагается убрать из action перечисление номеров и заменить его на следующий формат:
```json5
{
  "type": "pick_scooter_parking",
  "cluster_context": { // Произвольного формата объект, который нужно передать дальше
    "type": "cluster_complete_request",
    "cluster_id": 1337
  }
}
```

Полный ответ:
<details>
  <summary>Тык</summary>

  ```json5
  {
    "geometry": {
      "coordinates": [
        13.37,
        42.42
      ],
      "type": "Point"
    },
    "id": "drive__cluster__1337",
    "properties": {
      "appmetrica_prefix": "DriveCluster",
      "display_settings": {
        "z_index": 100.0,
        "zooms": [
          17.0,
          21.0
        ]
      },
      "options": [
        {
          "actions": [
            {
              "type": "drive_select_from_cluster",
              "cluster_context": {
                "type": "cluster_complete_request",
                "cluster_id": 1337
              }
            }
          ],
          "on": "tap"
        },
        {
          "on": "tap",
          "actions": [
            {
              "dst": {
                "position": [
                  13.37,
                  42.42
                ]
              },
              "type": "walk_route"
            }
          ]
        }
      ],
      "overlays": [
        {
          "anchor": [
            0,
            1
          ],
          "attributed_text": {
            "items": [
              {
                "color": "#0000FF",
                "font_size": 13,
                "font_weight": "medium",
                "text": "3", // Число машинок/самокатов в кластере
                "type": "text"
              }
            ]
          },
          "shape": "rounded_rectangle",
          "show_states": [
            "unselected",
            "selected"
          ],
          "zooms": [
            17.0,
            21.0
          ]
        }
      ],
      "style": {
        "autoscale": {
          "max_scale": 1.0,
          "max_zoom": 19.0,
          "min_scale": 0.6,
          "min_zoom": 15.0,
          "type": "linear"
        },
        "image": {
          "name": "superapp_drive_cluster_bubble",
          "type": "tag"
        }
      },
      "type": "drive"
    },
    "type": "Feature"
  }
  ```
</details>

По тапу нужно будет сделать новый запрос за списком ТС в кластере в новую ручку:
```json5
// POST /4.0/layers/v1/cluster
{
  "context": {
    "type": "cluster_complete_request",
    "cluster_id": 1337
  },
  // Кажется, можно обойтись без него, но на всякий случай:
  "state": {
    "bbox": [
      37.5,
      55.6,
      37.6,
      55.7
    ],
    "drive": {
      "demo_mode": true
    },
    "known_orders": [
    ],
    "location": [
      37.6,
      55.7
    ],
    "mode": "drive",
    "pin": [
      37.6,
      55.7
    ],
    "screen": "discovery",
    "zoom": 12.5
  }
}
```

В ответ будет приходить список ТС и базовая информация по кластеру:
```json5
{
  "title": {
    "items": [
      {
        "type": "text",
        "text": "Шереметьево",
        "font_size": 24,
        "color": "21201F"
      }
    ]
  },
  "subtitle": {
    "items": [
      {
        "type": "text",
        "text": "Парковка у терминала D · 3 машины",
        "font_size": 13,
        "color": "9E9B98"
      }
    ]
  },
  // Также по дизайну есть окно поиска "Номер или модель машины"
  // и "Рядом не нашлось машин с таким номером", если отфильтровать не получилось,
  // но, кажется, это клиентская логика.
  "car_details": [
    {
      "image": "https://carsharing.s3.yandex.net/drive/car-models/creta/creta-large-norm.png",
      "location": [
        37.55,
        55.75
      ],
      "name": "Hyundai Creta",
      "number": "н587ху750",
      "parking_place": "240A"
    },
    {
      "image": "https://carsharing.s3.yandex.net/drive/car-models/vw_polo/vw-polo-side-2-kaz_large.png",
      "location": [
        37.5,
        55.7
      ],
      "name": "Volkswagen Polo",
      "number": "о027ов799"
    },
    {
      "image": "https://carsharing.s3.yandex.net/drive/car-models/renault_kaptur/renault-kaptur-side-2-kaz_large.png",
      "location": [
        37.6,
        55.8
      ],
      "name": "Renault Kaptur",
      "number": "т577нх799"
    }
  ],
  /* По старому формату также передавались номера машин массивом, но предлагается теперь так не делать
  "car_numbers": [
    "н587ху750",
    "о027ов799",
    "т577нх799"
  ],
  */
}
```
