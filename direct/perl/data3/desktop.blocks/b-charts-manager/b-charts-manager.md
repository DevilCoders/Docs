#b-charts-manager

##Описание
Получение данных с сервера и построение графиков.
Без модификатора place бесполезен. 

###Авторы 
[skywhale](https://staff.yandex-team.ru/skywhale )
[grimfrid](https://staff.yandex-team.ru/grimfrid )

###Где используется
В `p-campaing-stat_type_mol`
   
###Взаимодействие с другими блоками
Взаимодействует с блоками: 
* `b-chart-filters` - Управляет фильтрами, подписываемся на его `change` и при изменении перестраиваем график.
* `i-chart-stat-data` - По выбранным фильтрам соверщает запрос за данными
* `b-chart` - Строит график 
  
##Как пользоваться и расширять
Переопределить методы для использование в конкретном месте можно с помощью
модификатора `place`

## Модфикаторы
- `place` - для тонкой настройки 

##Roadmap & known issues
-

##Пример

```
{
    block: 'b-charts-manager',
    js: {
        clientCurrency: 'RUB',
        reportData: {
            filters: {},
            groupByDate: 'day',
            withNds: 1,
            date: { from: '2017-02-09', to: '2017-02-16' }
        }
    },
    content: [
        { elem: 'switcher' },
        {
            elem: 'filters',
            mods: { limits: 'columns-groups' },
            columns: [
                { text: 'Показы', value: 'shows', selected: 'yes' },
                { text: 'Клики', value: 'clicks' },
                { text: 'CTR, %', value: 'ctr' },
                { text: 'Цена, руб', value: 'price' }
            ],
            groups: [
                { text: 'Пол', value: 'gender', group: 'gender', selected: 'yes' },
                { text: 'Возраст', value: 'age', group: 'age' }
            ]
        },
        {
            elem: 'export',
            types: [
                { text: 'PNG', MIME: 'image/png' },
                { text: 'JPEG', MIME: 'image/jpeg' },
                { text: 'SVG', MIME: 'image/svg+xml' }
            ],
            print: true
        },
        { elem: 'chart' }
    ]
} 
```
