Фильтр по цвету

Пример использования:
```jsx
const {initialState} = require('@self/platform/components/ColorFilter/__fixtures__');

const [state, setState] = React.useState(initialState);

<ColorFilter
    name="colorPicker"
    colorList={state.colorList}
    onSelect={({value}) =>
        setState({
            colorList: state.colorList.map((el) => {
                if (el.id === value) {
                    return {...el, isChecked: true};
                }

                return {...el, isChecked: false};
            })
        })
    }
/>
```

Раскрытие фильтров при ограниченной ширине контейнера:
```jsx
const {initialState} = require('@self/platform/components/ColorFilter/__fixtures__');
const [state, setState] = React.useState(initialState);

<div style={{width: '200px'}}>
    <ColorFilter
        name="colorPicker"
        colorList={state.colorList}
        onSelect={({value}) =>
            setState((state) => ({
                colorList: state.colorList.map((el) => {
                    if (el.id === value) {
                        return {...el, isChecked: true};
                    }
    
                    return {...el, isChecked: false};
                })
            }))
        }
    />
</div>
```
