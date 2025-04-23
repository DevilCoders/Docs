# Документация по Checkout API для магазинов 

- [Concept](#concept)
- [API](#api)
  - [YandexCheckoutRequest](#yandexcheckoutrequest)
  - [YandexCheckoutDetails](#yandexcheckoutdetails)
    - [YandexCheckoutCartItem](#yandexcheckoutcartitem)
    - [YandexCheckoutCartDetail](#yandexcheckoutcartdetail)
    - [YandexCheckoutShippingOption](#yandexcheckoutshippingoption)
    - [YandexCheckoutPickupOption](#yandexcheckoutpickupoption)
    - [YandexCheckoutDatetimeOption](#yandexcheckoutdatetimeoption)
  - [YandexCheckoutOptions](#yandexcheckoutoptions)
  - [YandexCheckoutState](#yandexcheckoutstate)
  - [События](#%D1%81%D0%BE%D0%B1%D1%8B%D1%82%D0%B8%D1%8F)
    - [Список событий](#%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA-%D1%81%D0%BE%D0%B1%D1%8B%D1%82%D0%B8%D0%B9)
  - [Результат оформления заказа](#%D1%80%D0%B5%D0%B7%D1%83%D0%BB%D1%8C%D1%82%D0%B0%D1%82-%D0%BE%D1%84%D0%BE%D1%80%D0%BC%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7%D0%B0)
- [Примеры](#%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B)
  - [Заказ с фиксированной ценой](#%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7-%D1%81-%D1%84%D0%B8%D0%BA%D1%81%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B9-%D1%86%D0%B5%D0%BD%D0%BE%D0%B9)
  - [Отложенное создание токена Яндекс Оплаты](#%D0%BE%D1%82%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%BD%D0%BE%D0%B5-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D1%82%D0%BE%D0%BA%D0%B5%D0%BD%D0%B0-%D1%8F%D0%BD%D0%B4%D0%B5%D0%BA%D1%81-%D0%BE%D0%BF%D0%BB%D0%B0%D1%82%D1%8B)
  - [Оплата наличными](#%D0%9E%D0%BF%D0%BB%D0%B0%D1%82%D0%B0-%D0%BD%D0%B0%D0%BB%D0%B8%D1%87%D0%BD%D1%8B%D0%BC%D0%B8)
  - [Онлайн оплата через внешние сервисы оплаты](#%D0%9E%D0%BD%D0%BB%D0%B0%D0%B9%D0%BD-%D0%BE%D0%BF%D0%BB%D0%B0%D1%82%D0%B0-%D1%87%D0%B5%D1%80%D0%B5%D0%B7-%D0%B2%D0%BD%D0%B5%D1%88%D0%BD%D0%B8%D0%B5-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D1%8B-%D0%BE%D0%BF%D0%BB%D0%B0%D1%82%D1%8B)
    - [Настройка коллбэков для внешних сервисов оплат](#%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%BA%D0%BE%D0%BB%D0%BB%D0%B1%D1%8D%D0%BA%D0%BE%D0%B2-%D0%B4%D0%BB%D1%8F-%D0%B2%D0%BD%D0%B5%D1%88%D0%BD%D0%B8%D1%85-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%BE%D0%B2-%D0%BE%D0%BF%D0%BB%D0%B0%D1%82)
  - [Обработка ошибки оплаты](#%D0%BE%D0%B1%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B0-%D0%BE%D1%88%D0%B8%D0%B1%D0%BA%D0%B8-%D0%BE%D0%BF%D0%BB%D0%B0%D1%82%D1%8B)
  - [Скидка за онлайн оплату](#%D0%A1%D0%BA%D0%B8%D0%B4%D0%BA%D0%B0-%D0%B7%D0%B0-%D0%BE%D0%BD%D0%BB%D0%B0%D0%B9%D0%BD-%D0%BE%D0%BF%D0%BB%D0%B0%D1%82%D1%83)
  - [Запрос контактов покупателя](#%D0%97%D0%B0%D0%BF%D1%80%D0%BE%D1%81-%D0%BA%D0%BE%D0%BD%D1%82%D0%B0%D0%BA%D1%82%D0%BE%D0%B2-%D0%BF%D0%BE%D0%BA%D1%83%D0%BF%D0%B0%D1%82%D0%B5%D0%BB%D1%8F)
  - [Запрос адреса доставки](#%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0-%D0%B4%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B8)
  - [Варианты доставки в зависимости от города](#%D0%B2%D0%B0%D1%80%D0%B8%D0%B0%D0%BD%D1%82%D1%8B-%D0%B4%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B8-%D0%B2-%D0%B7%D0%B0%D0%B2%D0%B8%D1%81%D0%B8%D0%BC%D0%BE%D1%81%D1%82%D0%B8-%D0%BE%D1%82-%D0%B3%D0%BE%D1%80%D0%BE%D0%B4%D0%B0)
  - [Самовывоз из магазина](#%D1%81%D0%B0%D0%BC%D0%BE%D0%B2%D1%8B%D0%B2%D0%BE%D0%B7-%D0%B8%D0%B7-%D0%BC%D0%B0%D0%B3%D0%B0%D0%B7%D0%B8%D0%BD%D0%B0)
  - [Переключение между доставкой и самовывозом](#%D0%BF%D0%B5%D1%80%D0%B5%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-%D0%B4%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%BE%D0%B9-%D0%B8-%D1%81%D0%B0%D0%BC%D0%BE%D0%B2%D1%8B%D0%B2%D0%BE%D0%B7%D0%BE%D0%BC)
  - [Наценка за способ доставки](#%D0%BD%D0%B0%D1%86%D0%B5%D0%BD%D0%BA%D0%B0-%D0%B7%D0%B0-%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1-%D0%B4%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B8)
  - [Выбор даты и времени доставки](#%D0%B2%D1%8B%D0%B1%D0%BE%D1%80-%D0%B4%D0%B0%D1%82%D1%8B-%D0%B8-%D0%B2%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%B8-%D0%B4%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B8)
  - [Информация о скидке по акции](#%D0%B8%D0%BD%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%86%D0%B8%D1%8F-%D0%BE-%D1%81%D0%BA%D0%B8%D0%B4%D0%BA%D0%B5-%D0%BF%D0%BE-%D0%B0%D0%BA%D1%86%D0%B8%D0%B8)
  - [Прием промокодов](#%D0%BF%D1%80%D0%B8%D0%B5%D0%BC-%D0%BF%D1%80%D0%BE%D0%BC%D0%BE%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2)
  - [Предзаполнение формы для повторных заказов](#%D0%9F%D1%80%D0%B5%D0%B4%D0%B7%D0%B0%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5-%D1%84%D0%BE%D1%80%D0%BC%D1%8B-%D0%B4%D0%BB%D1%8F-%D0%BF%D0%BE%D0%B2%D1%82%D0%BE%D1%80%D0%BD%D1%8B%D1%85-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7%D0%BE%D0%B2)
  - [Мульти-заказ](#%D0%BC%D1%83%D0%BB%D1%8C%D1%82%D0%B8-%D0%B7%D0%B0%D0%BA%D0%B0%D0%B7)


## Concept

В процессе оформления заказа принимают участие следующие стороны:
1. Фротенд интернет-магазина. Сайт, на котором пользователь выбирает товары и собирает корзину. Далее просто «Фронтенд».
2. Бекенд инетернет-магазина. Система, которая предоставляет данные о товарах, их стоимости, вариантах доставки и обрабатывает заказы. Далее просто «Бекенд».
3. `YandexCheckoutRequest` – API Яндекс Браузера. Предоставляет интерфейс для оформления заказа и проводит оплату.

Взаимодействие между системами выглядит так: `Бекенд <-> Фронтенд <-> YandexCheckoutRequest`.
- Бекенд взаимодействует только с Фронтендом магазина.
- `YandexCheckoutRequest` взаимодействует только с Фронтендом магазина.
- Фронтенд получает необходимые данные из Бекенда, передает их в `YandexCheckoutRequest`, отправляет результат обратно на Бекенд.

Все данные, необходимые для оформления заказа, предоставляет Бекенд магазина. Среди таких данных могут быть:
- Состав корзины и общая стоимость заказа. 
- Варианты доставки, их стоимость.
- Скидки и промокоды.
- Токены для проведения оплаты через Яндекс Оплату.
- Ошибки заполнения формы заказа.

Эти данные необходимо передавать в `YandexCheckoutRequest` посредством специального API.

## API

### YandexCheckoutRequest

Работа с формой оплаты начинается с создания объекта `new YandexCheckoutRequest(details)`. Объект доступен в глобальной области видимости (window).

Конструктор `YandexCheckoutRequest` может сгенерировать исключение в случаях:
1. Если не передан объект `YandexCheckoutDetails` в параметрах функции.
2. Если формат объекта `YandexCheckoutDetails` не соответствует требуемой схеме. 

TypeScript интерфейс объекта:
```ts
class YandexCheckoutRequest {
    constructor(details: YandexCheckoutDetails, options?: YandexCheckoutOptions);
    
    // Открытие диалога с формой заказа
    show(): Promise<YandexCheckoutState>;

    // Добавление/удаление обработчиков событий
    addEventListener(event: string, listener: (event: YandexCheckoutRequestUpdateEvent) => void);
    removeEventListener(event: string, listener: (event: YandexCheckoutRequestUpdateEvent) => void);
};
```

Для обмена данными с Фронтендом магазина используется два объекта:
1. `YandexCheckoutDetails` - данные, необходимые для отображения формы заказа. Этот объект передается из Фронтенда в `YandexCheckoutRequest`.
2. `YandexCheckoutState` – результат заполнения пользователем формы заказа. Этот объект передается из `YandexCheckoutRequest` во Фронтенд магазина. 

### YandexCheckoutDetails

Объект `YandexCheckoutDetails` используется для:
1. Предоставления обязательных данных в момент создания `YandexCheckoutRequest`. Среди них:
    - Общая стоимость заказа `YandexCheckoutDetails.total.amount`
    - Методы оплаты и их параметры `YandexCheckoutDetails.paymentOptions`
    - В списке заказов должен быть минимум один заказ `YandexCheckoutDetails.orders[0]`
    - В составе каждого заказа должен быть минимум один товар `YandexCheckoutDetails.orders[n].cartItems[0]`, с названием и ценой
2. Обновления интерфейса формы заказа по мере заполнения формы. Для этого используется подписка на события `YandexCheckoutRequest`.

TypeScript интерфейс объекта:
```ts
type Price = {
    value: number; // Целое число в копейках
    currency: string; // Код валюты по ISO 4217
};

type YandexCheckoutDetails = {
    // Итоговая стоимость заказа, обязательное поле
    total: {
        amount: Price;
        details?: Array<{
            label: string;
            amount: Price;
        }> | null;
    };
    
    // Способы оплаты заказа
    // – минимум один элемент в списке
    // – каждый тип не может быть использован больше одного раза
    paymentOptions: Array<{
        // На данный момент поддерживается:
        // – 'offline-cash' - оплата наличными
        // – 'offline-card' - картой при получении
        // – 'yandex-payments' - онлайн оплата через Яндекс Оплату
        // – 'online-external-payments' - онлайн оплата через внешние сервисы оплаты
        type: string;
        
        // Дополнительные настройки для способа оплаты, зависят от типа.
        data?: object;
    }>;

    // Настройки полей с контактами пользователя
    payerDetails?: Array<{
        // На данный момент поддерживается:
        // - 'name' - ФИО
        // - 'email' - электронная почта
        // - 'phone' - контактный телефон
        type: string;
        require?: boolean; // Сделать поле обязательным для заполнения
    }>,

    // Показать поле для комментария к заказу
    requestOrderComment?: boolean;

    // Скидка по промокоду
    promoCode?: {
        request: boolean; // Показать поле для ввода промокода
        value?: string | null; // Активный промокод
        amount?: Price | null; // Скидка по активному промокоду
    } | null;

    // Должен быть минимум один элемент в списке
    orders: Array<{
        // Уникальный идентфикатор заказа
        id: string;
        
        // Состав корзины, обязательное поле, минимум один элемент в массиве
        cartItems: Array<YandexCheckoutCartItem>;

        // Дополнительная информация о корзине (вес товаров и тд)
        cartDetails?: Array<YandexCheckoutCartDetail> | null;

        // Способы доставки
        shippingOptions?: Array<YandexCheckoutShippingOption> | null;

        // Запросить ввод города
        requestCity?: boolean;

        // Запросить ввод адреса доставки
        requestShippingAddress?: boolean;
        
        // Адреса точек для самовывоза
        pickupOptions?: Array<YandexCheckoutPickupOption> | null;

        // Варианты даты и времени доставки
        datetimeOptions?: Array<YandexCheckoutDatetimeOption> | null;
    }>;

    // Ошибки валидации полей формы заказа, которые будут показаны пользователю.
    // Переход к оплате будет заблокирован при наличии ошибки валидации хотя бы в одном из полей.
    validationErrors?: {
        // Общая ошибка для всей формы заказа
        error?: string | null;
        
        // Ошибки заполнения контактов
        payerDetails?: {
            name?: string | null;
            email?: string | null;
            phone?: string | null;
        } | null;
        
        // Ошибки валидации промокода
        promoCode?: string | null;
        
        orders?: Array<{
            // Уникальный идентфикатор заказа
            id: string;

            // Ошибки заполнения города
            city?: string | null;

            // Ошибки заполнения адреса доставки
            shippingAddress?: {
                address?: string | null; // Валидация города, улицы, дома
            } | null;
        }>;
    };
};

type YandexCheckoutDetailsUpdate = Partial<YandexCheckoutDetails>;
```

При обновлениях `YandexCheckoutDetails` можно передавать только измененные поля (тип `YandexCheckoutDetailsUpdate`). В этом случае:
- Значения объектов будут склеены: добавятся новые поля, в существующих полях значение обновится. Чтобы удалить поле, нужно передать `null` или пустой массив.
- Значения массивов будут перезаписаны. Исключение: массив `orders`. Каждый элемент списка заказов будет склеен по id заказа.  

#### YandexCheckoutCartItem

Товарная позиция в заказе. Используется для:
- [Отображения одного товара на форме заказа](https://jing.yandex-team.ru/files/nodge/2020-07-05T18:32:53Z.c499ff0.png)
- [Отображения нескольких товаров на форме заказа](https://jing.yandex-team.ru/files/nodge/2020-07-05T18:33:21Z.62db20f.png)
- [Экрана со списком товаров](https://jing.yandex-team.ru/files/nodge/cart.png)

Товар обязательно должен содержать название товара и его стоимость. В стоимость можно передать `0`, тогда будет отображаться подпись «Бесплатно».

Форма заказа автоматически выбирает наиболее подходящее по размеру изображение. Рекомендуется передавать каждое изображение в двух размерах: 
- `96x96`
- `176x176`

TypeScript интерфейс объекта:
```ts
type YandexCheckoutCartItem = {
    // Название товара
    title: string;
    
    // Стоимость одного товара
    amount: Price;
    
    // Количество товаров в корзине
    count: number;
    
    // Набор изображений товара, рекомендуется соотношение сторон 1:1 и не более 500x500px.
    // Можно передать все имеющиеся размеры, тогда будет использован наиболее подходящий размер для формы Чекаута.
    image?: Array<{
        url: string;
        width: number;
        height: number;
    }>;
};
```

Пример:
```js
const cartItems = [
    {
        title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
        amount: {
            value: 12990 * 100,
            currency: 'RUB',
        },
        count: 1,
        image: [
            { 
                url: 'https://via.placeholder.com/96x96',
                width: 96,
                height: 96,
            },
            { 
                url: 'https://via.placeholder.com/176x176',
                width: 176,
                height: 176,
            },
        ],
    },
    {
        title: 'Чехол для Samsung Galaxy A30',
        amount: {
            value: 990 * 100,
            currency: 'RUB',
        },
        count: 2,
    },
    {
        title: 'Подарок при покупке смартфора Samsung Galaxy',
        amount: {
            value: 0,
            currency: 'RUB',
        },
        count: 1,
        image: [],
    },
];
```

#### YandexCheckoutCartDetail

Характеристика заказа. Отображается на [экране со списком товаров](https://jing.yandex-team.ru/files/nodge/cart.png).

Может содержать либо цену, либо произвольный текст.

TypeScript интерфейс объекта:
```ts
type YandexCheckoutCartDetail = {
    label: string;
    amount?: Price; // Для вывода отформатированной цены
    value?: string; // Для вывода кастомного текста
};
```

Пример:
```js
const cartDetails = [
    {
        label: '5 товаров',
        amount: {
            value: 15990 * 100,
            currency: 'RUB',
        },
    },
    {
        label: 'Скидка по акции',
        amount: {
            value: -500 * 100,
            currency: 'RUB',
        },
    },
    {
        label: 'Вес заказа',
        value: '0.4 кг',
    },
];
```

#### YandexCheckoutShippingOption

Вариант доставки или самовывоза, на форме [отображается в виде radio-кнопки](https://jing.yandex-team.ru/files/nodge/2020-07-05T18:53:39Z.4bb5d03.png).

Варианты доставки могут быть добавлены после выбора города. Для заказов без доставки опции не передаются.

TypeScript интерфейс объекта:
```ts
type YandexCheckoutShippingOption = {
    id: string;
    label: string;
    amount: Price;
    datetimeEstimate?: string; // Примерный срок доставки выбранным методом
    selected?: boolean; // Предвыбранный способ доставки
};
```

Пример:
```js
const shippingOptions = [
    {
        id: 'express-delivery',
        label: 'Курьер, срочно',
        datetimeEstimate: 'В течение дня',
        amount: {
            value: 500 * 100,
            currency: 'RUB',
        },
    },
    {
        id: 'delivery',
        label: 'Курьер',
        datetimeEstimate: 'datetimeEstimate',
        amount: {
            value: 0,
            currency: 'RUB',
        },
        selected: true,
    },
    {
        id: 'pickup',
        label: 'Самовывоз',
        datetimeEstimate: 'С завтрашнего дня',
        amount: {
            value: 0,
            currency: 'RUB',
        },
    },
    {
        id: 'shipping',
        label: 'Почта России',
        datetimeEstimate: 'Через 3-4 дня',
        amount: {
            value: 0,
            currency: 'RUB',
        },
    },
    {
        id: 'pickpoint',
        label: 'PickPoint',
        amount: {
            value: 350 * 100,
            currency: 'RUB',
        },
    },
];
```

#### YandexCheckoutPickupOption

Пункт для самовывоза заказа. Отображается на [экране выбора адреса для самовывоза](https://jing.yandex-team.ru/files/nodge/2020-07-05T18:59:16Z.f76acf4.png). 

Список пунктов может быть добавлен на форму при выборе определенного способа доставки.

При передаче координат, пункт самовывоза будет [доступен для выбора на карте](https://jing.yandex-team.ru/files/nodge/2020-07-05T19:00:28Z.54a1180.png).

TypeScript интерфейс объекта:
```ts
type YandexCheckoutPickupOption = {
    id: string;
    label: string;
    address: string;
    coordinates?: {
        lon: number;
        lat: number;
    };
    selected?: boolean; // Предвыбранная точка самовывоза
};
```

Пример:
```js
const pickupOptions = [
    {
        id: 'option-1',
        label: 'Постамат Беру',
        address: 'м. Парк Культуры, ул. Льва Толстого, 17',
        coordinates: {
            lon: 37.6173,
            lat: 55.755826,
        },
    },
    {
        id: 'option-2',
        label: 'Постамат Беру',
        address: 'м. Парк Культуры, ул. Льва Толстого, 32',
        coordinates: {
            lon: -122.419416,
            lat: 37.774929,
        },
    },
];
```

#### YandexCheckoutDatetimeOption

Выбор [даты и времени доставки или самовывоза](https://jing.yandex-team.ru/files/nodge/2020-07-05T19:04:26Z.a20e9a3.png).

Если не предполагается выбор времени доставки, то в `timeOptions` нужно указать только один элемент.

TypeScript интерфейс объекта:
```ts
type YandexCheckoutDatetimeOption = {
    id: string;
    date: string; // Дата в формате ISO 8601
    timeOptions: Array<{
        id: string;
        label: string;
        amount: Price;
        selected?: boolean; // Предвыбранное время доставки
    }>;
    selected?: boolean; // Предвыбранная дата доставки
};
```

Пример:
```js
const datetimeOptions = [
    {
        id: '2020-05-19',
        date: '2020-05-19',
        timeOptions: [
            {
                id: '18-22',
                label: 'с 18:00 до 22:00',
                amount: {
                    value: 100 * 100, // 100р наценка на доставку вечером
                    currency: 'RUB',
                },
            },
        ],
    },
    {
        id: '2020-05-20',
        date: '2020-05-20',
        selected: true,
        timeOptions: [
            {
                id: '8-22',
                label: 'с 08:00 до 22:00',
                amount: {
                    value: 0,
                    currency: 'RUB',
                },
                selected: true,
            },
            {
                id: '8-10',
                label: 'с 08:00 до 10:00',
                amount: {
                    value: -100 * 100, // 100р скидка на доставку утром
                    currency: 'RUB',
                },
            },
            {
                id: '18-22',
                label: 'с 18:00 до 22:00',
                amount: {
                    value: 100 * 100, // Наценка на доставку вечером
                    currency: 'RUB',
                },
            },
        ],
    },
];
```

### YandexCheckoutOptions

Объект `YandexCheckoutOptions` используется для передачи дополнительных настроек.

```ts
type YandexCheckoutOptions = {
    // Показывается рядом с суммой заказа.
    // По умолчанию: домен страницы, на которой открыт чекаут.
    shopName?: string;
    
    // Показывается рядом с названием магазина. Рекомендуемый размер 48x48.
    // По умолчанию: favicon страницы, на которой открыт чекаут.
    shopIcon?: string;
    
    // Используется в случаях, если на одном домене работает несколько разных магазинов.
    // По умолчанию: `/`
    baseUrl?: string;
    
    // Токен для сервисов Яндекса, которые проводят оплату напрямую через Trust.
    serviceToken?: string;
};
```

### YandexCheckoutState

Объект `YandexCheckoutState` используется для передачи состояния формы из `YandexCheckoutRequest` во Фронтенд магазина. Фронтенд может получить состояние через обработку событий (свойство `event.checkoutState`).

TypeScript интерфейс объекта:
```ts
type YandexCheckoutState = {
    // Коментарий к заказу
    comment?: string;
    
    // Значение поля с промокодом
    promoCode?: string;

    // Контакты покупателя
    // Note: поле доступно только после перехода к оплате (событие `paymentStart`)
    payerDetails?: {
        name?: string;
        email?: string;
        phone?: string;
    };

    orders: Array<{
        // Уникальный идентфикатор заказа
        id: string;

        // Город, если заполнен пользователем
        city?: {
            city: string;
            region?: string; // Область/округ/регион
            country?: string;
        },
        
        // Идентификатор способа доставки, если выбран
        shippingOption?: {
            id: string;
        };

        // Адрес доставки, если заполнен пользователем
        shippingAddress?: {
            rawAddress: string; // Ввод пользователя
            district?: string; // Район города
            street?: string;
            house?: string;
            // Подъезд, домофон, этаж, квартира и комментарий к адресу становятся доступны
            // только после перехода к оплате (событие `paymentStart`)
            porch?: string;
            intercom?: string;
            apartment?: string;
            floor?: string;
            comment?: string;
        };

        // Идентификатор пункта самовывоза, если выбран
        pickupOption?: {
            id: string;
        };

        // Идентификатор даты и времени доставки, если выбраны
        datetimeOption?: {
            id: string;
            timeOption?: {
                id: string;
            };
        };
    }>;

    // Выбранный способ оплаты, если выбран
    paymentOption?: {
        // Выбранный тип оплаты. Реквизиты банковской карты не доступны
        // – 'offline-cash' - оплата наличными
        // – 'offline-card' - картой при получении
        // – 'yandex-payments' - онлайн оплата через Яндекс Оплату
        // – 'online-external-payments' - онлайн оплата через внешние сервисы оплаты
        type: string;
        
        // Дополнительные данные для выбранного способа оплаты
        data?: object;
    };
};
```

### События

По мере заполнения формы заказа можно обновлять интерфейс: добавлять и удалять поля, менять доступные опции. Для этого нужно подписаться на события и передавать объект `YandexCheckoutDetailsUpdate` в метод `event.updateWith(details)`. Объект `YandexCheckoutDetailsUpdate` должен содержать только поля, значения которых были обновлены. 

TypeScript интерфейс объекта события:
```ts
type YandexCheckoutDetailsUpdate = Partial<YandexCheckoutDetails>;

type YandexCheckoutRequestUpdateEvent = {
    // Тип события, для которого вызван обработчик
    type: string;
    
    // Состояние формы на момент наступления события
    checkoutState: YandexCheckoutState;
    
    // Метод для обновления формы заказа
    updateWith(details: YandexCheckoutDetailsUpdate | Promise<YandexCheckoutDetailsUpdate>): void;
};
```

Пример обработки события:
```js
checkoutRequest.addEventListener('shippingOptionChange', event => {
    event.updateWith(details);
});
```

В метод `event.updateWith()` можно передать промис:
```js
checkoutRequest.addEventListener('shippingOptionChange', event => {
    event.updateWith(Promise.resolve(details));
});
```

Чтобы предотвратить блокировку интерфейса, метод `event.updateWith()` должен вызываться синхронно. При этом метод `event.updateWith()` можно вызвать только один раз. 
```js
// ✅ ОК
checkoutRequest.addEventListener('shippingOptionChange', event => {
    event.updateWith(details);
});

// ✅ ОК
checkoutRequest.addEventListener('shippingOptionChange', event => {
    event.updateWith(Promise.resolve(details));
});

// ❌ Не сработает
checkoutRequest.addEventListener('shippingOptionChange', async event => {
    // await гарантирвоано не дает синхронно вызвать метод updateWith()  
    const details = await getNewDetails();
    // throws "InvalidStateError".
    event.updateWith(details);
});

// ❌ Не сработает
checkoutRequest.addEventListener('shippingOptionChange', event => {
    // Первый вызов пройдет успешно
    event.updateWith(details);
    // Повторный вызов приведет к ошибке "InvalidStateError".
    event.updateWith(otherDetails);
});

// ❌ Не сработает
checkoutRequest.addEventListener('shippingOptionChange', async event => {
    const p = Promise.resolve(details);

    // Первый вызов пройдет успешно
    event.updateWith(p);

    await p;

    // throws "InvalidStateError".
    event.updateWith(newDetails);
});
```

#### Список событий

| Событие                 | Когда вызывается                                                              | Зачем нужно                                                                                                                                                                                                                                                                          |
| ----------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `restoreState`          | При открытии формы заказа                                                     | Для синхронизации сохраненных данных (адрес, способ доставки и тд) с Фронтендом магазина. В ответ на событие магазин может предзаполнить форму предоставленными данными, проставив нужные флаги в `YandexCheckoutDetails`. Так же можно произвести валидацию предзаполненных данных. | 
| `cityChange`            | При выборе или автоматическом определении города                              | Обновить способы доставки для выбранного города                                                                                                                                                                                                                                      |
| `shippingOptionChange`  | При выборе способа доставки                                                   | Обновить стоимость заказа с учетом способа доставки. Показать/скрыть форму ввода адреса доставки. Показать/скрыть выбор пункта самовывоза.                                                                                                                                           |
| `shippingAddressChange` | При изменении любых полей в адресе доставки. Может вызываться по мере набора. | Проверить, что по выбранному адресу осуществляется доставка. Обновить стоимость заказа с учетом адреса доставки.                                                                                                                                                                     |
| `pickupOptionChange`    | При выборе пункта самовывоза                                                  | Обновить стоимость заказа с учетом пункта самовывоза. Обновить доступные даты самовывоза.                                                                                                                                                                                            |
| `datetimeOptionChange`  | При выборе даты или времени доставки                                          | Обновить стоимость заказа с учетом даты и времени доставки.                                                                                                                                                                                                                          |
| `promoCodeChange`       | При изменении промокода. Может вызываться по мере набора.                     | Проверить действительность промокода. Обновить информацию о скидке по промокоду. Обновить стоимость заказа с учетом промокода.                                                                                                                                                       |
| `paymentOptionChange`   | При изменении способа оплаты                                                  | Обновить стоимость заказа с учетом способа оплаты.                                                                                                                                                                                                                                   |
| `paymentStart`          | Когда пользователь нажимает кнопку «Оплатить»                                 | Проверить правильность заполнения всех полей формы. В этот момент становятся доступны контакты покупателя, можно проверить формат телефона, например. Создать платеж в Яндекс Оплате, предоставить токен для проведения платежа.                                                     |
| `paymentError`          | При неудачной попытке оплаты заказа                                           | Возможность прервать оформление заказа (по умолчанию пользователь может попробовать оплатить повторно). Возможность залогировать ошибку оплаты на Бекенд магазина.                                                                                                                   |


### Результат оформления заказа

Результат оформления заказа доступен после закрытия формы заказа.

Метод `checkoutRequest.show()` возвращает промис. При успешном оформлении заказа промис завершен с результатом в виде объекта `YandexCheckoutState`. 

Промис может быть завершен с ошибокой в следующих случаях:
- Пользователь закрыл форму оформления заказа, не оплатив заказ. В этом случае будет ошибка `AbortError`.
- Фатальной ошибки формы заказа. Например, некорректные данные в `YandexCheckoutDetails`. 

Ошибки оплаты не приводят к ошибке оформления заказа. Пользователю будет предложено попробовать оплатить заказа еще раз.

Пример:
```js
const checkoutRequest = new YandexCheckoutRequest(details);

try {
    const checkoutState = await checkoutRequest.show();

    console.log(checkoutState);
    /*
     * {
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
} catch (err) {
    if (err.name === 'AbortError') {
        // Показываем пользователю сообщение об отмене оформления заказа
        alert('Оформление заказа отменено');
    } else {
        // Показываем пользователю сообщение об ошибке
        alert('Ошибка оформления заказа, попробуйте снова');
    }
    
    console.error(err);
}
```

## Примеры

В примерах используются функции, реализация которых опущена, так как зависит от конкретного магазина:
- `getPaymentTokenFromBackend(checkoutState)` - получает токен Яндекс Оплаты через Бекенд магазина. 
- `sendResponseToBackend(checkoutState)` - отправляет результат оформления заказа на Бекенд. 

### Заказ с фиксированной ценой

В случае, когда финальная стоимость заказа известна заранее (не зависит от заполнения формы заказа), можно передавать токен Яндекс Оплаты при создании `YandexCheckoutRequest`.

```js
async function checkout() {
    // Получаем токен Яндекс Оплаты с Бекенда. Стоимость заказа фиксирована, поэтому не передаем состояние формы заказа.
    const paymentToken = await getPaymentTokenFromBackend();
    
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { paymentToken },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     */
}
```

### Отложенное создание токена Яндекс Оплаты

Для создания токена Яндекс Оплаты необходимо знать финальную стоимость заказа. Если во время заполнения формы стоимость заказа может поменяться, то рекомендуется создавать токен в момент начала оплаты заказа. Это позволяет не создавать заказ в Яндекс Оплате на каждое изменение в форме оформления заказа. 

Для отложенного создания токена нужно использовать событие `paymentStart`. Событие вызывается в момент, когда пользователь корректно заполнил форму и готов перейти к оплате. В обработчике события нужно создать заказ в Яндекс Оплате и передать токен оплаты через метод `event.updateWith(details)`.

Пустой или некорректный `paymentToken` после обработки события `paymentStart` считается фатальной ошибкой, при которой форма оформления заказа будет закрыта с ошибкой `InvalidStateError`.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: {
                    // На данном этапе токен можно не указывать
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    request.addEventListener('paymentStart', event => {
        // Получаем токен Яндекс Оплаты с Бекенда с учетом состояния формы заказа, затем формируем объект YandexCheckoutDetailsUpdate
        const detailsPromise = getPaymentTokenFromBackend(event.checkoutState).then(paymentToken => {
            return {
                paymentOptions: [
                    {
                        type: 'yandex-payments',
                        data: {
                            // Обновляем токен для проведения платежа 
                            paymentToken,
                        },
                    },
                ],
            };
        });
        
        event.updateWith(detailsPromise);
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Оплата наличными

В случае оффлайн оплаты Яндекс Чекаут только собирает данные для оформления заказа и передает их магазину для дальнейшей обработки.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Оплата наличными
                type: 'offline-cash',
            },
            {
                // Оплата картой при получении
                type: 'offline-card',
            }
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: {
                    paymentToken: await getPaymentTokenFromBackend();
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'offline-card',
     *         data: {},
     *     }
     */
}
```

### Онлайн оплата через внешние сервисы оплаты

Для создания URL формы оплаты могут потребоваться данные из формы оформления заказа. URL формы оплаты можно создавать отложенно, что позволяет не создавать его на каждое изменение в форме оформления заказа.

Для отложенного создания URL формы оплаты нужно использовать событие `paymentStart`. Событие вызывается в момент, когда пользователь корректно заполнил форму и готов перейти к оплате. В обработчике события нужно сгенерировать URL формы оплаты и передать его через метод `event.updateWith(details)`.

Пустой или некорректный `paymentFormUrl` после обработки события `paymentStart` считается фатальной ошибкой, при которой форма оформления заказа будет закрыта с ошибкой `InvalidStateError`.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через внешние сервисы оплаты
                type: 'online-external-payments',
                data: {
                    // На данном этапе URL формы оплаты можно не указывать
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    request.addEventListener('paymentStart', event => {
        // Получаем URL формы оплаты с Бекенда с учетом состояния формы заказа, затем формируем объект YandexCheckoutDetailsUpdate
        const detailsPromise = getPaymentFormUrlFromBackend(event.checkoutState).then(paymentFormUrl => {
            return {
                paymentOptions: [
                    {
                        type: 'online-external-payments',
                        data: {
                            // Обновляем URL формы оплаты для проведения платежа
                            paymentFormUrl,
                        },
                    },
                ],
            };
        });
        
        event.updateWith(detailsPromise);
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отправляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'online-external-payments',
     *     }
     * }
     */
}
```

#### Настройка коллбэков для внешних сервисов оплат

На стороне внешнего сервиса онлайн оплат необходимо настроить коллбэки по возвращению в Чекаут. Необходимо указать три коллбэка на три события:
- При успешной оплате: `https://checkout.tap.yandex.ru/online-external-payments/success`
- При неудачной оплате: `https://checkout.tap.yandex.ru/online-external-payments/failed`
- При отмене оплаты: `https://checkout.tap.yandex.ru/online-external-payments/cancel`

### Обработка ошибки оплаты

Ошибки проведения платежа обрабатываются внутри формы оформления заказа. По умолчанию пользователю будет предложено попробовать оплатить заказ повторно. Чтобы изменить это поведение, либо просто логировать ошибки оплаты, нужно использовать событие `paymentError`.

```js
async function checkout() {
    // Получаем токен Яндекс Оплаты с Бекенда. Стоимость заказа фиксирована, поэтому не передаем состояние формы заказа.
    const paymentToken = await getPaymentTokenFromBackend();
    
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { paymentToken },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    request.addEventListener('paymentError', () => {
        // Логируем ошибку
        console.error('Ошибка проведения платежа');
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```


### Скидка за онлайн оплату

Для применения скидки используется событие `paymentOptionChange`, в котором пересчитывается итоговая стоимость заказа.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
            details: [
                {
                    label: 'Товар',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                }
            ]
        },
        
        paymentOptions: [
            {
                // Оплата наличными
                type: 'offline-cash',
            },
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { paymentToken },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Пересчитываем стоимость заказа при выборе способа оплаты
    request.addEventListener('paymentOptionChange', event => {
        if (event.checkoutState.paymentOption?.type === 'yandex-payments') {
            event.updateWith({
                // Итоговая стоимость заказа
                total: {
                    // Стоимость с учетом скидки
                    amount: {
                        value: 12490 * 100,
                        currency: 'RUB',
                    },
                    
                    // Добавляем информацию о скидке в детализацию стоимости заказа
                    details: [
                        {
                            label: 'Товар',
                            amount: {
                                value: 12990 * 100,
                                currency: 'RUB',
                            },
                        },
                        {
                            label: 'Скидка при онлайн оплате',
                            amount: {
                                value: -500 * 100,
                                currency: 'RUB',
                            },
                        }
                    ]
                },
            });
        } else {
            event.updateWith({
                // Итоговая стоимость заказа
                total: {
                    // Стоимость без скидки
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    
                    // Удаляем информацию о скидке из детализацию стоимости заказа
                    details: [
                        {
                            label: 'Товар',
                            amount: {
                                value: 12990 * 100,
                                currency: 'RUB',
                            },
                        }
                    ]
                },
            });
        }
    });
    
    request.addEventListener('paymentStart', event => {
        // Получаем токен Яндекс Оплаты с Бекенда с учетом состояния формы заказа, затем формируем объект YandexCheckoutDetailsUpdate
        const detailsPromise = getPaymentTokenFromBackend(event.checkoutState).then(paymentToken => {
            return {
                paymentOptions: [
                    {
                        type: 'offline-cash',
                    },
                    {
                        type: 'yandex-payments',
                        data: {
                            // Обновляем токен для проведения платежа 
                            paymentToken,
                        },
                    },
                ],
            };
        });
        
        event.updateWith(detailsPromise);
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Запрос контактов покупателя

Контакты пользователя становятся доступны только после события `paymentStart`. 

Если необходима валидация контактов, нужно использовать событие `paymentStart`, так как в `YandexCheckoutState` контакты не появятся до тех пор, пока не наступит событие `paymentStart`.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { 
                    // Токен Яндекс Оплаты для проведения платежа
                    paymentToken: await getPaymentTokenFromBackend(), 
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
        
        // Запрашиваем имя, телефон и email покупателя
        // Имя и телефон делаем обязательными для заполнения 
        payerDetails: [
            {
                type: 'name',
                require: true,
            },
            {
                type: 'phone',
                require: true,
            },
            {
                type: 'email',
                require: false,
            }
        ],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     payerDetails: {
     *         name: 'Максим',
     *         phone: '+79876543210',
     *         email: 'admin@yandex.ru',
     *     }
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Запрос адреса доставки

Чтобы запросить ввод адреса доставки, нужно передать флаг `requestShippingAddress`. Валидацию города, улицы и дома можно производить по событию `shippingAddressChange`.
Для получения подъезда, домофона, этажа, квартиры и комментария необходимо дождаться события `paymentStart`.
  
В примере проверяем возможность доставки по улице и номеру дома.

```js
async function checkout() {
    const details = {        
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: {
                    // Токен Яндекс Оплаты для проведения платежа
                    paymentToken: await getPaymentTokenFromBackend(),
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
            
            // Показываем форму выбора города
            requestCity: true,

            // Показываем форму для ввода адреса доставки
            requestShippingAddress: true,
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Проверяем зону доставки при заполнении адреса 
    request.addEventListener('shippingAddressChange', event => {
        const shippingAddress = event.checkoutState.orders[0].shippingAddress;
        
        if (shippingAddress?.street && shippingAddress?.house) {
            const promise = checkDeliveryZoneOnBackend(shippingAddress).then(isOk => {
                if (isOk) {
                    // Без ошибок
                    return {};
                } else {
                    // Показываем пользователю ошибки заполнения адреса
                    return {
                        validationErrors: {
                            orders: [{
                                id: 'order-123',
                                shippingAddress: {
                                    address: 'Не доставляем по указанному адресу',
                                }
                            }],
                        },
                    };
                }
            });
            
            event.updateWith(promise);
        }
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *         city: {
     *             country: 'Россия',
     *             region: 'Московская область',
     *             city: 'Москва',
     *         },
     *         shippingAddress: {
     *             street: 'Льва Толстого',
     *             house: '19/2',
     *             district: 'Хамовники',
     *             apartment: '13-2',
     *             porch: '2',
     *             intercom: '1-2-3-4',
     *             floor: '29',
     *             comment: 'Вход во двор с торца здания',
     *         },
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Варианты доставки в зависимости от города

В зависимости от города доставки, можно предложить пользователю разные способы доставки.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { 
                    // Токен Яндекс Оплаты для проведения платежа
                    paymentToken: await getPaymentTokenFromBackend(),
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
            
            // Показываем форму для ввода города
            requestCity: true,
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Обновляем способы доставки при изменении города
    request.addEventListener('cityChange', event => {
        const city = event.checkoutState.orders[0].city.city;
        
        switch(city) {
            case 'Москва':
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Для Москвы предлагаем самовывоз
                        shippingOptions: [
                            {
                                id: 'pickup',
                                label: 'Самовывоз',
                                datetimeEstimate: 'Сегодня',
                                amount: {
                                    value: 0,
                                    currency: 'RUB',
                                },
                            },
                            {
                                id: 'shipping',
                                label: 'Почта России',
                                datetimeEstimate: 'Через 2-3 дня',
                                amount: {
                                    value: 1000,
                                    currency: 'RUB',
                                },
                            },
                        ],
                    }]
                });
                break;
                
            case 'Санкт-Петербург':
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Для Санкт-Петербурга предлагаем только доставку почтой
                        shippingOptions: [
                            {
                                id: 'shipping',
                                label: 'Почта России',
                                datetimeEstimate: 'Через 2-3 дня',
                                amount: {
                                    value: 2000,
                                    currency: 'RUB',
                                },
                            },
                        ],
                    }]
                });
                break;
                    
            default:
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Если не выбран город, то не показываем варианты доставки
                        shippingOptions: [],
                    }]
                });
        }
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *         shippingOption: {
     *             id: 'pickup',
     *         },
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Самовывоз из магазина

В случае самовывоза нужно предоставить список магазинов через поле `pickupOptions`. 

В примере список магазинов зависит от города доставки.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { 
                    // Токен Яндекс Оплаты для проведения платежа
                    paymentToken: await getPaymentTokenFromBackend(),
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
            
            // Показываем форму для ввода города
            requestCity: true,
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Обновляем пункты самовывоза при изменении города
    request.addEventListener('cityChange', event => {
        const city = event.checkoutState.orders[0].city.city;
        
        switch(city) {
            case 'Москва':
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Магазины в Москве
                        pickupOptions: [
                            {
                                id: 'msk-shop-1',
                                label: 'Первый магазин в Москве',
                                address: 'м. Парк Культуры, ул. Льва Толстого, 17',
                                coordinates: {
                                    lon: 37.6173,
                                    lat: 55.755826,
                                },
                            },
                            {
                                id: 'msk-shop-2',
                                label: 'Второй магазин в Москве',
                                address: '40-летия Победы, 5',
                                coordinates: {
                                    lon: 37.6173,
                                    lat: 55.755826,
                                },
                            },
                        ],
                    }]
                });
                break;
                
            case 'Санкт-Петербург':
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Магазин в Санкт-Петербурге
                        pickupOptions: [
                            {
                                id: 'spb-shop',
                                label: 'Магазин в Санкт-Петербурге',
                                address: 'Невский проспект, 32',
                                coordinates: {
                                    lon: 37.6173,
                                    lat: 55.755826,
                                },
                            },
                        ],
                    }]
                });
                break;
                    
            default:
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Если не выбран город, то не показываем пункты самовывоза
                        pickupOptions: [],
                    }]
                });
        }
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *         pickupOption: {
     *             id: 'msk-shop-2',
     *         },
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Переключение между доставкой и самовывозом

Если пользователю одновременно доступны доставка и самовывоз из пунктов выдачи, то на форме оформления нужно показывать разные поля:
- Адрес доставки в случае выбора доставки
- Пункты самовывоза в случае выбора самовывоза

Управлять отображением полей нужно через событие `shippingOptionChange`. 

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { 
                    // Токен Яндекс Оплаты для проведения платежа
                    paymentToken: await getPaymentTokenFromBackend(),
                },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
            
            // Способы доставки
            shippingOptions: [
                {
                    id: 'pickup',
                    label: 'Самовывоз',
                    datetimeEstimate: 'Сегодня',
                    amount: {
                        value: 0,
                        currency: 'RUB',
                    },
                },
                {
                    id: 'shipping',
                    label: 'Почта России',
                    datetimeEstimate: 'Через 2-3 дня',
                    amount: {
                        value: 1000,
                        currency: 'RUB',
                    },
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Обновляем форму при выборе способа доставки
    request.addEventListener('shippingOptionChange', event => {
        const shippingOption = event.checkoutState.orders[0].shippingOption;
        
        switch(shippingOption?.id) {
            case 'pickup':
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Не показываем форму ввода адреса, если выбран самовывоз
                        requestShippingAddress: false,
                        
                        // Показываем пункты выдачи, если выбран самовывоз
                        pickupOptions: [
                            {
                                id: 'msk-shop-1',
                                label: 'Первый магазин в Москве',
                                address: 'м. Парк Культуры, ул. Льва Толстого, 17',
                                coordinates: {
                                    lon: 37.6173,
                                    lat: 55.755826,
                                },
                            },
                            {
                                id: 'msk-shop-2',
                                label: 'Второй магазин в Москве',
                                address: '40-летия Победы, 5',
                                coordinates: {
                                    lon: 37.6173,
                                    lat: 55.755826,
                                },
                            },
                        ],
                    }]
                });
                break;
                
            case 'shipping':
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Показываем форму ввода адреса, если выбрана доставка
                        requestShippingAddress: true,
                        
                        // Не показываем пункты выдачи, если выбрана доставка
                        pickupOptions: [],
                    }]
                });
                break;
                    
            default:
                event.updateWith({
                    orders: [{
                        // Уникальный идентификатор заказа
                        id: 'order-123',
                        
                        // Не показываем форму ввода адреса, если не выбран способ доставки
                        requestShippingAddress: false,

                        // Не показываем пункты выдачи, если не выбран способ доставки
                        pickupOptions: [],
                    }]
                });
        }
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * В случае выбора доставки:
     * {   
     *     orders: [{
     *         id: 'order-123',
     *         shippingOption: {
     *             id: 'shipping',
     *         },
     *         shippingAddress: {
     *             street: 'Льва Толстого',
     *             house: '19/2',
     *             district: 'Хамовники',
     *             apartment: '13-2',
     *             floor: '1',
     *         },
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     * 
     * В случае выбора самовывоза:
     * {   
     *     orders: [{
     *         id: 'order-123',
     *         shippingOption: {
     *             id: 'pickup',
     *         },
     *         pickupOption: {
     *             id: 'msk-shop-1',
     *         },
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Наценка за способ доставки

Для пересчета стоимости заказа нужно обрабатывать событие `shippingOptionChange`.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: {},
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
            
            // Способы доставки
            shippingOptions: [
                {
                    id: 'pickup',
                    label: 'Самовывоз',
                    datetimeEstimate: 'Сегодня',
                    amount: {
                        value: 0,
                        currency: 'RUB',
                    },
                },
                {
                    id: 'shipping',
                    label: 'Почта России',
                    datetimeEstimate: 'Через 2-3 дня',
                    amount: {
                        value: 1000 * 100,
                        currency: 'RUB',
                    },
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Обновляем форму при выборе способа доставки
    request.addEventListener('shippingOptionChange', event => {
        const shippingOption = event.checkoutState.orders[0].shippingOption;
        
        if (shippingOption?.id === 'shipping') {
            event.updateWith({
                // Итоговая стоимость заказа
                total: {
                    // Стоимость с учетом доставки
                    amount: {
                        value: 13990 * 100,
                        currency: 'RUB',
                    },
                    
                    // Добавляем информацию о доставке в детализацию стоимости заказа
                    details: [
                        {
                            label: 'Товар',
                            amount: {
                                value: 12990 * 100,
                                currency: 'RUB',
                            },
                        },
                        {
                            label: 'Доставка',
                            amount: {
                                value: 1000 * 100,
                                currency: 'RUB',
                            },
                        }
                    ]
                },
            });
        } else {
            event.updateWith({
                // Итоговая стоимость заказа
                total: {
                    // Стоимость без доставки
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    
                    // Удаляем информацию о доставке из детализацию стоимости заказа
                    details: [
                        {
                            label: 'Товар',
                            amount: {
                                value: 12990 * 100,
                                currency: 'RUB',
                            },
                        }
                    ]
                },
            });
        }
    });
    
    request.addEventListener('paymentStart', event => {
        // Получаем токен Яндекс Оплаты с Бекенда с учетом состояния формы заказа, затем формируем объект YandexCheckoutDetailsUpdate
        const detailsPromise = getPaymentTokenFromBackend(event.checkoutState).then(paymentToken => {
            return {
                 paymentOptions: [
                    {
                        type: 'yandex-payments',
                        data: {
                            // Обновляем токен для проведения платежа 
                            paymentToken,
                        },
                    },
                ],
            };
        });
        
        event.updateWith(detailsPromise);
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *         shippingOption: {
     *             id: 'pickup',
     *         },
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Выбор даты и времени доставки

В примере ниже доступные даты и время доставки зависит от способа доставки. При выборе самовывоза скрываем выбор даты и времени.

Доступные даты доставки могут зависеть от города, метода доставки, адреса и других данных. Обновлять данные о доступных датах нужно с помощью соответствующих событий. В примере данные обновляются в событии `shippingOptionChange`.

Так же в примере реализован пересчет стоимости заказа для утреннего и вечернего времени доставки.

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                type: 'yandex-payments',
                data: {},
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
            
            // Способы доставки
            shippingOptions: [
                {
                    id: 'pickup',
                    label: 'Самовывоз',
                    datetimeEstimate: 'Сегодня',
                    amount: {
                        value: 0,
                        currency: 'RUB',
                    },
                },
                {
                    id: 'courier',
                    label: 'Курьер',
                    datetimeEstimate: 'Через 2-3 дня',
                    amount: {
                        value: 0,
                        currency: 'RUB',
                    },
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Показываем/скрываем выбор даты и времени доставки в зависимости от способа доставки
    request.addEventListener('shippingOptionChange', event => {
        const shippingOption = event.checkoutState.orders[0].shippingOption;
        
        if (shippingOption?.id === 'courier') {
            event.updateWith({
                orders: [{
                    // Уникальный идентификатор заказа
                    id: 'order-123',
                    
                    // Для доставки курьером требуется выбор даты и времени
                    datetimeOptions: [
                         {
                            id: '2020-05-19',
                            date: '2020-05-19',
                            timeOptions: [
                                {
                                    id: '18-22',
                                    label: 'с 18:00 до 22:00',
                                    amount: {
                                        value: 100 * 100, // 100р наценка на доставку вечером
                                        currency: 'RUB',
                                    },
                                },
                            ],
                        },
                        {
                            id: '2020-05-20',
                            date: '2020-05-20',
                            selected: true,
                            timeOptions: [
                                {
                                    id: '8-22',
                                    label: 'с 08:00 до 22:00',
                                    amount: {
                                        value: 0,
                                        currency: 'RUB',
                                    },
                                    selected: true,
                                },
                                {
                                    id: '8-10',
                                    label: 'с 08:00 до 10:00',
                                    amount: {
                                        value: -100 * 100, // 100р скидка на доставку утром
                                        currency: 'RUB',
                                    },
                                },
                                {
                                    id: '18-22',
                                    label: 'с 18:00 до 22:00',
                                    amount: {
                                        value: 100 * 100, // Наценка на доставку вечером
                                        currency: 'RUB',
                                    },
                                },
                            ],
                        },
                    ],
                }]
            });
        } else {
            event.updateWith({
                orders: [{
                    // Уникальный идентификатор заказа
                    id: 'order-123',
                    
                    // Для самовывоза не требуется выбор даты и времени
                    datetimeOptions: [],
                }]
            });
        }
    });
    
    // Обновляем стоимость заказа в зависимости от времени доставки
    request.addEventListener('datetimeOptionChange', event => {
        const datetimeOption = event.checkoutState.orders[0].datetimeOption;
        
        switch(datetimeOption?.timeOption?.id) {
            // Наценка за доставку в вечернее время
            case '18-22':
                event.updateWith({
                    // Итоговая стоимость заказа
                    total: {
                        // Стоимость с учетом платной доставки
                        amount: {
                            value: 13090 * 100,
                            currency: 'RUB',
                        },
                        
                        // Добавляем информацию о платной доставке в детализацию стоимости заказа
                        details: [
                            {
                                label: 'Товар',
                                amount: {
                                    value: 12990 * 100,
                                    currency: 'RUB',
                                },
                            },
                            {
                                label: 'Доставка',
                                amount: {
                                    value: 100 * 100,
                                    currency: 'RUB',
                                },
                            }
                        ]
                    },
                });
                break;
                
            // Скидка за доставку в утреннее время
            case '8-10':
                event.updateWith({
                    // Итоговая стоимость заказа
                    total: {
                        // Стоимость с учетом скидки
                        amount: {
                            value: 12890 * 100,
                            currency: 'RUB',
                        },
                        
                        // Добавляем информацию о скидке в детализацию стоимости заказа
                        details: [
                            {
                                label: 'Товар',
                                amount: {
                                    value: 12990 * 100,
                                    currency: 'RUB',
                                },
                            },
                            {
                                label: 'Доставка',
                                amount: {
                                    value: -100 * 100,
                                    currency: 'RUB',
                                },
                            }
                        ]
                    },
                });
                break;
                
            // Стандартная стоимость доставки
            default:
                event.updateWith({
                    // Итоговая стоимость заказа
                    total: {
                        // Стоимость с учетом стандартной доставки
                        amount: {
                            value: 12990 * 100,
                            currency: 'RUB',
                        },
                        
                        // Добавляем информацию о бесплатной доставке в детализацию стоимости заказа
                        details: [
                            {
                                label: 'Товар',
                                amount: {
                                    value: 12990 * 100,
                                    currency: 'RUB',
                                },
                            },
                            {
                                label: 'Доставка',
                                amount: {
                                    value: 0,
                                    currency: 'RUB',
                                },
                            }
                        ]
                    },
                });
        }
    });
    
    request.addEventListener('paymentStart', event => {
        // Получаем токен Яндекс Оплаты с Бекенда с учетом состояния формы заказа, затем формируем объект YandexCheckoutDetailsUpdate
        const detailsPromise = getPaymentTokenFromBackend(event.checkoutState).then(paymentToken => {
            return {
                paymentOptions: [
                    {
                        type: 'yandex-payments',
                        data: {
                            // Обновляем токен для проведения платежа 
                            paymentToken,
                        },
                    },
                ],
            };
        });
        
        event.updateWith(detailsPromise);
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *         shippingOption: {
     *             id: 'courier',
     *         },
     *         datetimeOption: {
     *             id: '2020-05-20',
     *             timeOption: {
     *                 id: '8-22',
     *             },
     *         },
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Информация о скидке по акции

Информацию о скидках по акциям можно передавать в детализацию стоимости заказа.

```js
async function checkout() {
    // Получаем токен Яндекс Оплаты с Бекенда. Стоимость заказа фиксирована, поэтому не передаем состояние формы заказа.
    const paymentToken = await getPaymentTokenFromBackend();
    
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 10000 * 100,
                currency: 'RUB',
            },
            details: [
                {
                    label: 'Товар',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                },
                {
                    label: 'Скидка по акции',
                    amount: {
                        value: -2990 * 100,
                        currency: 'RUB',
                    },
                }
            ],
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { paymentToken },
            },
        ],
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Прием промокодов

Для обработки промокодов нужно:
1. Запросить ввод промокода через параметр `promoCode.request`
2. Обработать событие `promoCodeChange`, чтобы проверить действительность промокода и пересчитать стоимость заказа

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: {},
            },
        ],
        
        promoCode: {
            // Включаем отображение поля для ввода промокода
            request: true,
        },
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    count: 1,
                },
            ],
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Показываем/скрываем выбор даты и времени доставки в зависимости от способа доставки
    request.addEventListener('promoCodeChange', event => {
        const promoCode = event.checkoutState.promoCode;
        
        // Если промокода нет, то завершаем обработку события 
        if (!promoCode) {
            return;
        }
        
        if (promoCode === 'SUPER_200') {
            event.updateWith({
                // Итоговая стоимость заказа с учетом промокода
                total: {
                    amount: {
                        value: 12790 * 100,
                        currency: 'RUB',
                    },
                    details: [
                        {
                            label: 'Товар',
                            amount: {
                                value: 12990 * 100,
                                currency: 'RUB',
                            },
                        },
                        {
                            label: 'Промокод SUPER_200',
                            amount: {
                                value: -200 * 100,
                                currency: 'RUB',
                            },
                        },
                    ],
                },
                promoCode: {
                    value: 'SUPER_200',
                    amount: {
                        value: -200 * 100, // промокод на 200р
                        currency: 'RUB',
                    },
                },
            });
        } else {
            event.updateWith({
                // Итоговая стоимость заказа без промокода
                total: {
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                    details: [
                        {
                            label: 'Товар',
                            amount: {
                                value: 12990 * 100,
                                currency: 'RUB',
                            },
                        },
                    ],
                },
                promoCode: null,
                validationErrors: {
                    promoCode: 'Старый промокод',  
                },
            });
        }
    });

    request.addEventListener('paymentStart', event => {
        // Получаем токен Яндекс Оплаты с Бекенда с учетом состояния формы заказа, затем формируем объект YandexCheckoutDetailsUpdate
        const detailsPromise = getPaymentTokenFromBackend(event.checkoutState).then(paymentToken => {
            return {
                paymentOptions: [
                    {
                        type: 'yandex-payments',
                        data: {
                            // Обновляем токен для проведения платежа 
                            paymentToken,
                        },
                    },
                ],
            };
        });
        
        event.updateWith(detailsPromise);
    });
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     promoCode: 'SUPER_200',
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Предзаполнение формы для повторных заказов

При повторных заказах форма может быть [предзаполнена данными из предыдущего заказа](https://jing.yandex-team.ru/files/nodge/2020-07-06T17:19:31Z.da20bd4.png).

Для предзаполнения формы нужно обработать событие `restoreState`. В событии необходимо:
1. Добавить необходимые опции в объект `YandexCheckoutDetails` на основании уже заполненных данных в объекте `YandexCheckoutState`.
2. В объекте `YandexCheckoutDetails` проставить флаг `selected` для корректных опций, которые выбраны в объекте `YandexCheckoutState`. 
3. Произвести валидацию данных во всех полях объекта `YandexCheckoutState`, проставить ошибки валидаци по необходимости.

При этом автоматически будут заполнятся следующие данные:
- Контакты пользователя всегда заполняются автоматически, независимо от обработки события `restoreState`.
- Будут выбраны опции, которые совпадают по идентификатору и не имеют значений с флагом `selected: true`.
- Будут презаполнены текстовые поля, которые включены в текущем `YandexCheckoutDetails` (комментарий к заказу, адрес доставки).

```js
async function checkout() {
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 12990 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: {
                    // Токен Яндекс Оплаты для проведения платежа
                    paymentToken: await getPaymentTokenFromBackend(),
                },
            },
        ],
        
        promoCode: {
            // Включаем отображение поля для ввода промокода
            request: true,
        },
        
        orders: [{
            // Уникальный идентификатор заказа
            id: 'order-123',
            
            // Список товаров в заказе
            cartItems: [
                 {
                    title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                    amount: {
                        value: 12990 * 100,
                        currency: 'RUB',
                    },
                },
            ],
            
            // Показываем форму выбора города
            requestCity: true,

            // Показываем форму для ввода адреса доставки
            requestShippingAddress: true,
        }],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Валидируем адрес доставки из предыдущего заказа
    request.addEventListener('restoreState', event => {
        const orders = event.checkoutState.orders || [];
        const validationErrors = {
            orders: [],
        };
        
        for (const order of orders) {
            const address = order.shippingAddress;
            
            // Реализация функции `validateAddress` опущена для краткости
            if (!validateAddress(address)) {
                validationErrors.orders.push({
                    id: order.id,
                    shippingAddress: {
                        address: 'Адрес вне зоны доставки',
                    },
                });
            }
        }
        
        event.updateWith({ validationErrors });
    });

    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     promoCode: 'SUPER_200',
     *     orders: [{
     *         id: 'order-123',
     *     }],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

### Мульти-заказ

Если заказ состоит из нескольких посылок, то можно для каждой посылки указать свои методы доставки, адреса самовывоза и другие данные.

```js
async function checkout() {
    // Получаем токен Яндекс Оплаты с Бекенда. Стоимость заказа фиксирована, поэтому не передаем состояние формы заказа.
    const paymentToken = await getPaymentTokenFromBackend();
    
    const details = {
        // Итоговая стоимость заказа
        total: {
            amount: {
                value: 15980 * 100,
                currency: 'RUB',
            },
        },
        
        paymentOptions: [
            {
                // Онлайн оплата через Яндекс Оплату
                type: 'yandex-payments',
                data: { 
                    // Токен Яндекс Оплаты для проведения платежа
                    paymentToken,
                },
            },
        ],
        
        orders: [
            // Первая посылка
            {
                // Уникальный идентфикатор заказа
                id: 'order-1',
                
                // Список товаров в заказе
                cartItems: [
                     {
                        title: 'Смартфон Samsung Galaxy A30 64GB чёрный',
                        amount: {
                            value: 12990 * 100,
                            currency: 'RUB',
                        },
                        count: 1,
                    },
                ],
                
                // Способы доставки первой посылки
                shippingOptions: [
                    {
                        id: 'pickup',
                        label: 'Самовывоз',
                        datetimeEstimate: 'Сегодня',
                        amount: {
                            value: 0,
                            currency: 'RUB',
                        },
                    },
                    {
                        id: 'courier',
                        label: 'Курьер',
                        datetimeEstimate: 'Через 2-3 дня',
                        amount: {
                            value: 0,
                            currency: 'RUB',
                        },
                    },
                ],
            },
            
            // Вторая посылка
            {
                // Уникальный идентфикатор заказа
                id: 'order-2',
                
                // Список товаров в заказе
                cartItems: [
                    {
                        title: 'Чехол для Samsung Galaxy A30',
                        amount: {
                            value: 2990 * 100,
                            currency: 'RUB',
                        },
                        count: 1,
                    },
                ],
                
                // Способы доставки второй посылки
                shippingOptions: [
                    {
                        id: 'courier',
                        label: 'Курьер',
                        datetimeEstimate: 'Через 14 дней',
                        amount: {
                            value: 0,
                            currency: 'RUB',
                        },
                    },
                ],
            }
        ],
    };
    
    const request = new YandexCheckoutRequest(details);
    
    // Показываем форму оформления заказа
    const response = await request.show();
    
    // Отпраляем результат на Бекенд
    await sendResponseToBackend(response);
    
    console.log(response);
    /*
     * {   
     *     orders: [
     *         {
     *             id: 'order-1',
     *             shippingOption: {
     *                 id: 'pickup',
     *             },
     *         },
     *         {
     *             id: 'order-2',
     *             shippingOption: {
     *                 id: 'courier',
     *             },
     *         },
     *     ],
     *     paymentOption: {
     *         type: 'yandex-payments',
     *     }
     * }
     */
}
```

