

## Дизайн

[figma](https://www.figma.com/file/SwG2Ihisatfp2sdggUSZ5l/Карта?node-id=1446%3A82178)

![org-discovery](https://jing.yandex-team.ru/files/pavelnekrasov/org_discovery.png "Дискавери организаций")


## Flow 

#### Экран саджеста
В ответе ручки `/4.0/persuggest/v1/suggest` добавляются сетевые адреса в 
results (у них `action: map_search`):

```json5
{
  "lang": "rus",
  "log": "XXX",
  "method": "geosuggest",
  "position": [
    37.847603,
    55.653194
  ],
  "subtitle": {
    "text": "Магазин мебели · 5 организаций в Москве",
    "hl": []
  },
  "text": "ИКЕА",
  "title": {
    "text": "ИКЕА",
    "hl": [
      [
        0,
        4
      ]
    ]
  },
  "image_tag": "custom_suggest_map_search",
  "action": "map_search",
  "layers_context": {
    "type": "org_geosearch",
    "search_query": "{\"text\":\"ИКЕА\",\"what\":[{\"attr_name\":\"chain_id\",\"attr_values\":[\"57249144\"]}]}"
  }
}
```

Сетевые адреса будут возвращаться только для `type: b` и `mode: normal`.

По нажатию на сетевой адрес нужно открыть дискавери экран для организаций с 
контекстом `layers_context` из ответа ручки suggest (см. далее). 

### Экран discovery

#### Работа с layers
Все хождения в layers должны выполняться с `mode: <текущий режим приложения>, 
screen: discovery` и контекстом layers_context из ответа resuts[].layers_context.

Пример:
```json5
{
  "state": {
    "mode": "normal",
    "screen": "discovery",
    ...
  },
  "context": results[].layers_context,
  ...
}
``` 

На экране должен быть поддержан `optimal_view` и отображение ошибки 
`no_objects_message`. Также при отстутствии объектов присылается `no_object_subtitle`.

Если layers не отвечает, либо 500-тит, то нужно отобразить ошибку с текстом 
из `TODO` с кнопкой `Повторить`.


#### Экшн для открытия карточки организации
тут подробное описание карточки:
https://st.yandex-team.ru/TAXIBACKEND-31719#5f8fdace81de5807ef95af83 

```
"action": {
  "type": "organization_card",
  "id": {
    "type": "geosearch/qr",
    "value": "12312341"
  },
  "mode": "xxxx"
}
```





