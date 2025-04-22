# SizeFilterPanel

Компонент для отображения значений фильтра размера. Значения выводятся в виде radio-группы значений.
Если в размерном фильтре содержиться несколько размерных шкал, то они будут отображены табами автоматически.

К консоле styleguidist можно посмотреть параметры, которые принимают обработчики событий компонента.

## Примеры использования

Обработчик изменения значения фильтра принимает три параметра: `filterId`, `valueId`, `value`, `filterType`, `unitId`.

### С одной размерной шкалой в фильтре
```jsx
const {isNoMatterValue} = require ('@self/project/src/entities/filterSearch/filterRadio/getters');
const initialState = require('@self/platform/components/SizeFilterPanel/fixtures/sizeFilterWithOneScale.json');
const [state, setState] = React.useState(initialState);
const onChangeHandler = (filterId, valueId, value, filterType, unitId) => {
    console.log(`onChange: filterId: ${filterId},` +
        `valueId: ${valueId}, value: ${value}, filterType: ${filterType}, unitId: ${unitId}`);

    setState({
        units: state.units.map(unit => ({
            ...unit,
            values: unit.values.map(value => ({
                ...value,
                isChecked: unitId === unit.id && valueId === value.id,
            })),
        })),
    });
};

const onResetHandler = (filterId, valueId, unitId) => {
    console.log(`onReset: filterId: ${filterId}`);

    setState({
        units: state.units.map(unit => ({
            ...unit,
            values: unit.values.map(value => ({
                ...value,
                isChecked: isNoMatterValue(value),
            })),
        })),
    });
};

<SizeFilterPanel
    filterId={state.id}
    units={state.units}
    onChange={onChangeHandler}
    onReset={onResetHandler}
    shouldDisplayTableSizeLink
    onLinkClick={() => console.log('Клик по ссылке таблицы размеров')}
    onChangeUnit={unitId => console.log(`onChangeUnit: active unitId: ${unitId}`)}
/>
```

### С несколькими размерными шкалами в фильтре
```jsx
const {isNoMatterValue} = require ('@self/project/src/entities/filterSearch/filterRadio/getters');
const initialState = require('@self/platform/components/SizeFilterPanel/fixtures/sizeFilterWithManyScales.json');
const [state, setState] = React.useState(initialState);
const onChangeHandler = (filterId, valueId, value, filterType, unitId) => {
    console.log(`onChange: filterId: ${filterId},` +
            `valueId: ${valueId}, value: ${value}, filterType: ${filterType}, unitId: ${unitId}`);

    const isNoMatterValue = valueId.endsWith('no_matter');

    setState({
        units: units.map(unit => ({
            ...unit,
            values: unit.values.map(value => ({
                ...value,
                isChecked: isNoMatterValue && value.id.endsWith('no_matter')
                    || (unitId === unit.id && valueId === value.id),
            })),
        })),
    });
};

const onResetHandler = (filterId, valueId, unitId) => {
    console.log(`onReset: filterId: ${filterId}`);

    setState({
        units: units.map(unit => ({
            ...unit,
            values: unit.values.map(value => ({
                ...value,
                isChecked: isNoMatterValue(value),
            })),
        })),
    });
};

<SizeFilterPanel
    defaultUnit={state.defaultUnit}
    filterId={state.id}
    units={state.units}
    onChange={onChangeHandler}
    onReset={onResetHandler}
    onLinkClick={() => console.log('Клик по ссылке таблицы размеров')}
    onChangeUnit={unitId => console.log(`onChangeUnit: active unitId: ${unitId}`)}
/>
```
