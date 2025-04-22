Виджет "Уведомление"
======

Универсальный обработчик уведомлений (плашки сверху экрана).

Для показа предназначен экшен `showNotification` из [actions/notification](https://github.yandex-team.ru/market/mobile/blob/develop/actions/notification.js).

Пример вызова:
```javascript
showNotification({
    // идентификатор для метрики
    id: 'add-to-wishlist',
    // Отображаемое сообщение.
    message: 'Товар добавлен в избранное',
    // Тип плашки: 'info' - черный, 'error' - красная. По умолчанию 'info'.
    type: 'info', // тип
    // Через сколько миллисекунд плашка будет автоматически скрыта. По умолчанию 2000.
    delay: 6000,
    // На уведомление можно кликнуть и перейти по ссылке
    link: buildUrl('touch:wishlist'),
    // Желтый текст, объясняющий действие по тапу
    callToAction: 'Перейти в избранное',
})

```
