# Ручки статистики продвижения моделей
Ключ в стейте `vendorsModelsPromotionStatistics`.

**Структура стейта**
```js
    // Список подробных отчётов по моделям
    reportsByModel: [
        {
            modelId: 532046004,
            modelTitle: 'Электросамокат',
            metrics: {
                AVG_BID: 35.43076923076923,
                AVG_CLICK_PRICE: 13.296153846153844,
                CHARGES: 1037.1,
                CLICKS_PAID: 78,
                CLICKS_TOTAL: 206,
                CR: 0.026214818521960868,
                CTR_NEW: 0.24546602797836087,
                SHOWS: 83922,
                TARGET_ACTIONS: 22,
            },

            // Необязательные параметры для воспроизведения фильтрации
            promotionType: 'PROMOTED',
            platform: 'TOUCH',
            ppGroup: 'PREMIUM',
            date: 1633703400000,
        },
    ],
```

#### POST `/vendors/<vendorId>/modelbids/statistics/byModel`

Возвращает подробный отчёт по моделям с пагинацией.

##### URL параметры
- page `<number>` - номер страницы
- pageSize `<number>` - количество элементов на странице
- sortBy `<string>` - название метрики для сортировки (например, `CLICKOUTS_RATE`)
- sortOrder `<string>` - порядок сортировки (`ASC` или `DESC`)
- text `<string>` - фильтр по названию модели
- from `<number>` - фильтр по дате начала
- to `<number>` - фильтр по дате окончания
- platform `<string|string[]>` - фильтр по платформам
- promotionType `<string|string[]>` - фильтр по типам продвижения
- ppGroup `<string|string[]>` - фильтр по местам показа

##### Тело запроса
- models `<number[]>` - фильтр по моделям

##### Ответ
- result `<Object>` - результат работы ручки
    - item
        - items `<Object[]>`- список отчётов
        - pager `Object` - объект пейджера
- errors `<Array[Object]>` - список ошибок

#### POST `/vendors/<vendorId>/modelbids/statistics/total`

Возвращает сводные показатели по моделям.

##### URL параметры
- text `<string>` - фильтр по названию модели
- from `<number>` - фильтр по дате начала
- to `<number>` - фильтр по дате окончания
- platform `<string|string[]>` - фильтр по платформам
- promotionType `<string|string[]>` - фильтр по типам продвижения
- ppGroup `<string|string[]>` - фильтр по местам показа

##### Тело запроса
- models `<number[]>` - фильтр по моделям

##### Ответ
- result `<Object>` - результат работы ручки
    - item
        - metrics `<Object>`- коллекция метрик
          - AVG_BID `<number>` - средняя ставка
          - AVG_CLICK_PRICE `<number>` - средняя цена платного клика
          - CHARGES `<number>` - расходы
          - CLICKS_PAID `<number>` - платные клики
          - CLICKS_TOTAL `<number>` - все клики
          - CR `<number>` - конверсия
          - CTR_NEW `<number>` - CTR
          - SHOWS `<number>` - показы карточек товара
          - TARGET_ACTIONS `<number>` - целевые действия
- errors `<Array[Object]>` - список ошибок
