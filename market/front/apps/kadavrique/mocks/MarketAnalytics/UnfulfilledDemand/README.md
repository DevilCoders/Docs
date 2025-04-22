# Маркет.Аналитика

#### GET `/data/unfulfilledDemand/categories`

[Swagger UI](https://analytics.tst.vs.market.yandex.net/swagger-ui.html#/unfulfilled-demand-controller/getAvailableCategoriesUsingGET)

Данные в стейте:
```js
{
    /**
     * Список категорий, присутствующих в данных по незакрытому спросу
     */
    categories: [
        {
            hid: number, // id категории
            parentHid: number, // id родительской категории
            name: string, // название категории
        }
    ]
}
```

#### POST `/data/unfulfilledDemand`

[Swagger UI](https://analytics.tst.vs.market.yandex.net/swagger-ui.html#/unfulfilled-demand-controller/getUnfulfilledDemandUsingPOST)

Данные в стейте:
```
{
    /**
     * Получение данных по незакрытому спросу
     */
    models: {
        data: [{
            modelName: string, // название модели
            categoryName: string, // название категории
            departmentName: string, // название департамента
            categoryId: number, // id категории модели
            departmentId: number, // id департамента
        }],
        paging: {
            pageCount: number, // общее количество страниц
            pageNumber: number, //текущая выбранная страница
            rowsPerPage: number // количество записей на странице
        }
    }
}
```

Тело запроса:
```
{
    filters: {
        name: string, // фильтр по названию
        categories: number[], //  фильтр по категориям
        departments: number[], // фильтр по департаментам
    },
}
```
