**m-date_type_link**

Оборачивает дату ссылкой со значением `href = this.ctx.url`.

Пример:

```js
{
    block: 'm-date',
    mods: { type: 'link' },
    url: '/foo',
    timestamp: '2012-05-23'
}
```


**m-date_type_anchor**

Выведет обертку из ссылки-якоря со значением `href = this.ctx.url || unix time от this.ctx.timestamp`.
И рядом сгенерирует якорь с атрибутом `name` равному `href`

Пример:

```js
{
    block: 'm-date',
    mods: { type: 'anchor' },
    timestamp: '2012-05-23'
}
```
