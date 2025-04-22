**Шапка**

![](header.png)

```ts
interface IHeaderBlock {
    type: EBlockType.HEADER;
    /**
     * Логотип сервиса + ссылка на сервис
     */
    logo: IImageLink;
    links: ILink[];
}
```

---

**Приветствие**

![](greeting.png)

```ts
interface IGreetingBlock extends IBaseBlock {
    type: EBlockType.GREETING;
    image: string;
    /**
     * Приветственный текст
     */
    text: string;
    /**
     * Определяет тип отображения
     * overlaying: false - текст располагается под изображением
     * overlaying: true - текст наложен поверх изображения
     */
    overlaying: boolean;
}
```

---

**Бронирование**

![](booking.png)

```ts
interface IBookingBlock extends IBaseBlock {
    type: EBlockType.BOOKING;
    hotelName: string;
    image: string;
    /**
     * Ссылка - адрес отеля
     */
    geoPosition: ILink;
    checkin: string;
    checkout: string;
    /**
     * Даты проживания
     */
    dates: string;
    /**
     * Ссылка на скачивание бронирования
     * Пример: https://travel.yandex.ru/download/hotels/voucher/YA-2527-9079-3892/?actionType=download
     */
    download: IButtonLink;
}
```

---

**Билет на поезд**

![](trainTicket.png)

```ts
interface ITrainTicketBlock extends IBaseBlock {
    type: EBlockType.TRAIN_TICKET;
    orderNumber: string;
    /**
     * Точки маршрута (Москва - Владимир)
     */
    points: string[];
    /**
     * Полезная информация о посадке (Нужен только паспорт и т.д.)
     */
    boardingHint: string;
    departure: IRoutePoint;
    arrival: IRoutePoint;
    /**
     * Длительность поездки в удобном для человека виде (примерный формат: 7 ч 45 мин, 2 д 12 ч)
     */
    duration: string;
    /**
     * Номер поезда / номер поезда + название
     */
    trainName: string;
    /**
     * Информация о вагоне / местах
     */
    trainInfo: string;
    /**
     * Список удобств
     */
    facilities: {
        icon: string;
        /**
         * Для тех кто не понял что это за иконка должна быть возможность показать хинт
         */
        hint: string;
    }[];
    /**
     * Ссылка на скачивание билета
     * Пример: https://travel.yandex.ru/download/trains/ticket/100cb47d-4491-4beb-aa52-474aac35e018
     */
    download: IButtonLink;
    /**
     * Ссылка - адрес/маршрут до вокзала
     */
    route: ILink;
}

interface IRoutePoint {
    /**
     * Название станции отправления
     */
    station: string;
    /**
     * Дата в удобном для человека формате (22 июля, суббота)
     */
    date: string;
    /**
     * Время в формате HH:MM
     */
    time: string;
    /**
     * Приписка в случае если дата предыдущей точки маршрута отличается от текущей
     * Примеры:
     *  - поезд отправляется 22 числа, а прибывает 23
     *  - первая часть маршрута попадает в одни сутки, а следующая - в другие
     */
    nextDateHint?: string;
}
```

---

**Блок "Полезное"**

-   Ориентируйся как местный
-   Передвигайся с комфортом
-   Музыка и фильмы в дорогу
-   Чтобы хватило места для всего
-   Если нужна помощь

![](common.png)

```ts
interface IUsefulBlock extends IBaseBlock {
    type: EBlockType.USEFUL;
    items: IUsefulBlockItem[];
}

interface IUsefulBlockItem {
    title: string;
    description: string;
    image: string;
    url: string;
}
```

---

**Карусель**

-   Аудиогид
-   События
-   Достопримечательности
-   Не забудьте забронировать отель

![](carousel.png)

```ts
interface ICarouselBlock extends IBaseActionBlock {
    type: EBlockType.CAROUSEL;
    items: ICarouselBlockItem[] | ICarouselBlockHotelItem[];
}

interface ICarouselBlockBaseItem {
    image: string;
    title: string;
    url: string;
}

interface ICarouselBlockHotelItem extends ICarouselBlockBaseItem {
    /**
     * Количество звезд. От 1 до 5. Целое число.
     * Может отстустовать, не у всех отелей есть звёзды.
     */
    stars?: number;
    rating: number;
    reviews: string;
    accommodation: string;
    orderInfo: string[];
    price: string;
}

interface ICarouselBlockItem extends ICarouselBlockBaseItem {
    description: string;
    info: {
        icon: string;
        text: string;
    };
}
```

---

**Погода**

![](weather.png)

```ts
interface IWeatherBlock extends IBaseActionBlock {
    type: EBlockType.WEATHER;
    items: IWeatherBlockItem[];
}

interface IWeatherBlockItem {
    /**
     * 2-х буквенное название дня недели
     */
    day: string;
    /**
     * Признак выходного дня
     */
    isWeekend: boolean;
    /**
     * Дата (20 янв)
     */
    date: string;
    temperature: {
        day: string;
        night: string;
    };
    /**
     * Иконка и текст для отображения погодных условий
     */
    conditions: {
        icon: string;
        description: string;
    };
}
```

---

**Перед отъездом**

![](before-departure.png)

```ts
interface IPreTripBlock extends IBaseBlock {
    type: EBlockType.BEFORE_DEPARTURE;
    blocks: {
        title: string;
        items: {
            icon: string;
            description: string;
        }[];
    }[];
    /**
     * Пожелания счастливого пути
     */
    partingWishes: string;
}
```

---

**Подвал**

![](footer.png)

```ts
interface IFooterBlock {
    type: EBlockType.FOOTER;
    /**
     * Ссылки на соцсети
     */
    social: IImageLink[];
    /**
     * Телефон поддержки и сопровождающий текст
     * Возможно стоит сразу упороться за транслокальность и в сопровождающий текст вставлять плейсхолдер
     * для последующей замены на ссылку с номером телефона
     */
    support: {
        phoneNumber: string;
        hint: string;
    };
    /**
     * Подвальные ссылки
     */
    links: ILink[];
}
```

---

**Дисклеймеры**

![](disclaimers.png)

```ts
interface IDisclaimersBlock {
    type: EBlockType.DISCLAIMERS;
    disclaimers: string[];
}
```
