---
title: API для подключения партнёров к Отелям (aka PacificAPI)
---

## Продуктовые требования

Для того чтобы показывать предложения clickout партнёров в [колдунщике](https://yandex.ru/support/webmaster/search-appearance/hotel-list.html), необходимо разработать сервис с единым API для их подключения.

Важно, чтобы наши усилия при подключении новых партнёров были сведены к минимуму.

Целевая схема: мы даём документацию и ключи доступа, партнёр отправляет свои данные, они валидируются онлайн и появляются в Отелях.

## Технические требования

Приложение должно иметь три API:
* для партнёров;
* для feeder;
* для searcher.

С точки зрения отельной архитектуры это будет плюс-минус новый партнёр без ограничения rps.

## Спецификация API

Использована push-модель, когда партнёры присылают свои данные самостоятельно, для того чтобы мы могли возвращать подробные ошибки валидации. При pull-модели каждое подключение бы упиралось в длительную переписку с партнёрами по поводу некорректных данных, либо в отдельный интерфейс типа Яндекс.Вебмастера.

Документация для партнёров: [Спецификация API](api.md)

### Обработка [оффера](api.md#offer)

Маппинг полей [TOffer](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/proto2/hotels.proto?rev=r9097788#L161) и [TSearchOffersReq](https://a.yandex-team.ru/arc_vcs/travel/hotels/proto2/hotels.proto?rev=r9097788#L312):
```json
{
    "offers": [
        {
            "id": {{TOffer.ExternalId}},
            "title": {{TOffer.DisplayedTitle}},
            "roomCount": {{TOffer.RoomCount}},
            "features": [
                "boardBasis": {{TOffer.Pansion}},
                "wifi": {{TOffer.WifiIncluded}}
            },
            "tariffs": [
                {
                    "conditions": {
                        "checkInDate": {{TSearchOffersReq.CheckInDate}},
                        "checkOutDate": {{TSearchOffersReq.CheckOutDate}},
                        "occupancy": {{TSearchOffersReq.Occupancy}}
                    },
                    "rate": {
                        "amount": {{TOffer.Price.Amount / days}},
                        "currency": {{TOffer.Price.Currency}}
                    },
                    "refundRules": {{RefundRule}}
                }
            ]
        }
    ]
}
```

### Обработка тарифов

Как применяются тарифы:
* Если выполняются все условия в `conditions`, то оффер имеет цену `days*rate` и условия возврата из `refundRules`;
* Ищем подходящий тариф последовательно по переданному списку, то есть первый тариф имеет наибольший приоритет и так далее;
* Условия тарифов могут пересекаться, при этом они не могут быть невыполнимыми — на это будет проверка;
* Цена оффера может состоять из нескольких тарифов, если у них одинаковые `groupId`, при этом `refundRules` тоже должны быть одинаковыми — на это будет проверка;

## Реализация

### Стек

* Go
* PostgreSQL (или YDB?)

### Архитектура

#### Квота на запись

Чтобы партнёры не сломали сервис загрузкой данных, вводим квоту на поставку данных в GB/час. Объёмы квоты определим нагрузочным тестированием.
При превышении объёма будем отдавать статус `429 Too Many Requests`.

#### REST API для партнёров

Основная нагрузка это запись:
1. Проверяет ограничение квоты.
2. Валидирует данные.
3. Записывает данные в БД.

#### GRPC API

* Сериализует отельные офферы из данных в БД для Searcher.
* Отдаёт отели и заказы для sandbox-тасков, которые складывают данные в YT.

### Структура БД
* Partners
    * id: string
    * oauth-client-id: string
    * name: string

* Hotels
    * id: string
    * partner_id: string
    * names: string[]
    * urls: string[]
    * phones: string[]
    * emails: string[]
    * address_country: string
    * address_region: string
    * address_district: string
    * address_settlement: string
    * address_postal_code: string
    * address_street_address: string
    * geo_latitude: float
    * geo_longitude: float
    * star_rating: int
    * photos: string[]
    * features_tv_in_room: bool
    * features_beach_line: enum

* HotelsVersions
    * partner_id: string
    * version: string

* Offers
    * id: string
    * partner_id: string
    * hotel_id: string
    * url: string
    * name: string
    * room_count: int
    * feature_board_basis: enum
    * feature_wifi: boolean

* OfferTariffs
    * id: string
    * partner_id: string
    * hotel_id: string
    * offer_id: string
    * group_id: string
    * condition_dates: daterange[]
    * condition_days: int4range
    * condition_weekdays: bit(7)
    * condition_occupancy_adults: int4range
    * condition_occupancy_children_ages: int4range[]
    * rate_amount: decimal
    * rate_currency: enum

* RefundRules
    * id: int
    * type: enum
    * partner_id: string
    * hotel_id: string
    * offer_id: string
    * tariff_id: string
    * starts_at: interval
    * ends_at: interval
    * penalty_amount: decimal
    * penalty_currency: enum

* Orders
    * id: string
    * token: string
    * hotel_id: string
    * offer_id: string
    * status: enum
    * check_in: date
    * check_out: date
    * price_amount: decimal
    * price_currency: enum

### План

1. Бутстрап проекта
    1. ya.make (2 SP)
    2. CI/Deploy (2 SP)
    3. Дашборды по метрикам Deploy и GRPC (3 SP)
2. Аутентификация
    1. Проверка OAuth токена по аналогии с ExternalAPI (3 SP)
3. Загрузка отелей
    1. Модели БД (2 SP)
    2. Внешние ручки:
        1. Ручки перезаписи данных обо всех отелях и отдельном отеле (3 SP)
        2. Ручка удаления данных (2 SP)
        3. Ручка получения данных (2 SP)
    3. Процесс выгрузки отельного фида (5 SP)
       sandbox-таск, который обходит ручки получения данных и складывает данные в YT.
    4. Тестирование (? SP)
4. Загрузка предложений
    1. Модели БД (2 SP)
    2. Внешние ручки:
        1. Ручки перезаписи данных обо всех предложениях и отдельном предложении (3 SP)
        2. Валидация данных во время перезаписи (3 SP)
        3. Ручка удаления данных (2 SP)
        4. Ручка получения данных (2 SP)
    3. Тестирование (? SP)
5. Нагрузочное тестировние
   1. Сгенерировать патроны (2 SP)
   2. Обстрелять минимальную конфигурацию на разладку для подсчёта размера квоты (3 SP)
6. Ручка для searcher
    1. Реализация ответа с предложениями (5 SP)
    2. Тестирование (? SP)
7. Загрузка данных о заказах
    1. Модели БД (2 SP)
    2. Внешняя ручка для загрузки данных (5 SP)
    3. Внутренняя ручка для выгрузки данных (3 SP)
    4. Выгрузка данных в биллинг (5 SP)
       sandbox-таск, который обходит ручки выгрузки данных и складывает данные в YT для биллинга.

## Название
Проект появился благодаря Федеральной Антимонопольной Службе и заключению мирового соглашения с компаниями, подавшими иск. Поэтому он называется как одно из полей в настольной игре Monopoly — "Pacific Avenue" (по-нашему улица Мира).

(альтернативное название Boardwalk)
