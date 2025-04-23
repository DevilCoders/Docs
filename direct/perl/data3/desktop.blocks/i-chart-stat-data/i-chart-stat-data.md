#i-chart-stat-data

##Описание
Формирует параметры запроса. 
Преобразует полученные данные в список, где каждый элемент содержит заголовок для легенды(колонка, значение среза), тип столбца, тип среза и список точек. 

###Авторы 
[skywhale](https://staff.yandex-team.ru/skywhale)

###Где используется
В `b-charts-manager`   

##Пример

```
    // смотри jsdoc метода _getSubmitParams
    var params = {
            columns: ['shows'],
            groupBy: ['age'],
            cid: '1974074',
            groupByDate: 'quarter',
            withNds: 0,
            date: {
                from: '2016-02-21',
                to: '2017-02-20'
            },
            statType: 'mol',
            filters: {
                campaign: {
                    eq: ['1974074']
                },
                banner: {
                    eq: '1604522290'
                },
                targettype: {
                    eq: 'context'
                }
            }
    
        };

    BEM.blocks['i-chart-stat-data']
        .get(params)
        .then(function(data) {
            // если resolved            
        }, function(event, eventName) {
            //если rejected
        });
```
