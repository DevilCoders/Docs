# Сущность `category`

Категории должны выстраиваться в дерево, для разных выбранных `globalFilters` и `brandId`
могут быть разные поддеревья, так как для разных глобальных фильтров и брендов категории отличаются.
У категорий должна быть одна корневая системная категория без данных, содержащая подкатегории
1го уровня.

## `fetchRootCategory`

```typescript
fetchRootCategory: <CategoryType = Category>(request: RootCategoryRequest) => Promise<RootCategoryResponse<CategoryType>>;
```

Получает информацию о подкатегориях системной корневой категории.
Это будут категории 1го уровня, они отображаются на экране каталога 1го уровня.
Учитывает `globalFilters`, `brandId`.

## `fetchCategory`

```typescript
fetchCategory: <CategoryType = Category>(request: CategoryRequest) => Promise<CategoryResponse<CategoryType>>;
```

Получает информацию о категории, а также информацию про все ее подкатегории.
Используется на экранах каталога, главном экране и экране категории.
Учитывает `globalFilters`, `brandId` и `categoryId`.
