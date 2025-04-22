# CompareCharacteristics

Сравнение характеристик товаров

Красивое отображение сравнения двух товаров, характеристики выводятся в два столбца
В контейнере по VersusId получает сравнение из стора

Характеристики сгруппированы по смыслу, как приходят из компаризатора, название группы выводится как заголовок,
группы отделены горизонтальной полосой, в группах отсортированы только те характеристики, по
которым есть значение у обоих товаров

Для разных типов данных имееет разное отображение:
* boolean - BooleanCharacteristic - рисует крестик/галочку и название характеристики
* number -  NumberCharacteristic - рисует два прогресс-бара (максимальное из двух значение берем за 90%)
* enum color - ColorCharacteristic - рисует две группы кружочков с цветом
* enum остальные - SimpleCharacteristic - название характеристики: значение (через запятую, если несколько)

Пример использования с контейнером:
```jsx

const parametersGroups = [{
    areValuesEqual: false,
    params: [{
        parameters: [{
            areValuesEqual: false,
            name: 'A',
            type: 'boolean',
            subType: 'color',
            comparedItems: [{
                id: 0,
                values: [],
            }],
        }],
        title: 'A',
    }, {
        parameters: [{
            areValuesEqual: false,
            name: 'B',
            type: 'number',
            subType: 'color',
            comparedItems: [{
                id: 0,
                values: [],
            }],
        }],
        title: 'B',
    }],
}, {
    areValuesEqual: false,
    params: [{
        parameters: [{
            areValuesEqual: false,
            name: 'A',
            type: 'boolean',
            subType: 'color',
            comparedItems: [{
                id: 0,
                values: [],
            }],
        }],
        title: 'A',
    }, {
        parameters: [{
            areValuesEqual: false,
            name: 'B',
            type: 'number',
            subType: 'color',
            comparedItems: [{
                id: 0,
                values: [],
            }],
        }],
        title: 'B',
    }],
}];
<div>
    Нужен нормальный мок!
    <CompareCharacteristics parametersGroups={parametersGroups} />
</div>
```
