# Сущность `shop`

## `fetchShops`

```typescript
fetchShops: <ShopType = Shop>(request: ShopsRequest) => Promise<ShopsResponse<ShopType>>;
```

Получает список магазинов по поисковому запросу.
Учитывает `globalFilters` и `search`.
Может поддерживать фильтрацию и пагинацию.
Используется на экране выбора магазина в фильтрах.

## `fetchShopsByProduct`

```typescript
fetchShopsByProduct?: <ShopType = Shop>(request: ShopsByProductRequest) => Promise<ShopsByProductResponse<ShopType>>;
```

Получает список магазинов по наличию товара и поисковому запросу.
Учитывает `globalFilters`, `productId` и `search`.
Может поддерживать пагинацию.
Используется на экране товара при выборе магазина.
Возвращает магазины и доступные в них атрибуты товара.

## `fetchShopsByCart`

```typescript
fetchShopsByCart: <ShopType = Shop, ShortProductType = ShortProduct>(request: ShopsByCartRequest) => Promise<ShopsByCartResponse<ShopType, ShortProductType>>;
```

Получает список магазинов по наличию корзины в магазине и поисковому запросу.
Учитывает `globalFilters`, `cart` и `search`.
Может поддерживать пагинацию.
Используется на экране оформления заказа при выборе магазина.
Возвращает магазины и часть корзины, доступную в них.
