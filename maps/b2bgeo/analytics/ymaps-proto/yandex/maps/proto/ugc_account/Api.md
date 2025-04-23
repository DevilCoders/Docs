## Frontoffice api
* **Фронтофис Maps UGC Account** - часть [**Maps UGC Account**][Readme], в которую приходят пользовательские запросы из ui.
* abc: https://abc.yandex-team.ru/services/maps-core-ugc-account/
* Исходники: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/ugc/account

### Request requirements
Each request must be pefrormed with TVM `ServiceTicket` and `UserTicket`.

### Headers
* `X-Ya-Service-Ticket`
* `X-Ya-User-Ticket`
* Accept: `application/x-protobuf`(default) or `text/x-protobuf`


### Response codes
| HTTP code | Response | Explanation |
|---|---|---
| 200 Ok | Proto for GET methods, empty for PUT ||
| 400 Bad Request |  | Request parameters malformed |
| 401 Unauthorized |  | No valid user or service ticket |
| 403 Forbidden |  | User does not have access to this object |
| 404 Not Found |  | Handler or assignment id not found |
| 410 Gone |  | Assignment or contribution with given id is removed |
| 429 Too Many Requests  |  | Rps quota exceeded |
| 500 Internal Server Error |  | Contact developers |


### Paging

Сделан для условно бесконечной ленты.
* `base_id`, Optional, id объекта в ленте, задаёт позицию в отранжированной ленте, относительно которой сервер формирует ответ
* `before_limit`, Optional, количество объектов, которые нужно вернуть перед объектом _base_id_, не используется без параметра _base_id_
* `after_limit`, Optional, количество объектов, которые нужно вернуть после объекта _base_id_, если не задавать _base_id_, то сервер вернёт задания из начала отранжированного списка

#### Сценарии
Пусть сервер знает ленту, которая состоит из объектов 100, 99, 98, 97, ..., 5, 4, 3, 2, 1. Будем считать объект 100 наиболее релевантным, а объект 1 - наименее релевантным.

| Сценарий | Запрос | Ответ |
|----------|--------|-------|
| получить объект по id | `base_id=5` или `base_id=5&after_limit=0&before_limit=0` | 5 |
| получить 5 самых релевантых объектов| `after_limit=5`| 100, 99, 98, 97, 96 |
| получить новые объекты в ленте (проверить, появились ли они) | `base_id=100&before_limit=1` | ответ пустой, если новых объектов не появилось; 101, если что-то появилось |
| получить следующую страницу объектов (скролл вниз) | `base_id=96&after_limit=5` | 95, 94, 93, 92, 91 |
| лента закончилась | `base_id=3&after_limit=10` | 2, 1 |
| лента закончилась, ответ пустой | `base_id=1&after_limit=10` | |
| получаем конкретный объект в ленте | `base_id=8&after_limit=0&after_limit=0` | 8 |
| пользователь смотрит на объект 35 и скроллит вверх | `base_id=35&before_limit=5` | 40, 39, 38, 37, 36 |
| запрос внутри ленты | `base_id=35&before_limit=2&after_limit=3` | 37, 36, 35, 34, 33, 32 |

### API

#### **/v1/assignments/find**
**Method**   | GET|
-------------|-|
**Params**   | |
`lang`   | Required, локаль пользователя: настройки языка и региона |
`metadata_ids` | Required, `10,11,12...`, список типов заданий, которые клиент хочет получить. Тип задания задаётся номером поля для соотвествующего задания в протобуфе. |
`status` | Optional, `active|done|postponed`, `active` по умолчанию
| ***Paging*** | Группа параметров для пейджинга |
`base_id`  | Optional, id задания, задаёт позицию в отранжированном списке заданий, относительно которой сервер формирует ответ
`before_limit`  | Optional, количество заданий, которые нужно вернуть перед заданием _base_id_, 0 по умолчанию, не используется без параметра _base_id_
`after_limit`  | Optional, количество заданий, которые нужно вернуть после задания _base_id_, 0 по умолчанию, если не задавать _base_id_, то сервер вернёт задания из начала отранжированного списка
**Description** | Получение списка заданий для пользователя. Можно получить задания, отфильтрованные по определённым `metadata_ids` или по статусу. По типу данных в задании клиент понимает, в чём суть задания и показывает нужную форму. |
**Response Body** | [Assignments][UgcAccount] |

#### **/v1/assignments/find_in_bbox**
**Method**   | GET|
-------------|-|
**Params**   | |
`lang`   | Required, локаль пользователя: настройки языка и региона |
`metadata_ids` | Required, `10,11,12...`, список типов заданий, которые клиент хочет получить. Тип задания задаётся номером поля для соотвествующего задания в протобуфе. Все задания переданных типов должны иметь геометрию. Если клиент передал тип задания, для которого геометрия не обязательна, он получит 400 bad request. |
`bbox`  | Required, bounding box области, по которой будут отфильтрованы задания. Размер ответа ограничен параметром `limit`.
`status` | Optional, `active|done|postponed`, `active` по умолчанию
`limit` | Optional, 100 по умолчанию. Ограничение на количество заданий в ответе сервера.
**Description** | Получение заданий для пользователя внутри заданного bounding box-а. Можно получить задания, отфильтрованные по определённым `metadata_ids` или по статусу. По типу данных в задании клиент понимает, в чём суть задания и показывает нужную форму. |
**Response Body** | [Assignments][UgcAccount] |

#### **/v1/assignments/skip**
**Method**   | PUT|
-------------|-|
**Params**   | |
`task_id` | Required, id задания |
**Description** | Пользователь нажал _"Не знаю"_/_"Удалить"_/_"Пропустить"_ или ещё как-то отметил, что не хочет делать задание. Переводим статус этого задания в `skipped`|
**Response Body** | Достаточно кода ответа |
**Details** | После обработки запроса сервис сохраняет куда-то данные о пропущенных заданиях, чтобы в дальнейшем **Сервис UGC** мог использовать эти данные при генерации новых заданий |

#### **/v1/contributions/find**
**Method**   | GET|
-------------|-|
**Params**   | |
`lang`   | Required, локаль пользователя: настройки языка и региона |
`metadata_ids` | Required, `10,11,12...`, список типов вклада, которые клиент хочет получить. Тип вклада задаётся номером поля для соотвествующего вклада в протобуфе. |
`base_id`  | Optional, id вклада, задаёт позицию в отсортированном по времени списке событий, относительно которой сервер формирует ответ
`before_limit`  | Optional, количество событий, которые нужно вернуть перед событием _base_id_, 0 по умолчанию, не используется без параметра _base_id_
`after_limit`  | Optional, количество событий, которые нужно вернуть после события _base_id_, 0 по умолчанию, если не задавать _base_id_, то сервер вернёт события из начала отсортированного списка
**Description** | Получение списка событий с вкладом пользователя. Можно фильтровать события по типу. |
**Response Body** | [Contributions][UgcAccount] |
**Details** | В ленте отображаются только превьюшки событий. За детальной информацией нужно идти в **Сервис UGC**. Он же предоставляет возможность каких-то действий с объектом вклада |

#### **/v1/contributions/stat**
**Method**   | GET|
-------------|-|
**Params**   | |
`metadata_ids` | Required, `10,11,12...`, список типов вклада, по которым клиент хочет посчитать статистику. Тип вклада задаётся номером поля для соотвествующего вклада в протобуфе. |
**Description** | Получение статистики (числа) вкладов пользователя. Можно фильтровать вклады по типу. |
**Response Body** | [ContributionsStat][UgcAccount] |
**Details** | |


[UgcAccount]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/ugc_account.proto
[Readme]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Readme.md
