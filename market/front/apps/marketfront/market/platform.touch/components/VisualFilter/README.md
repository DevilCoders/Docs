```jsx
const values = [
    {
        filterId: 'color',
        filterValue: {
            id: 'tomato',
            found: 10,
            code: 'tomato',
            value: 'tomato',
        },
    },
    {
        filterId: 'color',
        filterValue: {
            id: 'gold',
            found: 1,
            code: 'gold',
            value: 'gold',
        },
    },
    {
        filterId: 'color',
        filterValue: {
            id: 'green',
            found: 12,
            code: 'green',
            value: 'green',
        },
    }
];

const initialState = { activeValues: [] };
const onChange = ({filterId, value}) => {
    const activeValue = values.find((filter) => {
        return (
            filter.filterValue.value === value &&
            filter.filterId === filterId
        );  
    });
    
    setState({
        activeValues: [
            activeValue
        ],
    });
};


<div style={{width: '300px', border: '1px solid gray', borderRadius: '4px',  padding: '20px'}}>
    <VisualFilter
        title='Цвет'
        size='l'
        values={values}
        onValueChange={onChange}
        activeValues={state.activeValues}
        kind="product"
    />
</div>

```


#### С ограниченным числом одновременно показываемых фильтров (`maxValuesCount`)
```jsx

const values = [
    {
        filterId: 'color',
        filterValue: {
            id: 'tomato',
            found: 10,
            code: 'tomato',
            value: 'tomato',
        },
    },
    {
        filterId: 'color',
        filterValue: {
            id: 'gold',
            found: 1,
            code: 'gold',
            value: 'gold',
        },
    },
    {
        filterId: 'color',
        filterValue: {
            id: 'green',
            found: 12,
            code: 'green',
            value: 'green',
        },
    },
    {
        filterId: 'color',
        filterValue: {
            id: '#fff',
            found: 5,
            code: '#fff',
            value: '#fff',
        },
    },
    {
        filterId: 'color',
        filterValue: {
            id: 'blue',
            found: 19,
            code: 'blue',
            value: 'blue',
        },
    },
];

const initialState = {
    activeValues: [],
    maxValuesCount: 3,
};

const onChange = ({filterId, value}) => {
    const activeValue = values.find((filter) => {
        return (
            filter.filterValue.value === value &&
            filter.filterId === filterId
        );  
    });
    
    setState({
        activeValues: [
            activeValue
        ],
    });
};

const onAllFiltersClick = () => {
    setState({
        maxValuesCount: values.length   
    });
};

<div style={{width: '300px', border: '1px solid gray', borderRadius: '4px',  padding: '20px'}}>
    <VisualFilter
        title='Цвет'
        size='l'
        values={values}
        onValueChange={onChange}
        activeValues={state.activeValues}
        kind="product"

        maxValuesCount={state.maxValuesCount}
        onAllFiltersClick={onAllFiltersClick}
    />
</div>
```

####  Несколько boolean-фильтров в одном списке

```jsx
const values = [
    {
        filterId: 'boolean-1',
        filterName: 'Wi-Fi',
        filterValue: {
            id: 'tomato',
            found: 10,
            value: 'Wi-Fi',
        },
    },
    {
        filterId: 'boolean-2',
        filterName: 'Bluetooth',
        filterValue: {
            id: 'gold',
            found: 1,
            value: 'Bluetooth',
        },
    },
    {
        filterId: 'boolean-3',
        filterName: 'Веб-камера',
        filterValue: {
            id: 'green',
            found: 12,
            value: 'Веб-камера',
        },
    }
];

const initialState = { activeValues: [] };
const onChange = ({filterId, value}) => {
    const isAlreadyActive = Boolean(
        state.activeValues.find(filter => filter.filterId === filterId)
    );
    
    if (isAlreadyActive) {
        const activeValues = state.activeValues.filter(
            filter => filter.filterId !== filterId
        );
        
        setState({
            activeValues: activeValues,
        });
        
        return;
    }
    
    const activeValue = values.find((filter) => {
        return (
            filter.filterValue.id === value &&
            filter.filterId === filterId
        );  
    });
    
    setState({
        activeValues: [
            ...state.activeValues,
            activeValue
        ],
    });
};


<div style={{width: '300px', border: '1px solid gray', borderRadius: '4px',  padding: '20px'}}>
    <VisualFilter
        title='Особенности'
        size='auto'
        type={'boolean'}
        values={values}
        onValueChange={onChange}
        activeValues={state.activeValues}
        kind="product"
    />
</div>

```
