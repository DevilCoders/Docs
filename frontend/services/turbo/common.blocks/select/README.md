## Select

Можно передать в блок поле `state`, оно прокинется на клиент и будет использовать блок `state`, лежащий на `.page__result` для передачи подписчикам нового выбранного значения.

В `state` можно передать строку. Например, в поле `size` будет отправляться значение выбранного элемента селекта:
```js
{
    block: 'select',
    state: 'size'
}
```

В `state` можно передать объект. Например, в поле `size` будет отправляться значение, а в поле `sizeText` будет отправляться текст выбранного элемента:
```js
{
    block: 'select',
    state: {
        size: 'value',
        sizeText: 'text'
    }
}
```
