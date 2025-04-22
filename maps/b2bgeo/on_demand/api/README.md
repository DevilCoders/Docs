[[toc]]

# О сервисе

Сервис предназначен для распределения заказов по курьерам доставки по запросу. Сервис подходит для использования компании если:
- У компании есть система, в которую попадают заказы. В этой же системе хранятся статусы заказа. Например, принят, готовится, готов, ждет отправки, отправлен, доставлен, закрыт.
- У компании есть либо самописное, либо купленное моб.приложение курьеров, откуда можно получать локацию. В этом же приложении курьеры меняют статусы заказа. У некоторых компаний курьер может отказаться принимать заказ.
- Самый главный принцип распределения заказа на курьера - время доставки нового заказа до клиента. При этом есть определенные нормы "справедливости" распределения заказов среди курьеров.
- Курьеры могут быть всех типов: авто/пеший/вело.

Для использования данного сервиса, пользователю (компании) необходимо:
- Загрузить всех своих курьеров в справочник ТС.
- Указать, какие из загруженных курьеров могут выполнять заказы в текущий момент.
- Отправлять актуальные позиции активных курьеров.
- Опрашивать сервис по назначениям на курьеров, соглашаться или отказываться от этих назначений.

Для распределения заказа на курьера пользователь готовит задание, которое представляет из себя список локаций, которые должен посетить курьер (то есть магазин/даркстор из которого курьер должен забрать товар, и точку доставки), и время прибытия в каждую локацию (как можно скорее, либо временное окно).
После загрузки задания пользователю предлагается назначение - выбранный для выполнения задания курьер. Пользователь может либо подтвердить назначение, либо отказаться от него. Во втором случае пользователю предлагается другой курьер, и так до тех пор, пока назначение не будет подтверждено.

Курьеры, на которых в данный момент назначен какой-то заказ, не могут получить новое назначение, чтобы получить новое назначение, предыдущее должно быть помечено выполненым. С этого момента курьер снова становится доступным для назначения.

# On-demand dispatch API

## Задания

### POST /on-demand/companies/<company_id>/tasks

Добавление задания в диспетчер.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Формат запроса

**Тело запроса**
| название поля | тип | описание |
|---|---|---|
| `tasks` | array of object | массив заданий для распределения |
| `tasks[].number` | string | идентификатор задания в системе пользователя |
| `tasks[].locations` | array of location | массив упорядоченных локаций для посещения курьером |
| `tasks[].locations[].*` |||
| `type` | enum | тип локации:<br>- `depots` - забрать заказ из склада<br>- `pickup` - забрать заказ из другой точки<br>- `delivery` - отвезти заказ в точку|
| `value` | object | расположение локации
| `value.depots` | array of objects | склады, с которых можно забрать товар; используется при `type == "depots"`
| `value.depots[].id` | string | идентификатор depot в справочнике
| `value.point` | object | координаты локации; используется при `type in ("pickup", "delivery")` |
| `value.point.lat` | number | широта |
| `value.point.lon` | number | долгота |
| `value.time` | object | желаемое время посещения локации; используется при `type in ("pickup", "delivery")` |
| `value.time.type` | enum | тип времени:<br>- `window` - по временному окну (требует указания `time.window`)<br>- `asap` - как можно скорее |
| `value.time.value` | object | временное окно; используется при `time.type == "window"` |
| `value.time.value.<start\|end>` | number | начало и конец временного окна в Unixtime |

**Пример**
```
{
    "tasks": [
        {
            "number": "my_task_identifier",
            "locations": [
                {
                    "type": "depots",
                    "value": {
                        "depots": [ {"id": "123"} ]
                    }
                },
                {
                    "type": "delivery",
                    "value": {
                        "point": {
                            "lat": 55.735525,
                            "lon": 37.642474
                        },
                        "time": {
                            "type": "asap"
                        }
                    }
                }
            ]
        }
    ]
}
```

#### Формат ответа

**Тело ответа**
| название поля | тип | описание |
|---|---|---|
| `tasks` | array of object | массив соответствий идентификаторов заданий в системе пользователя и в диспетчере |
| `tasks[].id` | string | идентификатор задания в диспетчере |
| `tasks[].number` | string | идентификатор задания в системе пользователя |

**Пример**
```
{
    "tasks": [
        {
            "id": "92911",
            "number": "my_task_identifier"
        }
    ]
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 400 | Invalid request body |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 422 | Request cannot be processed |
| 500 | Internal error |

### GET /on-demand/companies/<company_id>/tasks/<task_id>

Получение задания из диспетчера.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Формат ответа

**Тело ответа**
| название поля | тип | описание |
|---|---|---|
| `id` | string | идентификатор задания в диспетчере |
| `number` | string | идентификатор задания в системе пользователя |
| `locations[].*` |||
| `type` | enum | тип локации:<br>- `depots` - забрать заказ из склада<br>- `pickup` - забрать заказ из другой точки<br>- `delivery` - отвезти заказ в точку|
| `value` | object | расположение локации
| `value.depots` | array of objects | склады, с которых можно забрать товар; используется при `type == "depots"`
| `value.depots[].id` | string | идентификатор depot в справочнике
| `value.point` | object | координаты локации; используется при `type in ("pickup", "delivery")` |
| `value.point.lat` | number | широта |
| `value.point.lon` | number | долгота |
| `value.time` | object | желаемое время посещения локации; используется при  `type in ("pickup", "delivery")` |
| `value.time.type` | enum | тип времени:<br>- `window` - по временному окну (требует указания `time.window`)<br>- `asap` - как можно скорее |
| `value.time.value` | object | временное окно; используется при `time.type == "window"` |
| `value.time.value.<start\|end>` | number | начало и конец временного окна в Unixtime |

**Пример**
```
{
    "id": "92912",
    "number": "my_task_identifier",
    "locations": [
        {
            "type": "pickup",
            "value": {
                "point": {
                    "lat": 55.733974,
                    "lon": 37.587093
                },
                "time": {
                    "type": "window",
                    "value": {
                        "start": 1628154000,
                        "end": 1628190000,
                    }
                }
            }
        },
        {
            "type": "delivery",
            "value": {
                "point": {
                    "lat": 55.735525,
                    "lon": 37.642474
                },
                "time": {
                    "type": "asap"
                }
            }
        }
    ]
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Task is not found |
| 500 | Internal error |

### GET /on-demand/companies/<company_id>/tasks/<task_id>/assignment

Получение назначения для этого задания из диспетчера.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Формат ответа

**Тело ответа**
| название поля | тип | описание |
|---|---|---|
| `id` | string | идентификатор назначения в диспетчере |

**Пример**
```
{
    "id": "929123",
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 202 | Assignment is not yet created |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Task is not found |
| 500 | Internal error |

### DELETE /on-demand/companies/<company_id>/tasks/<task_id>

Удаление задания из диспетчера.
* Если назначение с заданием уже предложено курьеру, но ещё не принято, то оно будет помечено, как отмененное.
* Если назначение уже взято курьером, то:
    * если там есть другие задания, то текущее задание будет отменено, но остальные задания останутся;
    * если там нет других заданий, то назначение будет отменено.

NOTE: В реальности задание может быть не удалено, пока есть рабочие назначения, которые ссылаются на него, но мы перестанем его отдавать по этому пути.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |


#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Task is not found |
| 500 | Internal error |

## Назначения

### GET /on-demand/companies/<company_id>/assignments/<assignment_id>

Получение назначения для этого задания из диспетчера.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Формат ответа

**Тело ответа**
| название поля | тип | описание |
|---|---|---|
| `id` | string | идентификатор назначения в диспетчере |
| `status` | enum | статус текущего назначения:<br>- suggested - назначение предложено курьеру<br>- running - курьер работает над эти назначением<br>- rejected - предложение было отклонено курьером<br>- canceled - назначение было взято в работу, но потом отменено |
| `courier_id` | string | идентификатор курьера на этом назначении |
| `locations` | array of objects | массив локаций для посещения в этом назначении |
| `locations[].*` |||
| `type` | enum | тип локации:<br>- `depots` - забрать заказ из склада<br>- `pickup` - забрать заказ из другой точки<br>- `delivery` - отвезти заказ в точку|
| `value` | object | расположение локации
| `value.depots` | array of objects | склады, с которых можно забрать товар; используется при `type == "depots"`
| `value.depots[].id` | string | идентификатор depot в справочнике
| `value.point` | object | координаты локации; используется при `type in ("pickup", "delivery")` |
| `value.point.lat` | number | широта |
| `value.point.lon` | number | долгота |
| `tasks` | array of objects | массив задач этой локации |
| `tasks[].id` | string | идентификатор задачи |

**Пример**
```
{
    "id": "929123",
    "status": "suggested",
    "courier_id": "123",
    "locations": [
        {
            "type": "depots",
            "value": {
                "depots": [ {"id": "100"} ]
            },
            "tasks": [
                {
                    "id": "300"
                }
            ]
        },
        {
            "type": "pickup",
            "value": {
                "point": {
                    "lat": 55.733974,
                    "lon": 37.587093
                },
            },
            "tasks": [
                {
                    "id": "200"
                }
            ]
        },
        {
            "type": "delivery",
            "value": {
                "point": {
                    "lat": 55.735525,
                    "lon": 37.642474
                }
            },
            "tasks": [
                {
                    "id": "300"
                },
                {
                    "id": "200"
                }
            ]
        }
    ]
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 202 | Assignment is not yet created |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Task is not found |
| 500 | Internal error |

## Курьеры

Сущности курьеров будут использоваться из справочника

### GET /on-demand/companies/<company_id>/couriers/online

Получение всех курьеров справочника, участвующих в распределении

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| `apikey` | string | ключ для доступа к API |
| `page` | number | номер страницы в постраничном выводе |
| `per_page` | number | количество объектов на странице |

#### Формат ответа

**Тело ответа**
| название поля | типа/формат/допустимые значения | описание |
|---|---|---|
| `couriers` | array of objects |  |
| `couriers[].id` | string | идентификатор курьера в справочнике |

**Пример**
```
{
    "couriers": [
        {
            "id": "153"
        },
        {
            "id": "899"
        }
    ]
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 500 | Internal error |

### POST /on-demand/companies/<company_id>/couriers

Проставление статуса многих курьеров

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| `apikey` | string | ключ для доступа к API |

#### Формат ответа

**Тело запроса**
| название поля | типа/формат/допустимые значения | описание |
|---|---|---|
| `couriers` | array of objects |  |
| `couriers[].id` | string | идентификатор курьера в справочнике |
| `couriers[].status` | enum | статус курьера в on-demand:<br>- `online` - курьер участвует в распределении<br>- `offline` - курьер не участвует в распределении |

**Пример**
```
{
    "couriers": [
        {
            "id": "153",
            "status": "online"
        },
        {
            "id": "899",
            "status": "offline"
        }
    ]
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Couriers are not found |
| 500 | Internal error |


### GET/PATCH /on-demand/companies/<company_id>/couriers/<courier_id>

Получение/замена текущего статуса курьера

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| `apikey` | string | ключ для доступа к API |

#### Формат запроса/ответа

**Тело запроса/ответа**
| название поля | типа/формат/допустимые значения | описание |
|---|---|---|
| `status` | enum | статус курьера в on-demand:<br>- `online` - курьер участвует в распределении<br>- `offline` - курьер не участвует в распределении |

**Пример**
```
{
    "status": "online"
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Courier is not found |
| 500 | Internal error |

### GET /on-demand/companies/<company_id>/couriers/<courier_id>/suggestions

Получение предлагаемых назначений курьера на маршруты.

NOTE: Здесь же будут выдаваться точки притяжения для курьеров в будущем.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Формат ответа

**Тело ответа**
| название поля | тип | описание |
|---|---|---|
| `assignments` | array of objects | Предложения для курьера |
| `assignments[].id` | string | идентификатор назначения |

**Пример**
```
{
    "assignments":[ { "id": "3952" } ]
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Courier is not found |
| 500 | Internal error |

### POST /on-demand/companies/<company_id>/couriers/<courier_id>/suggestions/<assignment_id>/accept

Принятие назначения на маршрут, курьер считается занятым после этого вызова.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Courier or assignment is not found |
| 422 | Assignment is no longer available or is not suggested to the courier |
| 500 | Internal error |

### DELETE /on-demand/companies/<company_id>/couriers/<courier_id>/suggestions/<assignment_id>

Отклонение назначения на маршрут, курьер считается свободным после этого вызова, задания будут назначены на другого курьера.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Courier or assignment is not found |
| 422 | Assignment is no longer available or is not suggested to the courier |
| 500 | Internal error |

### POST /on-demand/companies/<company_id>/couriers/<courier_id>/assignments/<assignment_id>/complete

Выполнение уже взятого назначения, курьер освобождается если все его назначения выполнены.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Courier or assignment is not found |
| 422 | Assignment is no longer available or is not suggested to the courier |
| 500 | Internal error |

## Справочник

### POST /reference-book/companies/<company_id>/couriers/<courier_id>/push-positions

Отправка позиций курьера.

#### Параметры запроса

| название параметра | типа/формат/допустимые значения | описание |
|---|---|---|
| apikey | string | ключ для доступа к API |

#### Формат запроса

**Тело запроса**
| название поля | типа/формат/допустимые значения | описание |
|---|---|---|
| `positions` | array of objects | массив позиций |
| `positions[].*` | | |
| `accuracy` | number | точность GPS в метрах |
| `point` | object | текущие координаты курьера |
| `point.lat` | number | широта |
| `point.lon` | number | долгота |
| `timestamp` | number | временная метка в unixtime |

**Пример**
```
{
    "positions": [
        {
            "accuracy": 50,
            "point": {
                "lat": 55.735525,
                "lon": 37.642474
            }
            "timestamp": 1628258400
        }
    ]
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 400 | Invalid request body |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 404 | Courier is not found |
| 422 | New positions are older than previous ones or data is invalid |
| 500 | Internal error |


### POST/GET /reference-book/companies/<company_id>/depots

Аналогично ручкам /companies/<company_id>/depots, просто зеркало в reference-book, чтобы иметь консистентный API.

## Настройки компании

### GET/PATCH /on-demand/companies/<company_id>/settings

Получение/изменение настроек компании для on-demand-а
NOTE: Какие нужны настройки пока непонятно, мы ещё подумаем.

#### Параметры запроса

| название параметра | тип | описание |
|---|---|---|
| `apikey` | string | ключ для доступа к API |

#### Формат запроса/ответа

**Тело запроса/ответа**
| название поля | типа/формат/допустимые значения | описание |
|---|---|---|
| `quality` | enum | качество/скорость распределения on-demand:<br>- `low` - низкое качество, быстрое распределение новых заданий<br>- `medium` - среднее качество, более долгое распределение заданий |

**Пример**
```
{
    "quality": "low"
}
```

#### Коды ответа

| код ответа | |
|---|---|
| 200 | Success |
| 401 | Invalid apikey |
| 402 | Banned apikey |
| 403 | Request to this company is not allowed |
| 500 | Internal error |


## Сценарии использования

### Настройка справочника

```
$ curl -X POST "<api-prefix>/reference-book/companies/<company_id>/couriers?apikey=<APIKEY>" -d '[
        {
            "number": "4293-courier",
            "phone": "+78888888888",
        },
        {
            "number": "2344-courier",
            "phone": "+79999999999",
        }
    ]
$ curl -X POST "<api-prefix>/reference-book/companies/<company_id>/vehicles?apikey=<APIKEY>" -d '[
        {
            "number": "4293-veh",
            "name": "4293-name",
            "routing_mode": "driving"
        },
        {
            "number": "2344-veh",
            "name": "2344-name",
            "routing_mode": "driving"
        }
    ]
$ curl -X POST "<api-prefix>/reference-book/companies/<company_id>/link-courier-vehicle?apikey=<APIKEY>" -d '{
            "vehicle_id": "1",
            "courier_id": "1"
        }
$ curl -X POST "<api-prefix>/reference-book/companies/<company_id>/link-courier-vehicle?apikey=<APIKEY>" -d '{
            "vehicle_id": "2",
            "courier_id": "2"
        }
$ curl -X POST "<api-prefix>/reference-book/companies/<company_id>/depots?apikey=<APIKEY>" -d '[
        {
            "number": "my-depot",
            "address": "Moscow, ...",
            "lat": 55.734739,
            "lon": 37.643045
        }
    ]
```

### Проставление статуса online у курьеров, которые должны участвовать в распределении
```
$ curl "<api-prefix>/on-demand/companies/<company_id>/couriers/<courier_id>?apikey=<APIKEY>" -d '{
    "status": "online"
}'
```


### Получение прямо сейчас работающих в on-demand курьеров
```
$ curl "<api-prefix>/on-demand/companies/<company_id>/couriers/online?apikey=<APIKEY>"
```

### Координаты курьеров

Текущие координаты курьера необходимы, чтобы диспетчер мог рассчитать время приезда курьера на склад/в магазин за товаром.

```
$ curl -X POST "<api-prefix>/reference-book/companies/<company_id>/couriers/<courier_id>/push-positions?apikey=<APIKEY>" -d '{
    "positions": [
        {
            "accuracy": 50,
            "point": {
                "lat": 55.735525,
                "lon": 37.642474
            }
            "timestamp": 1628258400
        }
    ]'
```

### Работа с заданиями

**1. Добавление задания**

```
$ curl -X POST "<api-prefix>/on-demand/companies/<company_id>/tasks?apikey=<APIKEY>" -d '{...}'
{
    "tasks": [
        {
            "number": "my_task_identifier",
            "locations": [
                {
                    "type": "depots",
                    "value": {
                        "depots": [ {"id": "123"} ]
                    }
                },
                {
                    "type": "delivery",
                    "value": {
                        "point": {
                            "lat": 55.735525,
                            "lon": 37.642474
                        },
                        "time": {
                            "type": "asap"
                        }
                    }
                }
            ]
        }
    ]
}
```

**2. Получение решения**

Каждый курьер поллит диспетчер, пока не получит непустой список назначений, которые он может взять.

```
$ curl "<api-prefix>/on-demand/companies/<company_id>/couriers/<courier_id>/suggestions?apikey=<APIKEY>"
```

**3.a. Курьер соглашается с назначением**

Для подтверждения назначения необходимо его принять.

```
$ curl -X POST "<api-prefix>/on-demand/companies/<company_id>/couriers/<courier_id>/suggestions/<assignment_id>/accept?apikey=<APIKEY>"
```

**3.b. Курьер отказался от назначения**

Для отказа от назначения необходимо удалить назначение из предложенных.

```
$ curl -X DELETE "<api-prefix>/on-demand/companies/<company_id>/couriers/<courier_id>/suggestions/<assignment_id>?apikey=<APIKEY>"
```

После этого диспетчер снова попытается найти подходящего курьера. Курьер из отклонённого назначения в дальнейшем решении не участвует. Для получения нового назначения снова поллим метод из пункта 2. Задачу пересоздавать не нужно.

**4. Курьер завершает задание**

Когда курьер закончил выполнение задания, диспетчеру необходимо сообщить об этом, чтобы он мог использовать освободившегося курьера для дальнейших назначений. Для этого необходимо завершить назначение.

```
$ curl -X POST "<api-prefix>/on-demand/companies/<company_id>/couriers/<courier_id>/assignments/<assignment_id>/complete?apikey=<APIKEY>"
```
