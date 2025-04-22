# RatingDistribution

Блок распределения оценок

Содержит звездочки и прогресс-бар напротив них.

Пример использования:
```jsx
const grades = [
    {value: 5, number: 5, percent: 50},
    {value: 4, number: 5, percent: 50},
    {value: 3, number: 0, percent: 0},
    {value: 2, number: 0, percent: 0},
    {value: 1, number: 0, percent: 0},
];

<RatingDistribution grades={grades} />

```
