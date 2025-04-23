# Резолвер addItemToComparison

## Описание

Резолвер, добавляющий продукты в список сравнения (Comparison)


Параметры:

| Parameter | Type | Description | Default | Value |
|---------------|----------|------------------|------------------| ------- |
| `items`* | array | Массив элементов для добавления в список | - | - |
| `items.categoryId`** | number | id категории, он же hid | - | - |
| `items.productId`** | number | id товара | - | - |
\* - минимум один элемент<br>
\*\* — обязательный параметр

Пример параметров:
```
    items: [{
        categoryId: number,
        productId: number,
    }]
```


Ссылочки:

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/api/app/handlers/addItemToComparison/v2/constraints.js)

Возвращает пустой ответ
```
{
  "results": [
    {
      "handler": "addItemToComparison",
      "result": []
    }
  ],
  "collections": {}
}
```
