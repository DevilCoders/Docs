# Отрытые вопросы по API rooms

## Известные ошибки и опечатки в описании методов
Страницы на которых нужно исправить описание или путь:
* [ ] [`rooms-backend/api/hotels/get-faq`](../../frontend/spec/rooms-backend/api/hotels/get-faq)

  Исправить: назначения, `path`. Проставить коментарии в ответе.

* [ ] [`rooms-backend/api/hotels/get-hotel-info`](../../frontend/spec/rooms-backend/api/hotels/get-hotel-info)

  Исправить: назначения.

* [ ] [`rooms-backend/api/offers/retrieve-hotel-offers`](../../frontend/spec/rooms-backend/api/offers/retrieve-hotel-offers)

  Исправить: `path`.

## Очевидные не точности api
### Отказ от наследования в пользу инкапсуляции
Не вижу смысла убирать наследовадования:
* в запросах, потому что оно тривиально
* в иерархии `IHotel` это чуть похоже на OOP
  ```plantuml
  @startuml
  IHotelInfo -|> IHotel
  IHotel <|- IHotelWithDefaultOffer

  note top of IHotel: Отели в результатах поиска отелей
  note top of IHotelInfo: Детальное описание отеля
  note top of IHotelWithDefaultOffer: Отели в результатах поиска отелей \n c предложением по умолчанию
  @enduml
  ```
Считаю лучше отказаться от наследования в пользу поля:
* [ ] использование `IWithHotelImages`;
* [ ] использование `IAsyncResponse`.

### Поисковое api
Методы:
* [`rooms-backend/api/hotels/search-hotels`](../../frontend/spec/rooms-backend/api/hotels/search-hotels)
* [`rooms-backend/api/offers/search-hotels-and-retrieve-offers`](../../frontend/spec/rooms-backend/api/offers/search-hotels-and-retrieve-offers)

* [ ] объеденить в общий класс `IHotelPageNavigationParams` и `IHotelSortParams`;
* [ ] объеденить в общий класс `IHotelFilterParams` и `IHotelPriceFilterParams`.

### Метод retrieve-hotel-offers
С методом [`rooms-backend/api/offers/retrieve-hotel-offers`](../../frontend/spec/rooms-backend/api/offers/retrieve-hotel-offers), есть несколько открытых
вопросов.

* Нужно ли использовать поиск запрос вариантов бронирования по одному отелю или по нескольким?
  Вроде как сейчас используем по одному, но ... .
* Если по нескольким то делать `POST` или `GET`?
  У нас везде `GET`, но при передачи масивов в `GET` достаточно быстро переполняются размеры HTTP-header'а.
* Если использовать `POST`, то как задавать запрос?
  `JSON` в теле запроса или `FORM` в теле запроса или часть параметров в теле (`hotelIds`), а остальные в `url`.

короче сложно. Возможно в самом деле заменить на запрос предложенй по одному отелю.

### Поле `IHotelOffers#searchIsFinished`
* [ ] переименовать `IHotelOffers#searchIsFinished` в `IHotelOffers#isRetrieved`;
* [ ] добавить общее поле `isRetrieved` в ответе [`rooms-backend/api/offers/search-hotels-and-retrieve-offers`](../../frontend/spec/rooms-backend/api/offers/search-hotels-and-retrieve-offers)
       и возможно [`rooms-backend/api/offers/retrieve-hotel-offers`](../../frontend/spec/rooms-backend/api/offers/retrieve-hotel-offers) .
