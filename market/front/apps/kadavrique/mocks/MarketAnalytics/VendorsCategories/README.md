# Маркет.Аналитика

[Swagger UI](https://analytics.tst.vs.market.yandex.net/swagger-ui.html)

Данные в стейте:
```js
{
    /**
     * Список категорий партнёра
     */
    categories: [
        {
            name: 'Стики',
            hid: 18601530,
        },
    ],
}
```
#### GET `/partners/<partnerId>/categories`

Возвращает список подключённых категорий партнёра

##### Параметры
- **partnerId** `<number>` - идентификатор партнёра

##### Ответ
- **categories** `<Object[]>` - список категорий
- **partner** `<Object>` - информация о партнёре
    - **partner.type** `<string>` - тип партнёра (пока поддерживается только `VENDOR`)
    - **partner.id** `<number>` - идентификатор партнёра
