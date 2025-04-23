# FilterEnumValuesLikeRadioList

Компонент для отображения списка значений `enum`-фильтра в виде radio-группы значений с единственным выбором и 
значением "Неважно". 

В обработчик изменения значения фильтра передаются два параметра: `filterId`, `valueId`, `value`, `filterType`. 

В консоле styleguidist можно посмотреть параметры, которые принимают обработчики событий компонента.

## Пример использования
Компонент чаще всего используется как структурный view-елемент при построения более комплексных отображений.

### Пример 1. Стандартный вариант использования
```jsx
const initialState = require('@self/platform/components/FilterEnumValuesLikeRadioList/__fixtures__/filter.json');
const {isNoMatterValue} = require('@self/project/src/entities/filterSearch/filterRadio/getters');

const [state, setState] = React.useState(initialState);
 
const onChangeHandler = (filterId, valueId, value, filterType) => {
    console.log(`onChage: filterId: ${filterId}, valueId: ${valueId}, value: ${value}, filterType: ${filterType}`);     

    setState(prevState => ({
        values: initialState.values.map(value => ({
            ...value,
            isChecked: valueId === value.id,
        })),    
    }));
};

const onResetHandler = (filterId) => {
    console.log(`onReset: filterId: ${filterId}`);     

    setState(prevState => ({
        values: initialState.values.map(value => ({
            ...value,
            isChecked: isNoMatterValue(value),
        })),    
    }));
};

<FilterEnumValuesLikeRadioList 
    withDefaultSelection
    filterId={state.id}
    values={state.values}
    onChange={onChangeHandler}
    onReset={onResetHandler}
/>
```
