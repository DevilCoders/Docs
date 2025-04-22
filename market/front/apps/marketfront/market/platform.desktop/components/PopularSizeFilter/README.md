# PopularSizeFilter

Популярный фильтр размера в выподающем контейнере.


## Примеры использования

### Пример 1. Несколько размерных сеток в фильтре
```jsx
const {isNoMatterValue} = require('@self/project/src/entities/filterSearch/filterRadio/getters');
const initialState = {
    filter: require('@self/platform/components/PopularSizeFilter/__fixtures__/sizeFilterWithManyScales.json')
};
const [state, setState] = React.useState(initialState);
const onChangeHandler = (filterId, valueId, value, filterType, unitId) => {
    console.log(`onChange: filterId: ${filterId},` +
        `valueId: ${valueId}, value: ${value}, filterType: ${filterType}, unitId: ${unitId}`);
    
    const isNoMatterValue = valueId.endsWith('no_matter');

    setState(({filter}) => ({
        filter: {
            ...filter,
            units: filter.units.map(unit => ({
                ...unit,
                values: unit.values.map(value => ({
                    ...value,
                    isChecked: isNoMatterValue && value.id.endsWith('no_matter')
                        || (unitId === unit.id && valueId === value.id),
                })),
            })),
        },
    }));
};
const onResetHandler = (filterId, valueId, unitId) => {
    console.log(`onReset: filterId: ${filterId}`);

    setState(({filter}) => ({
        filter: {
            ...filter,
            units: filter.units.map(unit => ({
                ...unit,
                values: unit.values.map(value => ({
                    ...value,
                    isChecked: isNoMatterValue(value),
                })),
            })),
        },
    }));
};
<PopularSizeFilter
    filter={state.filter}
    onChange={onChangeHandler}
    onReset={onResetHandler}
    onLinkClick={() => console.log('Клик по ссылке таблицы размеров')}
/>
```

### Пример 2. Одна размерная сетка в фильтре
```jsx
const {isNoMatterValue} = require('@self/project/src/entities/filterSearch/filterRadio/getters');
const initialState = {
    filter: require('@self/platform/components/PopularSizeFilter/__fixtures__/sizeFilterWithOneScale.json')
};
const [state, setState] = React.useState(initialState);
const onChangeHandler = (filterId, valueId, value, filterType, unitId) => {
    console.log(`onChange: filterId: ${filterId},` +
        `valueId: ${valueId}, value: ${value}, filterType: ${filterType}, unitId: ${unitId}`);

    setState(({filter}) => ({
        filter: {
            ...filter,
            units: filter.units.map(unit => ({
                ...unit,
                values: unit.values.map(value => ({
                    ...value,
                    isChecked: unitId === unit.id && valueId === value.id,
                })),
            })),
        },
    }));
};
const onResetHandler = (filterId, valueId, unitId) => {
    console.log(`onReset: filterId: ${filterId}`);

    setState(({filter}) => ({
        filter: {
            ...filter,
            units: filter.units.map(unit => ({
                ...unit,
                values: unit.values.map(value => ({
                    ...value,
                    isChecked: isNoMatterValue(value),
                })),
            })),
        },
    }));
};
<PopularSizeFilter
    filter={state.filter}
    onChange={onChangeHandler}
    onReset={onResetHandler}
    onLinkClick={() => console.log('Клик по ссылке таблицы размеров')}
/>
```
