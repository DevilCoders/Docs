## Избранное

Можно получить избранные отели пользователя с помощью getFavoriteHotels и отели из пошаренной ссылки с помощью getSharedFavoriteHotels.
Обе ручки могут вернуть предложения не во всех отелях, если предложения ещё не получены от партнёров. В таком случае нужно дозапросить предложения для нужных отелей с помощью getFavoriteHotelsOffers.

## Методы

-   `addFavoriteHotel` :: `POST /api/hotels_portal/v1/add_favorite_hotel`
-   `removeFavoriteHotels` :: `POST /api/hotels_portal/v1/remove_favorite_hotels`
-   `shareFavoriteHotels` :: `POST /api/hotels_portal/v1/share_favorite_hotels`
-   `getFavoriteHotels` :: `GET /api/hotels_portal/v1/get_favorite_hotels`
-   `getSharedFavoriteHotels` :: `GET /api/hotels_portal/v1/get_shared_favorite_hotels`
-   `getFavoriteHotelsOffers` :: `GET /api/hotels_portal/v1/get_favorite_hotels_offers`
