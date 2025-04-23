**Рейтинг магазина**

### skkDisabled

```jsx

<ShopRatingSpread
    ratingToShow={3.8}
    grades={[]}
    skkDisabled
/>

```

### ratingToShow

```jsx
<ShopRatingSpread
    ratingToShow={3.2}
    grades={[]}
/>
```

```jsx
<ShopRatingSpread
    ratingToShow={4.9}
    grades={[
        {
            number: 3,
            percent: 0.14285714285714285,
            value: 1,
        }, {
            number: 4,
            percent: 0.19047619047619047,
            value: 2,
        }, {
            number: 4,
            percent: 0.19047619047619047,
            value: 3,
        }, {
            number: 4,
            percent: 0.19047619047619047,
            value: 4,
        }, {
            number: 6,
            percent: 0.2857142857142857,
            value: 5,
        },
    ]}
/>
```

### grades
Массив объектов типа `Grade` для отображения полосок с распределением оценок

```jsx
<ShopRatingSpread
    ratingToShow={3.2}
    grades={[
        {
            number: 3,
            percent: 0.14285714285714285,
            value: 1,
        }, {
            number: 4,
            percent: 0.19047619047619047,
            value: 2,
        }, {
            number: 4,
            percent: 0.19047619047619047,
            value: 3,
        }, {
            number: 4,
            percent: 0.19047619047619047,
            value: 4,
        }, {
            number: 6,
            percent: 0.2857142857142857,
            value: 5,
        },
    ]}
/>
```
