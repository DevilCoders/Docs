# Сущность `brand`

## `fetchBrands`

```typescript
fetchBrands: <BrandType = Brand>(request: BaseRequest) => Promise<BrandsResponse<BrandType>>;
```

Получает список всех брендов сервиса. Используется на экране каталога, брендов и бренда.
Учитывает `globalFilters`.
