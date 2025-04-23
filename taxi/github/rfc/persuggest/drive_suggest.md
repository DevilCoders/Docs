# Саджест для Драйва

### Дизайн

![drive-discovery](https://jing.yandex-team.ru/files/pavelnekrasov/drive_suggest_v2.jpg "Саджест Драйва")

### Клиентский флоу

#### Краткое описание

Флоу саджеста Драйва похож на флоу саджеста такси. Принципиальные отличия:
- все запросы в ручки persuggest выполняются с `state.current_mode = drive`.
- в ответе ручки finalsuggest в `services.drive` будет приходить информация о 
доступности сервиса Драйва и контекст для отображения машин Драйва на карте 
с помощью сервиса `layers`.
- получив `services.drive.layers_context` в ответе `finalsuggest`, должен быть 
выполнен вызов ручки `/4.0/layers/v2/objects` для отображения офферов на карте.


#### Расширение ручек persuggest
Все запросы в persuggest должны выполняться с `state.current_mode = drive`.
В ответ ручки finalsuggest в режиме Драйва добавляется объект `drive` в `services`.

Если есть офферы Драйва , то формат ответа такой:
```json5
{
  ...
  "services": {
    ...
    "drive": {
      "available": true,
      "layers_context": {
        "type": "drive_fixpoint_offers",
        "src": [37.5, 55.5],
        "dst": [38.5, 56.5],
        "offer_count_limit": 5,
        ...
      }
    }
  }
}
``` 
 `layers_context` приходит только при запросе для точки B (`"type": "b"`).
 Получив  `layers_context` в ответе finalsuggest, должен быть 
выполнен вызов ручки `/4.0/layers/v2/objects` для отображения офферов на карте
(похожий флоу в шорткате Драйва).
 
Если нет офферов Драйва, то формат ответа такой:
```json5
{
  ...
  "services": {
    ...
    "drive": {
      "available": false,
      "unavailability_reason": {
        "message": "Нет доступных машин",
        "code": "no_cars"
      }
    }
  }
}
``` 

Формат `services.drive`
```yaml
DriveService:
    type: object
    additionalProperties: false
    properties:
        available:
            type: boolean
        layers_context:
            type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: |
                json определяется из кодогенерации сервиса layers
        unavailability_reason:
            type: object
            additionalProperties: false
            properties:
                message:
                    type: string
                code:
                    type: string
                    enum:
                      - no_experiment
                      - not_portal
                      - bad_request
                      - no_drive_response
                      - not_registered
                      - no_service
                      - no_cars
                      - bad_dst
                      - other
            required:
              - message
              - code
    required:
      - available
```

#### Порядок вызова ручек (нет активного заказа в Драйве)

**Все запросы persuggest** выполняются для точки `B` с 
`type=b`. Во всех запросах в `state.fields` указывается текущая точка `A`.

При нажатии кнопки Драйва делается запрос `/4.0/persuggest/v1/zerosuggest` с 
- `type=b`
- `position` - текущая координата пина

Запрос в layers при этом не делается, т.е. просто открывается карточка саджеста. 

По аналогии с таксишным саджестом отображается ответ `/4.0/persuggest/v1/zerosuggest` 
пока не введен адрес в строке.

При вводе адреса дергается ручка 
`/4.0/persuggest/v1/suggest`. 

Если выбран адрес, у которого `action=search` либо адрес из `zerosuggest`, то 
дергается ручка `finalsuggest` с `action=finalize`. Если в ответе `finalsuggest`:
 `services.drive.available == false`, то выводится сообщение об ошибке 
 (**слои не дергаются**) и 
 в зависимости от кода ошибки (`reason_code`) нужно сделать действие:
 
- `no_service / no_cars` — кнопка «поехать на такси». прокидывать на summary с точками А и Б, выбирать тариф из personalstate
- `bad_dst` — кнопка «поменять адрес». возвращает в саджест, поле ввода пустое
- `no_experiment / not_portal / bad_request / no_drive_response / not_registered / other` — «вернуться на главный»
 
 
 Если `services.drive.available == true`, 
 то открывается экран с офферами Драйва (см. описание далее).

При нажатии кнопки `Карта` открывается карта выбора точки `B` (аналогично 
таксишному выбору точки `B`). В слоях выставляется `screen=choose_b, mode=drive`.

На каждый сдвиг пина дергается `finalsuggest`  
с `action=pin_drop` и `sticky=false`. Если в ответе `finalsuggest` 
`services.drive.available == false`,
то выводится сообщение об ошибке из ответа и на кнопку `Готово` нельзя нажать.
 
При нажатии на кнопку `Готово` открывается экран с офферами Драйва (см. описание 
далее).

#### Экран с выбором офферов Драйва
Экран открыватся после ответа `finalsuggest` с `service.drive.available==true`.
Действия аналогичны действия по нажатию на шорткат Драйва 
(https://github.yandex-team.ru/taxi/rfc/blob/master/drive-shortcut/shortcut.md)
Идем в `/4.0/layers/v2/objects` с контекстом 
`layers_context` из ответа `finalsuggest`  и `"mode": "drive"`, `"screen": "main"`.
 Контекст должен быть передан 
в корне запроса в поле `"context"` **as-is** (т.е. при изменении формата 
контекста не нужно изменять клиентов)

Пример запроса:
 ```json
 {
  "context": {
    "type": "drive_fixpoint_offers",
    "src": [
      37.880318157794707,
      55.754543995739407
    ],
    "dst": [
      37.6425634912552,
      55.73475967775757
    ],
    "offer_count_limit": 5,
    "preferred_car_number": "м668от799",
    "previous_offer_ids": [
       "offer_1",
       "offer_2"
    ]
  },
  "state": {
    "bbox": [
      37.868574701220695,
      55.73813247694166,
      37.892082162849164,
      55.762261637963604
    ],
    "location": [
      37.88048333333333,
      55.755160000000004
    ],
    "mode": "drive",
    "screen": "main",
    "zoom": 14.60303
  }
}
 ```
 
layers вернет все машинки на карте с прогруженными офферами. 
Клиент делает объект `selected_object_id` выбранным (как будто на него нажал 
пользователь) и центрирует карту на выбранном объекте с учетом положения пользователя и пешего маршрута.
 При выборе объекта открывается карточка драйва из SDK с 
прогруженным оффером. При нахождении на экране с машинками фикса
все хождения в layers должны быть с контекстом.  

В случае пустого ответа layers нужно отобразить ошибку из поля 
optimal_view.no_objects_message и кнопку  
 «поехать на такси», по которой прокидывать на summary с точками А и Б, выбирать тариф из personalstate.

Если ручка objects не отвечает, нужно показывать шиммеринг и по таймауту 
отобразить стандартное сообщение об ошибке и кнопку  «поехать на такси», 
по которой прокидывать на summary с точками А и Б, выбирать тариф из personalstate.

Такой же подход нужно повторить при нажатии на шорткат Драйва.


#### Бронирование машины
После брони машины на экране с выбором офферов драйва нужно поменять экран 
в слоях на `totw` (`mode` остается `drive`) и убрать `context` из запросов.

#### Активный заказ
Если есть активный заказ в Драйве, то по нажатию на кнопку Драйва нужно 
открыть карту и выставить 
`screen=totw, mode=drive` в слоях (без `context`)


#### Резюме по слоям

Есть активный заказ:
1. По нажатию на кнопку `Драйв` выставляем (`screen=totw, mode=drive`)

Нет активного заказа:
1. По нажатию на кнопку `Драйв` слои не дёргаются 
2. Нажимаем “карта” в саджесте драйва: (`screen=choose_b, mode=drive`)
3. finalsuggest сказал, что сервис недоступен - не дергаем слои.
4. finalsuggest сказал, что сервис доступен: `screen=main, mode=drive` + контекст из последнего ответа finalsuggest
5. После брони машины - `screen=totw, mode=drive` без контекста.



### Альтернативный подход без финализации адресов саджеста

*Пока не делаем, т.к. много правок на клиентах*

В этом подходе предлагается ускорить интерфейс за счет того, что не дергается 
ручка `finalsuggest` при выборе адреса из `zerosuggest` и из `suggest`-а.

Из `services.drive` убираем `layers_context` и добавляем его в каждый адрес 
из `results` ответа саджестовых ручек.

Формат ответа `finalsuggest` для точки `A` не меняется. Для точки B
 поле `service.drive.available` всегда `true` (как в таксишном саджесте).

Для точки `B` адреса из `results` ручек `suggest`, `zerosuggest` и `finalsuggest`
расширяются полем `drive_layers_context`. По нажатию на адрес с `drive_layers_context`
должен быть открыт экран с выбором офферов Драйва (с контекстом `drive_layers_context` из 
адреса)
