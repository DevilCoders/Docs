# Сущность `product`

## `fetchProduct`

```typescript
fetchProduct: <ProductType = Product>(request: ProductRequest) => Promise<ProductResponse<ProductType>>;
```

Получает информацию о товаре. Используется на экране товара.

## `fetchProductsByCategory`

```typescript
fetchProductsByCategory: <ShortProductType = ShortProduct>(request: ProductsByCategoryRequest) => Promise<ProductsResponse<ShortProductType>>;
```

Получает список товаров категории и бренда.
Может поддерживать фильтрацию, сортировку и пагинацию.
Используется на экране категории и бренда, на главном экране.

## `fetchRecommendedProducts`

```typescript
fetchRecommendedProducts?: <ShortProductType = ShortProduct>(request: RecommendedProductsRequest) => Promise<ProductsResponse<ShortProductType>>;
```

Получает список рекомендованных товаров.
Учитывает `globalFilters`.
Может поддерживать пагинацию.
Используется на главном экране.

## `fetchRelatedProductsByProduct`

```typescript
fetchRelatedProductsByProduct?: <ShortProductType = ShortProduct>(request: ProductsByProductRequest) => Promise<ProductsResponse<ShortProductType>>;
```

Получает список товаров, связанных с товаром в запросе.
Учитывает `globalFilters` и `productId`.
Может поддерживать пагинацию.
Используется на экране товара.

## `fetchRecommendedProductsByProduct`

```typescript
fetchRecommendedProductsByProduct?: <ShortProductType = ShortProduct>(request: ProductsByProductRequest) => Promise<ProductsResponse<ShortProductType>>;
```

Получает список рекомендованных товаров по другому товару.
Учитывает `globalFilters` и `productId`.
Может поддерживать пагинацию.
Используется на экране товара.

## `fetchRecommendedProductsByCart`

```typescript
fetchRecommendedProductsByCart?: <ShortProductType = ShortProduct>(request: ProductsByCartRequest) => Promise<ProductsResponse<ShortProductType>>;
```

Получает список рекомендованных товаров по корзине.
Учитывает `globalFilters` и `cart`.
Может поддерживать пагинацию.
Используется на экране корзины.
