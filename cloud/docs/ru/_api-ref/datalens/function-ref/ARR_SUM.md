---
editable: false
---

# ARR_SUM



#### Синтаксис {#syntax}


```
ARR_SUM( array )
```

#### Описание {#description}
Возвращает сумму элементов в массиве `array`.

**Типы аргументов:**
- `array` — `Массив дробных чисел | Массив целых числел`


**Возвращаемый тип**: Зависит от типов аргументов

{% note info %}

Функция не работает для массивов с `Nullable` элементами. Чтобы удалить из массива элементы, равные `NULL`, используйте [REPLACE](REPLACE_ARRAY.md).

{% endnote %}


#### Пример {#examples}



| **[int_array]**   | **[float_array]**   | **ARR_SUM([int_array])**   | **ARR_SUM([float_array])**   |
|:------------------|:--------------------|:---------------------------|:-----------------------------|
| `'[21,12,0]'`     | `'[14.3,0.42,15]'`  | `33`                       | `29.72`                      |
| `'[-4,12,0]'`     | `'[0,-3,12]'`       | `8`                        | `9.00`                       |
| `'[5,7,9]'`       | `'[3.2,2.3,3.2]'`   | `21`                       | `8.70`                       |




#### Поддержка источников данных {#data-source-support}

`ClickHouse 21.8`.
