# RadioFiltersPanel

Компонент для показа radio-фильтров в виде интерактивных табов с навигацией по hover. 

## Пример использования

В обработчик изменения значения фильтра передаются два параметра: `filterId`, `valueId`, `value`, `filterType`. 

В консоле styleguidist можно посмотреть параметры, которые принимают обработчики событий компонента.

### Пример 1. Несколько фильтров в списке
```jsx
const {isNoMatterValue} = require('@self/project/src/entities/filterSearch/filterRadio/getters');
const initialState = {
    filters: require('@self/platform/components/RadioFiltersPanel/__fixtures__/filters.json'),
};
const [state, setState] = React.useState(initialState);

const onChangeHandler = (filterId, valueId, value, filterType) => {
    console.log(`onChange: filterId: ${filterId}, valueId: ${valueId}, value: ${value}, filterType: ${filterType}`);
    
    setState(({filters}) => ({
        filters: filters.map(filter => {
             if (filterId !== filter.id) {
                 return filter;
             }
             
             return {
                 ...filter,
                 values: filter.values.map(value => ({
                     ...value,
                     isChecked: valueId === value.id,
                 })),
             };
         })
    }));
};

const onResetHandler = (filterId, valueId) => {
    console.log(`onReset: filterId: ${filterId}`);
    
    setState(({filters}) => ({
        filters: filters.map(filter => {
             if (filterId !== filter.id) {
                 return filter;
             }
             
             return {
                 ...filter,
                 values: filter.values.map(value => ({
                     ...value,
                     isChecked: isNoMatterValue(value),
                 })),
             };
         })
    }));
};

<RadioFiltersPanel
    filters={state.filters}
    onChange={onChangeHandler}
    onReset={onResetHandler}
/>
```

### Пример 2. Один фильтр в списке (фолбэк)
```jsx
const {isNoMatterValue} = require('@self/project/src/entities/filterSearch/filterRadio/getters');
const filter = require('@self/platform/components/RadioFiltersPanel/__fixtures__/filter.json');
const initialState = {
    filters: [filter],
};
const [state, setState] = React.useState(initialState);

const onChangeHandler = (filterId, valueId, value, filterType) => {
    console.log(`onChange: filterId: ${filterId}, valueId: ${valueId}, value: ${value}, filterType: ${filterType}`);
    
    setState(({filters}) => ({
        filters: filters.map(filter => {
             if (filterId !== filter.id) {
                 return filter;
             }
             
             return {
                 ...filter,
                 values: filter.values.map(value => ({
                     ...value,
                     isChecked: valueId === value.id,
                 })),
             };
         })
    }));
};

const onResetHandler = (filterId, valueId) => {
    console.log(`onReset: filterId: ${filterId}`);
    
    setState(({filters}) => ({
        filters: filters.map(filter => {
             if (filterId !== filter.id) {
                 return filter;
             }
             
             return {
                 ...filter,
                 values: filter.values.map(value => ({
                     ...value,
                     isChecked: isNoMatterValue(value),
                 })),
             };
         })
    }));
};

<RadioFiltersPanel
    filters={state.filters}
    onChange={onChangeHandler}
    onReset={onResetHandler}
/>
```
