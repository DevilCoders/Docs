## Методы

-   `getHotelReviews`:: `/api/hotels_portal/v1/get_hotel_reviews`
-   `setHotelReviewReaction`:: `/api/hotels_portal/v1/set_hotel_review_reaction`
-   `addHotelReview`:: `/api/hotels_portal/v1/add_hotel_review`
-   `editHotelReview`:: `/api/hotels_portal/v1/edit_hotel_review`
-   `deleteHotelReview`:: `/api/hotels_portal/v1/delete_hotel_review`
-   `uplaodHotelReviewImage`:: `/api/hotels_portal/v1/upload_hotel_review_image`
-   `deleteHotelReviewImages`:: `/api/hotels_portal/v1/delete_hotel_review_images`

## Особенности

-   На странице отзывов фильтруем максимум по 1 интенту (`IKeyPharse`). (Поэтому в бекенде 1 параметр `keyPharse` в ручке отзывов.)
-   Давать возможность ставить лайки/дизлайки нужно _только_ залогиненым (с passport-id) пользователям.
-   Отзывы могут писать только залогиненые пользователи
-   Для работы с отзывами АПИ использует сервис [UGC](https://wiki.yandex-team.ru/jandekspoisk/ugc/)

## Процесс написания отзыва и добавления фотографий к ним

UGC работает с фотографиями в отзывах немного неочевидным образом:

-   Если сначала загрузить фотографии к отелю, а потом создать отзыв с пустым списком фото, то отзыв создастся со всеми загруженными ранее фотографиями
-   Если удалить отзыв, то фотографии отзыва автоматически удалятся
-   Если удалить фото, то оно удалится из отзыва в любом случае (сохранены ли изменения в отзыве или нет)
-   Если загрузить фото к существующему отзыву и не обновить отзыв, то фото прикрепится к отзыву автоматически

Поэтому при удалении/добавлении фотографий при создании, редактировании и удалении отзывов важен правильный порядок операций

### Как создать отзыв

-   Пользователь пишет комментарий, ставит оценку, загружает фотографии. Фронт загружает фотографии с помощью запроса `uplaodHotelReviewImage` и запоминает id загруженных фотографий.
-   Если пользователь нажимает "Сохранить отзыв", то фронт отправляет в АПИ запрос `addHotelReview` с данными отзыва с id прикрепленных фотографий.
-   Если пользователь передумал писать отзыв и наживает "Отменить", то фронт отправляет в АПИ запрос `deleteHotelReviewImages` с id прикрепленных фотографий. Мы их удаляем, чтобы они не добавились в другой отзыв пользователя, который он может написать в будущем

### Как отредактировать отзыв

-   Пользователь меняет комментарий, меняет оценку, удаляет и загружает фотографии. Фронт загружает фотографии с помощью запроса `uplaodHotelReviewImage`, удаляет фотографии, не отправляя запрос в АПИ, и запоминает id удаленных фотографий и id загруженных фотографий.
-   Если пользователь нажимает "Сохранить отзыв", то фронт отправляет в АПИ запрос `editHotelReview` с данными отзыва с id отсавшихся в отзыве фотографий после удаления и id новых загруженных фотографий и запрос `deleteHotelReviewImages` с id удаленных фотографий. Мы их не удаляем в момент когда пользователь нажал "Удалить фото", чтобы была возможность отменить изменения отзыва.
-   Если пользователь нажимает "Отменить", то фронт отправляет в АПИ запрос `deleteHotelReviewImages` с id новых загруженных фотографий. Мы их удаляем, чтобы они не добавились к существующему отзыву

### Как удалить отзыв

-   Пользователь нажимает "Удалить отзыв", фронт отправляет в АПИ запрос deleteHotelReview с id отзыва. Фотографии отзыва удалятся автоматически.
