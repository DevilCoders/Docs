## Страницы на сайте

### 1. IndexPage

**Используемые endpoints:**

-   [rooms-backend/api/hotels/search-hotels](api/hotels/search-hotels)
-   [rooms-backend/api/hotels/get-faq](api/hotels/get-faq)
-   [rooms-backend/api/hotels/get-hotel-available-search-params](api/hotels/get-hotel-available-search-params)

    возможно

**Открытые вопросы по странице:**

-   что за кнопка "найти отель"?

    **Ответ:** кнопка ведет на модал с фильтрами ( где выбор дат и прочее), не текстовый инпут!

-   в выдаче на главной есть цены, на какие даты цены, или это историческая цена?

    **Ответ:** идеале цена на сегодня, возможно ли считать исторической, не уверен до конца, важно "дать понять
    пользователю о ценовой категории отеля, уловно мета-москва - от 2000р за ночь,
    а другой отель - от 5000р за ночь, при этом слово "от" использовать не надо

    **Замечание:** Что такое цена на сегодня?

    -   Цена за которую можно поселиться сегодня.
    -   А если сегодня весь отель выкуплен.
    -   Цена за которую можно сегодня забронировать проживание через неделю.
    -   Цена за которую можно сегодня забронировать проживание на майские праздники (высокий сезон).

-   есть кнопка "отели на карте", но дат нету, какие цены будем показывать?

    **Ответ:** не нужна. Будем показывать (сегодня, 1 ночь, 1 человек) (а почему на 2 взрослых?).

-   вопрос по блоку "скидка на первый заказ" - мы не знаем что есть "первый заказ"

    **Ответ:** пока предикат не понятен.

-   вопрос уточнить нужен ли на этой странице ([rooms-backend/api/hotels/get-hotel-filters](api/hotels/get-hotel-available-search-params))

    **Ответ:**

### 2. SearchPage (Список | Карта)

**Используемые endpoints:**

-   [rooms-backend/api/hotels/get-hotel-filters](api/hotels/get-hotel-available-search-params)
-   [rooms-backend/api/offers/search-hotels-and-retrieve-offers](api/offers/search-hotels-and-retrieve-offers)

**Открытые вопросы по странице:**

-   Какие поддерживаем сортировки?

### 3. HotelPage (Обычная + Без Дат)

**Используемые endpoints:**

-   [rooms-backend/api/offers/retrieve-hotel-offers](api/offers/retrieve-hotel-offers)
-   [rooms-backend/api/hotels/get-hotel-info](api/hotels/get-hotel-info)
-   [rooms-backend/api/hotels/get-hotel-reviews](api/hotels/get-hotel-reviews)
-   [rooms-backend/api/hotels/get-hotel-images](api/hotels/get-hotel-images)
-   [rooms-backend/api/hotels/get-hotel-room-images](api/hotels/get-hotel-room-images)

### 4. HappyPage

### 5. BookPage

### 6. OrderPage( + форма поиска заказа)

### 7. PayPage (Платежка)

## список API

### Поиск вариантов бронирования номеров в отеле

В методах этого раздела возвращаем актуальные цены номеров, поэтому все методы:

-   получают параметры бронирования, даты и количество гостей
-   работают в асинхронном режиме, потому что получение актуальной информации
    о вариантах бронирования может быть долгим.

**Методы:**

2. поиск отелей вместе с актуальными ценами ([search-hotel-with-offers](api/offers/search-hotels-and-retrieve-offers))

    Аналогичен поиску отелей ([search-hotels](api/hotels/search-hotels)), но содержит
    так же данные об актуальной цене номер

    `path:` `rooms-backend/api/offers/search-hotel-with-offers`

    `method:` `GET`
