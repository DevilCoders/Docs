 RadioButton
 ```jsx
 initialState = {value: 3};
 <RadioButton
     options={[
        {label: 'Пункт 1', value: 1},
        {label: 'Пункт 2', value: 2},
        {label: 'Пункт 3', value: 3},
        {label: 'Пункт 4', value: 4, disabled: true}
     ]}
     onChange={(value) => {
        setState({ value: value })
     }}
     name="radio1"
     value={state.value}
     onMouseEnter={() => console.log('onMouseEnter')}
     onMouseLeave={() => console.log('onMouseLeave')}
 />
 ```
Состояние с ошибкой

 ```jsx
 initialState = {value: 3};
 <RadioButton
     error={true}
     options={[
        {label: 'Пункт 1', value: 1},
        {label: 'Пункт 2', value: 2},
        {label: 'Пункт 3', value: 3},
        {label: 'Пункт 4', value: 4, disabled: true}
     ]}
     onChange={(value) => {
        setState({ value: value })
     }}
     name="radio1"
     value={state.value}
     onMouseEnter={() => console.log('onMouseEnter')}
     onMouseLeave={() => console.log('onMouseLeave')}
 />
 ```