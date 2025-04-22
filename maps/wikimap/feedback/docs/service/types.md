# Список типов фидбека

Тип фидбека задаётся тройкой полей `(form_id, question_id, answer_id)` из [OriginalTask](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/original-task.json). Данные самого фидбека пережаются в соответствующих объектах в `question_context` и `answer_context`.

## Допустимые значений form_id & question & answer

| question_id       | answer_id          | form_id      | question_context                                           | answer_context                                             | Значение и формат                                                                                              |
| ----------------- | ------------------ | ------------ | ---------------------------------------------------------- | ---------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| other             | comment            | Любое        | —                                                          | —                                                          | Комментарий в свободной форме<br/><br/>Используется поле `message`                                             |
| other             | toponym            | other        | —                                                          | other (поле `text` обязательно)                            | Комментарий в свободной форме                                                                                  |
| other             | auto               | other        | —                                                          | other (поле `text` обязательно)                            | Комментарий в свободной форме                                                                                  |
| other             | bicycle            | other        | —                                                          | other (поле `text` обязательно)                            | Комментарий в свободной форме                                                                                  |
| other             | masstransit        | other        | —                                                          | other (поле `text` обязательно)                            | Комментарий в свободной форме                                                                                  |
| other             | truck              | other        | —                                                          | other (поле `text` обязательно)                            | Комментарий в свободной форме                                                                                  |
| wrong_address     | report_address     | toponym      | toponym (<a href=#toponym_address_example>адрес</a>)       | toponym (<a href=#toponym_address_example>адрес</a>)       | Указание другого адреса                                                                                        |
| add_object        | entrance           | toponym      | —                                                          | entrance (<a href=#entrance_example>вход</a>)              | Добавление подъезда у топонима                                                                                 |
| add_object        | gate               | toponym      | —                                                          | toponym (<a href=#toponym_example>объект</a>)              | Добавить проход/проезд в заборе                                                                                |
| add_object        | toponym            | toponym      | —                                                          | toponym (<a href=#toponym_address_example>адрес</a>)       | Добавить адрес<br/><br/>Поле `message` обязательно                                                             |
| add_object        | fence              | toponym      | —                                                          | fence   (<a href=#fence_context>забор</a>)                 | Добавить забор                                                                                                 |
| add_object        | road               | toponym      | —                                                          | (deprecated) toponym (<a href=#toponym_example>объект</a>) | Добавить дорогу                                                                                                |
| add_object        | road               | toponym      | —                                                          | road (<a href=#road_example>дорога</a>)                    | Добавить дорогу                                                                                                |
| add_object        | barrier            | toponym      | —                                                          | toponym (<a href=#toponym_example>объект</a>)              | Добавить шлагбаум                                                                                              |
| add_object        | stop               | toponym      | —                                                          | toponym (<a href=#toponym_example>объект</a>)              | Добавить остановку                                                                                             |
| add_object        | parking            | toponym      | —                                                          | parking (<a href=#parking_context>парковка</a>)            | Добавить парковку                                                                                              |
| add_object        | crosswalk          | toponym      | —                                                          | toponym (<a href=#toponym_example>объект</a>)              | Добавить пешеходный переход                                                                                    |
| add_object        | other              | toponym      | —                                                          | toponym (<a href=#toponym_example>объект</a>)              | Добавить объект                                                                                                |
| add_object        | settlement_scheme  | toponym      | —                                                          | —                                                          | Добавить схему СНТ/дачного посёлка <br/><br/>Данные - фото и комментарий пользователя - приходят без контекста |
| approve_object    | barrier            | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Подтвердить существование и расположение шлагбаума                                                             |
| approve_object    | crosswalk          | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Подтвердить существование и расположение пешеходного перехода                                                  |
| approve_object    | entrance           | toponym      | entrance (<a href=#entrance_example>вход</a>)              | —                                                          | Подтверждение подъезда у топонима                                                                              |
| approve_object    | fence              | toponym      | fence    (<a href=#fence_context>забор</a>)                | —                                                          | Подтвердить существование и расположение забора                                                                |
| approve_object    | gate               | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Подтвердить существование и расположение калитки                                                               |
| approve_object    | parking            | toponym      | parking (<a href=#parking_context>парковка</a>)            | —                                                          | Подтвердить существование и расположение парковки                                                              |
| approve_object    | road               | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Подтвердить существование дороги                                                                               |
| approve_object    | address            | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Подтвердить корректность адреса                                                                                |
| wrong_entrance    | report_location    | toponym      | entrance (<a href=#entrance_example>вход</a>)              | entrance (<a href=#entrance_example>вход</a>)              | Подъезд/парадная указан неверно (Вход указан неверно)                                                          |
| wrong_entrance    | report_entrance    | toponym      | entrance (<a href=#entrance_example>вход</a>)              | entrance (<a href=#entrance_example>вход</a>)              | Подъезд/парадная указан неверно (Вход указан неверно) и/или добавление/изменение названия                      |
| wrong_entrance    | not_found          | toponym      | entrance (<a href=#entrance_example>вход</a>)              | —                                                          | Подъезд/парадная указан неверно (Входа здесь нет)                                                              |
| wrong_name        | report_name        | toponym      | toponym (<a href=#toponym_example>объект</a>)              | toponym (<a href=#toponym_example>объект</a>)              | Добавить/изменить название места (пример — добавить название озера, реки)<br/><br/>Поле `message` обязательно  |
| wrong_name        | report_name        | toponym      | stop (<a href=#stop_context>объект</a>)                    | stop (<a href=#stop_context>объект</a>)                    | Добавить/изменить название остановки                                                                           |
| wrong_location    | report_location    | toponym      | toponym (<a href=#toponym_example>объект</a>)              | toponym (<a href=#toponym_example>объект</a>)              | Местоположение топонима указано неверно                                                                        |
| wrong_location    | report_location    | toponym      | stop (<a href=#stop_context>объект</a>)                    | stop (<a href=#stop_context>объект</a>)                    | Местоположение остановки указано неверно                                                                       |
| wrong_barrier     | report_location    | toponym      | toponym (<a href=#toponym_example>объект</a>)              | toponym (<a href=#toponym_example>объект</a>)              | Местоположение шлагбаума указано неверно                                                                       |
| wrong_gate        | report_location    | toponym      | toponym (<a href=#toponym_example>объект</a>)              | toponym (<a href=#toponym_example>объект</a>)              | Местоположение калитки указано неверно                                                                         |
| wrong_subway      | report_subway      | toponym      | —                                                          | entrance (<a href=#toponym_example>вход</a>)               | Местоположение или имя станции метро или входа в метро указано неверно<br/><br/>Поле `center_point` или `name` обязательно.                                                                         |
| wrong_subway      | other              | toponym      | —                                                          | —                                                          | Что-то не так со станцией метро |
| remove_object     | toponym            | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Удалить объект с карты  <br/><br/>Поле `message` обязательно                                                   |
| remove_object     | toponym            | toponym      | stop (<a href=#stop_context>объект</a>)                    | —                                                          | Удалить остановку с карты                                                                                      |
| wrong_barrier     | not_found          | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Удалить шлагбаум с карты<br/><br/>Поле `message` обязательно                                                   |
| wrong_gate        | not_found          | toponym      | toponym (<a href=#toponym_example>объект</a>)              | —                                                          | Удалить калитку с карты <br/><br/>Поле `message` обязательно                                                   |
| wrong_subway      | not_found          | toponym      | —                                                          |  —                                                          | Здесь нет станции метро или входа в метро |
| add_object        | entrance           | organization | company (<a href=#sprav_entrance_example>вход в орг-ю</a>) | company (<a href=#sprav_entrance_example>вход в орг-ю</a>) | Добавление подъезда у организации.                                                                             |
| wrong_entrance    | report_location    | organization | company (<a href=#sprav_entrance_example>вход в орг-ю</a>) | company (<a href=#sprav_entrance_example>вход в орг-ю</a>) | Неправильное расположение входа у организации (известно куда)                                                  |
| wrong_entrance    | not_found          | organization | company (<a href=#sprav_entrance_example>вход в орг-ю</a>) | company (<a href=#sprav_entrance_example>вход в орг-ю</a>) | Неправильное расположение входа у организации (неизвестно куда).                                               |
| wrong_information | report_information | organization | company (<a href=#sprav_example>организация</a>)           | company (<a href=#sprav_example>организация</a>)           | Неверная информация об организации                                                                             |
| add_object        | organization       | organization | —                                                          | company (<a href=#sprav_example>организация</a>)           | Добавление организации                                                                                         |
| opened            | report_open        | organization | company (<a href=#sprav_closed>статус орг-и</a>)           | company (<a href=#sprav_closed>статус орг-и</a>)           | Организация открыта                                                                                            |
| closed            | permanent          | organization | company (<a href=#sprav_closed>статус орг-и</a>)           | company (<a href=#sprav_closed>статус орг-и</a>)           | Организация закрыта навсегда                                                                                   |
| closed            | temporary          | organization | company (<a href=#sprav_closed>статус орг-и</a>)           | company (<a href=#sprav_closed>статус орг-и</a>)           | Организация временно закрыта                                                                                   |
| closed            | probably           | organization | company (<a href=#sprav_closed>статус орг-и</a>)           | company (<a href=#sprav_closed>статус орг-и</a>)           | Возможно, организация закрыта                                                                                  |
| closed            | moved              | organization | company (<a href=#sprav_closed>статус орг-и</a>)           | company (<a href=#sprav_closed>статус орг-и</a>)           | Организация переехала                                                                                          |
| wrong_route       | report_route       | route        | route (q, <a href=#route_question_context>маршрут</a>)     | route (a, <a href=#route_answer_context>препятствия</a>)   | Исправление маршрута                                                                                           |
| wrong_lines       | report_lines       | toponym      | stop (<a href=#stop_context>остановка</a>)                 | stop (<a href=#stop_context>остановка</a>)                 | Исправление списка маршрутов на остановке                                                                      |
| add_object        | provider           | toponym      | —                                                          | provider (<a href=#provider_context>провайдер</a>)         | Добавить интернет-провайдера для здания                                                                        |

На вики: (устаревшее) [описание с примерами форм](https://wiki.yandex-team.ru/maps/feedback/qa/).

## Примеры

### Пример question_context & answer_context топонима <div id=toponym_address_example></div>

Полная схема: [toponym.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/toponym.json)

```json
{
  "toponym": {
    "address": [
      {
        "kind": "street",
        "name": "Кастанаевская улица"
      },
      {
        "kind": "house",
        "name": "30к1"
      }
    ],
    "center_point": {
      "lat": 55.73736,
      "lon": 37.486481
    }
  }
}
```

### Пример question_context & answer_context объекта <div id=toponym_example></div>

Полная схема: [toponym.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/toponym.json)

```json
{
  "toponym": {
    "name": "asdfasdf", // Опциональное поле
    "center_point": {
      "lat": 55.738803742131125,
      "lon": 37.59734473872754
    }
  }
}
```

### Пример question_context & answer_context подъезда <div id=entrance_example></div>

Полная схема: [entrance.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/entrance.json)

```json
{
  "entrance": {
    "name": "2",
    "center_point": {
      "lat": 55.738803742131125,
      "lon": 37.59734473872754
    }
  }
}
```

### Пример answer_context организации. Добавление подъезда <div id=sprav_entrance_example></div>

Полная схема: [sprav-company.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/sprav-company.json)

Только лишь поле `entrance` из <a href=#sprav_example>общей информации об организации</a>.

```json
{
  "company": {
    "entrances": [
      {
        "name": "main",
        "center_point": {
          "lat": 55.80436280112614,
          "lon": 37.490062957720085
        }
      }
    ]
  }
}
```

### Пример answer_context организации. Добавление изменение статуса закрытости <div id=sprav_closed></div>

Полная схема: [sprav-company.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/sprav-company.json)

Только лишь поле `status` из <a href=#sprav_example>общей информации об организации</a>.

```json
{
  "company": {
    "status": "closed_permanently"
  }
}
```

### Пример question_context & answer_context организации <div id=sprav_example></div>

Полная схема: [sprav-company.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/sprav-company.json)

```json
{
  "company": {
    "name": "Деловой центр Диапазон",
    "urls": [
      "http://business-center-diapazon.ru/",
      "http://www.bc-diapason.ru/"
    ],
    "hours": [
      {
        "breaks": [
          {
            "end_time": 840,
            "start_time": 780
          }
        ],
        "end_time": 1140,
        "start_time": 600,
        "day_of_week": "Monday"
      },
      {
        "breaks": [
          {
            "end_time": 840,
            "start_time": 780
          }
        ],
        "end_time": 1140,
        "start_time": 600,
        "day_of_week": "Tuesday"
      },
      {
        "breaks": [
          {
            "end_time": 840,
            "start_time": 780
          }
        ],
        "end_time": 1140,
        "start_time": 600,
        "day_of_week": "Wednesday"
      },
      {
        "breaks": [
          {
            "end_time": 840,
            "start_time": 780
          }
        ],
        "end_time": 1140,
        "start_time": 600,
        "day_of_week": "Thursday"
      },
      {
        "breaks": [
          {
            "end_time": 840,
            "start_time": 780
          }
        ],
        "end_time": 1140,
        "start_time": 600,
        "day_of_week": "Friday"
      }
    ],
    "status": "closed_unknown",
    "emails": [],
    "phones": [
      "+7 (999) 768-71-04"
    ],
    "address": "Россия, Москва, 1-й Волоколамский проезд, 10, стр. 1",
    "entrances": [
      {
        "name": "main",
        "center_point": {
          "lat": 55.803215,
          "lon": 37.490647
        }
      }
    ],
    "coordinates": {
      "lat": 55.803317,
      "lon": 37.490735
    },
    "rubric_names": [
      "Бизнес-центр"
    ]
  }
}
```

### Пример question_context маршрута <div id=route_question_context></div>

Полная схема: [route-question-context.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/route-question-context.json)

```json
{
  "route": {
    "travel_mode": "pedestrian",
    "traffic_jams": false,
    "way_points": [
      {"lon": 37.588461580598135, "lat": 55.73387438556429},
      {"lon": 37.58926969774817, "lat": 55.73381419716051}
    ],
    "uri": "ymapsbm1://route/driving/0LfQtNC10YHRjCDQsdGD0LTQtdGCINC-0L_QuNGB0LDQvdC40LUg0LzQsNGA0YjRgNGD0YLQsA",
    "encoded_points": "4o89AuhwUgMzAAAA3____yQAAADo____PAEAADX___87AAAA2v___3UAAAC0____6QAAAG7___9CAAAA2P___7MAAACR____NQAAAN____8=",
    "segments": [{
      "from": {"lon": 37.588461580598135, "lat": 55.73387438556429},
      "to": {"lon": 37.58926969774817, "lat": 55.73381419716051},
      "travel_mode": "pedestrian"
    }]
  }
}
```

### Пример answer_context - фидбек на препятствие <div id=route_answer_context></div>

Полная схема: [route-answer-context.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/route-answer-context.json)

```json
{
  "route": {
    "errors": [{
      "point": {"lon": 37.588461580598135, "lat": 55.73387438556429},
      "type": "obstruction"
    }],
    "segments": [{
      "points": [
        {"lon": 37.588461580598135, "lat": 55.73387438556429},
        {"lon": 37.58926969774817, "lat": 55.73381419716051}
      ],
      "travel_mode": "pedestrian"
    }]
  }
}
```

### Пример question_context & answer_context парковки <div id=parking_context></div>

[Пример](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/tests/examples_tests/parking-context.json)

Полная схема: [parking-context.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/parking-context.json)

### Пример question_context & answer_context остановки <div id=stop_context></div>

Полная схема: [stop.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/stop.json)

```json
{
  "stop": {
    "center_point": {
      "lat": 55.73736,
      "lon": 37.486481
    },
    "uri": "ymapsbm1://transit/stop?id=stop__10125314",
    "lines": [
      {
        "uri": "ymapsbm1://transit/line?id=239_60_bus_roadconssochi",
        "threads": [
          {
            "threadId": "239B_60_bus_roadconssochi"
          }
        ]
      },
      {
        "uri": "ymapsbm1://transit/line?id=3332698775",
        "threads": [
          {
            "threadId": "333270261"
          }
        ]
      }
    ]
  }
}
```


### Пример question_context & answer_context забора <div id=fence_context></div>

[Пример](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/tests/examples_tests/fence-context.json)

Полная схема: [fence-context.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/fence-context.json)

### Пример answer_context провайдера <div id=provider_context></div>

Полная схема: [provider-context.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/provider-context.json)

```json
{
  "provider": {
    "name": "Ростелеком",
    "site_url": "https://rt-tariff.ru/",
    "text": "Ростелеком-Раменки",
    "uri": "ymapsbm1://org?oid=42"
  }
}
```

### Пример answer_context дороги <div id=road_example></div>

Полная схема: [road-context.json](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/feedback/api/schemas/v1/definitions/road-context.json)

```json
{
  "road": {
    "name": "улица Поисковая",
    "center_point": {
      "lat": 55.73736,
      "lon": 37.486481
    },
    "points": [
      {"lon": 37.588461580598135, "lat": 55.73387438556429},
      {"lon": 37.58926969774817, "lat": 55.73381419716051}
    ]
  }
}
```
