# Отображение реальных статусов кампаний

Синхронизация статусов РК с Директ - нужно чтобы отображать реальные статусы кампании. Сейчас есть кейсы когда в директе кампания остановлено (например 0 денег на счету) а у нас она отображается как активная.
Основная сложность в том, чтобы логически синхронизировать статусы РК и объявлений у нас со статусами РК и объявлений в директе (условная таблица маппингов и переходов).

Тикет: [https://st.yandex-team.ru/EDAPARTNERS-1857](https://st.yandex-team.ru/EDAPARTNERS-1857)

## Состояния РК в Директе

- CONVERTED
Кампания велась в у. е. до перехода рекламодателя на работу в реальной валюте, в настоящее время перемещена в специальный архив и доступна только для чтения.
- ARCHIVED
Кампания помещена в архив с помощью метода archive, пользователем в веб-интерфейсе или автоматически (если на счете нет средств и показов не было более 30 дней).
- SUSPENDED
- ENDED
- ON
- OFF
- UNKNOWN
Используется для обеспечения обратной совместимости и отображения состояний, не поддерживаемых в данной версии API.

## Статусы РК в Директе

- DRAFT
- MODERATION
- ACCEPTED
- REJECTED
- UNKNOWN
Используется для обеспечения обратной совместимости и отображения статусов, не поддерживаемых в данной версии API.

## Отображение статусов и состояний в статусы CPM
статусы CPM:
|typname        |enumlabel          |
|---------------|-------------------|
|campaign_status|active             |
|campaign_status|ended              |
|campaign_status|in_creation_process|
|campaign_status|not_created        |
|campaign_status|ready              |
|campaign_status|rejected           |
|campaign_status|suspended          |

отображение:
| статус\состояние | ARCHIVED | SUSPENDED | ENDED    | ON        | OFF      |
|------------------|----------|-----------|----------|-----------|----------|
| DRAFT            | ended    | suspended | ended    | ?         | ?        |
| MODERATION       | ended    | suspended | ended    | ?         | ?        |
| ACCEPTED         | ended    | suspended | ended    | ?         | ?        |
| REJECTED         | rejected | rejected  | rejected | rejected  | rejected |

Если кампания в состоянии ON, то campaign_status должен быть active, ended или suspended. 

? = не меняем статус
## Отображение статусов и состояний в статусы CPC
статусы CPC:

|typname      |enumlabel|
|-------------|---------|
|advert_status|paused   |
|advert_status|started  |

отображение:
| статус\состояние | ARCHIVED | SUSPENDED | ENDED  | ON| OFF|
|------------------|----------|-----------|--------|---|----|
| DRAFT            | paused   | paused    | paused | ? | ?  |
| MODERATION       | paused   | paused    | paused | ? | ?  |
| ACCEPTED         | paused   | paused    | paused | ? | ?  |
| REJECTED         | paused   | paused    | paused | ? | ?  |

? = не меняем статус

## Как получить статусы Директа

[GET: https://api.direct.yandex.com/json/v5/campaignsext](https://julia90-d-docapi-9171-d-10-d-tech2-d-dev.daas-unstable.locdoc-test.yandex.ru/direct/doc/ref-v5/campaignsext/get.html)

Получать можем только для конкретного партнера, у которого есть право управления кампанией.

Параметры, которые необходимо передать:
- авторизационный токен владельца кампаний
- SelectionCriteria.Ids - ids кампаний 
- FieldNames: Id, State, Status - какую информацию нужно вернуть

## Как обновить

Запускаем периодику, которая идет по всем партнерам. Для каждого партнера получаем список его кампаний со статусами от директа и из нашей таблички. Если отображение статуса и состояния из директа в наши статусы не соответствует реальности - обновляем в наших табличках для конкретной кампании.

- Статусы директа - ручка GET: https://api.direct.yandex.com/json/v5/campaignsext
- Статусы CPM кампаний - из таблички eats_resatapp_marketing.campaigns
- Статусы CPC кампаний - из таблички eats_resatapp_marketing.advert
