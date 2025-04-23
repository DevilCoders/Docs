#b-chart

##Описание
Блок для создания графика с помощь библиотеки highcharts

###Автор 
[grimfrid](https://staff.yandex-team.ru/grimfrid)
[skywhale](https://staff.yandex-team.ru/skywhale)

###Где используется
В `b-charts-manager`
   
###Взаимодействие с другими блоками
-
  
##Как пользоваться и расширять
- Если нужно добавить новый тип графика - добавляем модификатор view

## Модфикаторы
**view** - вид графика line/area/columns
**stacking** - переключает график в режим отображения "Среза" (см. пример)

##Roadmap & known issues
-

##Пример

Диаграмма с 2мя колонками одной размерности

```
    {
        block: 'b-chart',
        mods: {
            view: 'column'
        },
        js: {
            series: [
                {
                    column: 'shows',
                    name: 'Показы',
                    data: [
                        {
                            x: 1487538000000, 
                            y: 1016508 
                        },
                        {
                            x: 1487624400000, 
                            y: 948559 
                        }
                    ]
                },
                {
                    column: 'clicks',
                    name: 'Клики',
                    data: [
                        {
                            x: 1487538000000, 
                            y: 906508 
                        },
                        {
                            x: 1487624400000, 
                            y: 558559 
                        }
                    ]
                }
            ],
            options: {
                groupByDate: 'day'
            }
        }
    }
```

Диаграмма со срезом
```
    {
        block: 'b-chart',
        mods: {
            view: 'column',
            stacking: 'yes'
        },
        js: {
            series: [
                {
                    column: 'shows',
                    groupBy: 'gender',
                    name: 'Женский',
                    data: [
                        {
                            x: 1487538000000, 
                            y: 1016508 
                        },
                        {
                            x: 1487624400000, 
                            y: 948559 
                        }
                    ]
                },
                {
                    column: 'shows',
                    groupBy: 'gender',
                    name: 'Мужской',
                    data: [
                        {
                            x: 1487538000000, 
                            y: 906508 
                        },
                        {
                            x: 1487624400000, 
                            y: 558559 
                        }
                    ]
                }
            ],
            options: {
                groupByDate: 'day'
            }
        }
    }
```
