**Назначение:** Поиск отелей в справочнике отелей и с актуальными ценами.

**path:** `rooms-backend/api/offers/search-hotels-and-retrieve-offers`

**method:** `GET`

**Описание**
В методах этого раздела возвращаем актуальные цены номеров, поэтому все методы:

-   получают параметры бронирования, даты и количество гостей
-   работают в асинхронном режиме, потому что получение актуальной информации
    о вариантах бронирования может быть долгим.
