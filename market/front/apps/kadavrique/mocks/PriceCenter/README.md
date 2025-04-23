# PriceCenter

Swagger: https://price-center.tst.vs.market.yandex.net/swagger-ui.html

Данные в стейте:
```js
{
    /**
     * Граф категорий - все узлы и список смежности
     * @see costsAndSalesCategories
     */
    categoriesTree: {
        nodes: [],
        adjTo: {},
    },

    /**
     * Список офферов
     * @see costsAndSalesOffers
     */
    offers: {
        data: [],
        totalCount: 0,
    },
    /**
     * Данные для графика в расходах и продажах
     * @see costsAndSalesDiagram
     */
    diagram: {
        series: [],
        total: [
            {
                param: 'click_count',
                values: [1, 3, 2],
            },
        ],
        timeScale: ['2018-09-11', '2018-09-12', '2018-09-13'],
        calculationType: 'AVERAGE',
    },

    /**
     * Режим работы страницы
     * @see costsAndSalesReportCalculationType
     */
    calculationType: {reportCalculationType: ['AVERAGE']},

    /**
     * Данные для таблицы на странице stat-placement
     * @see getPlacementStat
     */
    placementStatData: {
        table: {
            mostRecentDayWithData: '2020-01-08',
            total: 1,
            page: 1,
            pageSize: 10,
            rows: [{data: {}, metaData: {}}],
        },
    },

    /**
     * Данные о регионах
     * @see getRegions
     */
    regions: {
        id: 10000,
        name: 'Земля',
        parentId: 10000,
        regions: [],
        children: [],
    },

    /**
     * Данные о новых карточках модели
     * @see getNewModels
     */
    resultRows: [],
    totalCount: 3,
    page: 1,
    countPerPage: 10,
    categoriesTree: {
        nodes: [],
        adjTo: {},
    },
    offers: {
        data: [],
        totalCount: 0,
    },
    diagram: {
      series: [],
      total: [],
      timeScale: [],
      calculationType: 'AVERAGE'
    },
    calculationType: {
        reportCalculationType: [],
    },
    placementStatData: {
        entityRows: [],
        table: [],
    },
}
```

## Cтраница "Расходы и заказы"

### costsAndSalesCategories
Принимает на вход описание графа категорий и ids:string[]
Возвращает объекты соответствующие идентификаторам категорий в ids и их непосредственных детей в формате price-center.

### costsAndSalesOffers
Возвращает список оферов, отфильтрованный по категории (параметр ids:string[])

### costsAndSalesDiagram
Возвращает ровно то, что передали в ветке diagram

### costsAndSalesReportCalculationType
Возвращает ровно то, что передали в ветке calculationType

### getPlacementStat
Принимает на вход параметры фильтрации таблицы

```ts
detaliztion = "day" | "week" | "month" // (по дефолту "day")
entity = "clicks" | "views" | "costs"  // (по дефолту "clicks")
```

возвращает отфильтрованную таблицу
