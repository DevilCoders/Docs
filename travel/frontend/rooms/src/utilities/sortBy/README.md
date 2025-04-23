Функция для нескольких последовательных уровней сортировки

```js
const arr = [
    {
        a: 2,
        b: 3,
    },
    {
        a: 3,
        b: 2,
    },
    {
        a: 2,
        b: 4,
    },
    {
        a: 5,
        b: 2,
    },
];

arr.sort(
    sortBy((first, second) => {
        if (first.a > second.a) {
            return 1;
        }
        if (first.a < second.a) {
            return -1;
        }
        if (first.a === second.a) {
            return 0;
        }
    }).thenBy((first, second) => {
        if (first.b > second.b) {
            return 1;
        }
        if (first.b < second.b) {
            return -1;
        }
        if (first.b === second.b) {
            return 0;
        }
    }),
);

// "[{"a":2,"b":3},{"a":2,"b":4},{"a":3,"b":2},{"a":5,"b":2}]"
```
