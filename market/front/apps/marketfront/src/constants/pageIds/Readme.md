## Важно

Так как мы переносим все виджеты в `@self/root/src`, то необходимо поддерживать pageIds для двух Маркетов.

## Пример

Мы переносим какой-нибудь виджет из Покупок `@self/project/src`.
В этом виджете есть `<Link route={{pageId: PAGE_IDS_COMMON.ORDERS_TRACK}} .../>`,
значит нужно поддержать этот `ORDERS_TRACK` и в `index.market.(desktop|touch).js`
В противном случае вместо ссылки в белом Маркете будет `<span>`.

Если нет пока нет такой страницы на белом, то создать `external:...` ссылку.
```js
index.pokupki.js:
ORDERS_TRACK: 'blue-market:order-track',
```
```js
index.market.desktop.js
ORDERS_TRACK: 'market:order-track',
```
