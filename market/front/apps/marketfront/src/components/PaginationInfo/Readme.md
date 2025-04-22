### Песочница
```jsx noeditor
<Helper.Playground
    component={PaginationInfo}
    defaultValues={{
        currentPage: 3,
        itemsCount: 82,
        itemsPerPage: 10
    }}
/>
```

### Примеры

#### Пример с выравниванеим по центру
```jsx
<PaginationInfo
    currentPage={3}
    itemsCount={82}
    itemsPerPage={10}
/>
```

#### Пример с выравниванеим по правой стороне `align={'right'}`
```jsx
<PaginationInfo
    currentPage={3}
    itemsCount={82}
    itemsPerPage={10}
    align={'right'}
/>
```
