# ReasonToBuyBest

Бейджик "Выбор покупателей"

Отображается на сниппетах модели или на КМ при наличии свойства:
```json
{
    "entity": "product",
    "reasonsToBuy": [{
      "id": "best_by_factor",
      "factor_name": "звук",
      "factor_priority": "0"
    }, {
     "id": "best_by_factor",
     "factor_name": "качество фотографий",
     "factor_priority": "2"
   }, {
     "id": "best_by_factor",
     "factor_name": "мощный процессор",
     "factor_priority": "3"
   }]
}
```

Дефолтный вид:
```jsx
const reasons = ['звук', 'качество фотографий', 'мощный процессор'];

<ReasonToBuyBest list={reasons} view="full" />
```

Укороченный вид с иконкой и тултипом при наведении:
```jsx
const reasons = ['звук', 'качество фотографий', 'мощный процессор'];

<ReasonToBuyBest list={reasons} view="short" />
```
