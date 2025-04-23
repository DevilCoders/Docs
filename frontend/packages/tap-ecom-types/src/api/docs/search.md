# Поиск

## `suggest`

```typescript
suggest?: <SuggestItemType = SuggestItem>(request: SuggestRequest) => Promise<SuggestResponse<SuggestItemType>>;
```

Возвращает список наиболее подходящих под поисковый запрос подсказок
категорий, брендов и способов дополнить запрос.
Учитывает `globalFilters` и `search`.
Используется в режиме поиска как подсказка при наборе запроса.

## `search`

```typescript
search?: <BrandType = Brand, CategoryType = Category, ShortProductType = ShortProduct, SearchItemType = SearchItem>(request: SearchRequest) => Promise<ProductsResponse<BrandType, CategoryType, ShortProductType, SearchItemType>>;
```

Получает в поле `relevant` списки наиболее подходящих брендов, категорий и товаров
по поисковому запросу, которые будут отображаться в верхней части экрана поиска.
Также получает в поле `items` общий список брендов, категорий и товаров по поисковому запросу.
Учитывает `globalFilters` и `search`.
Может поддерживать пагинацию общего списка.
Используется на экране поиска.
