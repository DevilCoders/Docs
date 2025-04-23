Компонент фильтра-диапазона.

### Пример

```jsx
    <RangeFilter
        filterId="glprice"
        defaultFilterState={{from: '', to: ''}}
        isResetButtonVisible={false} 
        initialMin="1"
        initialMax="100"
        onChange={(filterId, state) => console.log(state)}
        onReset={(filterId) => console.log(filterId)}
    />
```
