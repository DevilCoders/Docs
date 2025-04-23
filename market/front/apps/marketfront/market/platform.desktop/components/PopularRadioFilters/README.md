# PopularRadioFilters

Популярные фильтры в выподающем контейнере.

## Примеры использования


### Пример 1. Несколько фильтров в списке
```jsx
const {isNoMatterValue} = require('@self/project/src/entities/filterSearch/filterRadio/getters');
const initialState = {
    filters: require('@self/platform/components/PopularRadioFilters/__fixtures__/filters.json')
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
                    isChecked: valueId === value.id,
                })),
            };
        })
    }));
};

<PopularRadioFilters
    filters={state.filters}
    onChange={onChangeHandler}
    onReset={onResetHandler}
/>
```

### Пример 2. Один фильтр в списке
```jsx
const {isNoMatterValue} = require('@self/project/src/entities/filterSearch/filterRadio/getters');
const radioFilter = require('@self/platform/components/PopularRadioFilters/__fixtures__/filter.json');
const initialState = {
    filters: [radioFilter],
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
                    isChecked: valueId === value.id,
                })),
            };
        })
    }));
};

<PopularRadioFilters
    filters={state.filters}
    onChange={onChangeHandler}
    onReset={onResetHandler}
/>
```
