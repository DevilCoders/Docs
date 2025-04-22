# Ручки услуг
Ключ в стейте `vendorProductsData`.

**Структура стейта**
```js
    list: {}, // объект, описывающий услуги
    requestPaymentUrl: 'about:blank', // значение по умолчанию ссылки для пополнения баланса
    transferStatus: true, // флаг успешности перевода средств
```


## Получение информации о продукте
`GET /vendors/<vendorId>/<productKey>`

К дефолтным параметрам подмешивает данные из стейта. Данные берутся из `list.{productKey}`. Значение `vendorId` — из параметров запроса.

**Дефолтные значения**
```js
    clientName: 'your-mama',
    orderId: 666,
    balance: 60000,
    expenses: 2000,
    monthExpenses: 500,
    placement: 'ACTIVE',
    clientId: 100200300,
    contractId: 0,
    offer: true,
    contractType: 1,
    tariffs: [],
    logins: [],
    activeCutoffTypes: [],
```

Если необходимо вернуть ошибку, например, нет доступа или услуга не подключена, в продукт достаточно добавить поле `error`, значение будет завернуто в стандартную ошибку бекенда.

**Пример данных услуги для которой будет возвращена ошибка**
```js
    error: {
        code: 'ENTITY_NOT_FOUND'
    }
```

## Получение доступных средств для перевода
`GET /vendors/<vendorId>/<productKey>/billing/availableTransfer`

Будет использовано свойство из стейта `balance` соответствующей услуги. Если услуга не определена в стейте, вернет дефолтное `10000`

## Перевод средств между услугами
`POST /vendors/<vendorId>/<productKey>/billing/makeTransfer/<toVendorId>/<toProductKey>`

Возвращает значение `transferStatus` из стейта.

## Перевод средств между услугами
`GET /vendors/<vendorId>/<productKey>/billing/availableTransfer`

Будет использовано свойство из стейта `balance` соответствующей услуги. Если услуга не определена в стейте, вернет дефолтное `10000`

## Получение ссылки на пополнение баланса
`POST /vendors/<vendorId>/<productKey>/billing/requestPayment`

Возвращает значение `requestPaymentUrl` из стейта.
