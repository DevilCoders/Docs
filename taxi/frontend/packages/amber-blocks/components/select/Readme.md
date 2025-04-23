Компонент выпадающего списка c пунктами (используется https://github.com/JedWatson/react-select)

Выпадающий список с одним выбором
```jsx harmony
const RadioButton = require('../radio-button').default;
const Grid = require('../../styleguide/components/grid/Grid').default;

initialState = {theme: 'outline'};

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
         Тема:
         <br/><br/>
         <RadioButton
             options={[
                {label: 'Outline', value: 'outline'},
                {label: 'Underline', value: 'underline'}
             ]}
             onChange={(value) => {
                setState({ theme: value })
             }}
             name="theme"
             value={state.theme}
         />
    </Grid>
    <Grid item spacing={2} size={6}>
        M
    </Grid>
    <Grid item spacing={2} size={6}>
        L
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            theme={state.theme}
            placeholder="Выберите победителя ЧМ 2018"
            value={state.value || ''}
            options={[
              { value: 'russia', label: 'Россия' },
              { value: 'brazil', label: 'Бразилия' },
              { value: 'spain', label: 'Испания' },
              { value: 'germany', label: 'Германия' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            theme={state.theme}
            size="l"
            placeholder="Выберите победителя ЧМ 2018"
            value={state.value || ''}
            options={[
              { value: 'russia', label: 'Россия' },
              { value: 'brazil', label: 'Бразилия' },
              { value: 'spain', label: 'Испания' },
              { value: 'germany', label: 'Германия' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
</Grid>
```


Выпадающий список с длинным текстом в опции
```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
<Grid container spacing={2}>
    <Grid item spacing={2} size={6}>
        <p>без enableMultilineLabel</p>
        <div style={{width: '200px'}}>
            <SelectStyleguide
                placeholder="Выберите победителя ЧМ 2018"
                value={state.value || ''}
                options={[
                { value: 'russia', label: 'Россия' },
                { value: 'brazil', label: 'Бразилия' },
                { value: 'spain', label: 'Испания' },
                { value: 'germany', label: 'Германия' },
                { value: 'china', label: 'Китайская Народная Республика', title: 'Китайская Народная Республика' }
                ]}
                onChange={value => setState({ value })}
            />
        </div>
    </Grid>
    <Grid item spacing={2} size={6}>
        <p>с enableMultilineLabel</p>
        <div style={{width: '200px'}}>
            <SelectStyleguide
                enableMultilineLabel
                placeholder="Выберите победителя ЧМ 2018"
                value={state.value || ''}
                options={[
                { value: 'russia', label: 'Россия' },
                { value: 'brazil', label: 'Бразилия' },
                { value: 'spain', label: 'Испания' },
                { value: 'germany', label: 'Германия' },
                { value: 'china', label: 'Китайская Народная Республика', title: 'Китайская Народная Республика' }
                ]}
                onChange={value => setState({ value })}
            />
        </div>
    </Grid>
</Grid>


```

Выпадающий список со множественным выбором
```jsx harmony
const RadioButton = require('../radio-button').default;
const Grid = require('../../styleguide/components/grid/Grid').default;

initialState = {theme: 'outline'};

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
         Тема:
         <br/><br/>
         <RadioButton
             options={[
                {label: 'Outline', value: 'outline'},
                {label: 'Underline', value: 'underline'}
             ]}
             onChange={(value) => {
                setState({ theme: value })
             }}
             name="theme"
             value={state.theme}
         />
    </Grid>
    <Grid item spacing={2} size={6}>
        M
    </Grid>
    <Grid item spacing={2} size={6}>
        L
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            theme={state.theme}
            className="MultiSelect"
            multi
            placeholder="Выберите сервисы доставки еды"
            value={state.value || ''}
            options={[
              { value: 'foodfox', label: 'Foodfox' },
              { value: 'delivery', label: 'Delivery Club' },
              { value: 'netflix', label: 'Netflix' },
              { value: 'inst', label: 'Instagram' },
              { value: 'long', label: 'rjhglwkrghlw584utwlerkgjlw5;o8g9uw;lfjsglskjtgpw5gusfljghsfdkgls;dlgj' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            theme={state.theme}
            size="l"
            className="MultiSelect"
            multi
            placeholder="Выберите сервисы доставки еды"
            value={state.value || ''}
            options={[
              { value: 'foodfox', label: 'Foodfox' },
              { value: 'delivery', label: 'Delivery Club' },
              { value: 'netflix', label: 'Netflix' },
              { value: 'inst', label: 'Instagram' },
              { value: 'long', label: 'rjhglwkrghlw584utwlerkgjlw5;o8g9uw;lfjsglskjtgpw5gusfljghsfdkgls;dlgj' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
    <Grid item spacing={2} size={12}>
        без удаления
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            removeSelected={false}
            theme={state.theme}
            className="MultiSelect"
            multi
            placeholder="Выберите сервисы доставки еды"
            value={state.value || ''}
            options={[
              { value: 'foodfox', label: 'Foodfox' },
              { value: 'delivery', label: 'Delivery Club' },
              { value: 'netflix', label: 'Netflix' },
              { value: 'inst', label: 'Instagram' },
              { value: 'long', label: 'rjhglwkrghlw584utwlerkgjlw5;o8g9uw;lfjsglskjtgpw5gusfljghsfdkgls;dlgj' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            removeSelected={false}
            theme={state.theme}
            size="l"
            className="MultiSelect"
            multi
            placeholder="Выберите сервисы доставки еды"
            value={state.value || ''}
            options={[
              { value: 'foodfox', label: 'Foodfox' },
              { value: 'delivery', label: 'Delivery Club' },
              { value: 'netflix', label: 'Netflix' },
              { value: 'inst', label: 'Instagram' },
              { value: 'long', label: 'rjhglwkrghlw584utwlerkgjlw5;o8g9uw;lfjsglskjtgpw5gusfljghsfdkgls;dlgj' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
</Grid>
```

Выпадающий список - в режиме загрузки
```jsx harmony

<SelectStyleguide
    className="MultiSelect"
    isLoading
    placeholder="Выберите сервисы доставки еды"
    value={state.value || ''}
    options={[
      { value: 'foodfox', label: 'Foodfox' },
      { value: 'delivery', label: 'Delivery Club' },
      { value: 'netflix', label: 'Netflix' },
      { value: 'inst', label: 'Instagram' }
    ]}
    onChange={value => setState({ value })}
/>

```

Выпадающий список с ошибкой
```jsx harmony
const RadioButton = require('../radio-button').default;
const Grid = require('../../styleguide/components/grid/Grid').default;

initialState = {theme: 'outline'};

<Grid container spacing={2}>
    <Grid item spacing={2} size={12}>
         Тема:
         <br/><br/>
         <RadioButton
             options={[
                {label: 'Outline', value: 'outline'},
                {label: 'Underline', value: 'underline'}
             ]}
             onChange={(value) => {
                setState({ theme: value })
             }}
             name="theme"
             value={state.theme}
         />
    </Grid>
    <Grid item spacing={2} size={6}>
        M
    </Grid>
    <Grid item spacing={2} size={6}>
        L
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            error
            theme={state.theme}
            placeholder="Выберите сервисы доставки еды"
            value={state.value || ''}
            options={[
              { value: 'netflix', label: 'Netflix' },
              { value: 'inst', label: 'Instagram' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
    <Grid item spacing={2} size={6}>
        <SelectStyleguide
            error
            theme={state.theme}
            size="l"
            placeholder="Выберите сервисы доставки еды"
            value={state.value || ''}
            options={[
              { value: 'netflix', label: 'Netflix' },
              { value: 'inst', label: 'Instagram' }
            ]}
            onChange={value => setState({ value })}
        />
    </Grid>
</Grid>
```

Выпадающий список с возможностью добавить элемент
```jsx
const Creatable = require('./index').CreatableSelect;
<Creatable
    placeholder="Выберите сервисы доставки еды"
    options={[
      { value: 'netflix', label: 'Netflix' },
      { value: 'inst', label: 'Instagram' }
    ]}
    onChange={value => setState({ value })}
/>
```

Выпадающий список с асинхронной загрузкой элементов
```jsx harmony
const Async = require('./index').AsyncSelect;
const services = [
    { value: 'netflix', label: 'Netflix' },
    { value: 'inst', label: 'Instagram' }
];
const filterServices = (inputValue) => ({options: services.filter(i => i.label.toLowerCase().includes(inputValue.toLowerCase()))});
const loadOptions = (inputValue) => new Promise((resolve, reject) => {
    setTimeout(() => resolve(filterServices(inputValue)), 1000);
});
<Async
    placeholder="Выберите сервисы доставки еды"
    defaultOptions
    loadOptions={loadOptions}
/>
```
