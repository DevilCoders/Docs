```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;
const Taxicar = require('../icon/Taxicar').default;
const RadioButton = require('../radio-button').default;

initialState = {theme: 'outline', value: ''};

const componentProps = {
    placeholder: `Поле с темой ${state.theme}`,
    theme: state.theme,
    value: state.value,
    onChange: (value) => setState(prevState => ({...prevState, value}))
};

function toNumber(v) {
    if (!v) {
        return undefined;
    }

    if (v === '-' || v.endsWith('.')) {
        return v;
    }

    v = parseFloat(v);

    if (!v && v !== 0) {
        return undefined;
    }

    return v;
}

function handleNumberChange(value) {
    setState(prevState => ({...prevState, value: toNumber(value)}))
}

<Grid container spacing={2} style={{width: 600}}>
    <Grid item spacing={2} size={12}>
         Тема:
         <br/><br/> 
         <RadioButton
             options={[
                {label: 'Outline', value: 'outline'},
                {label: 'Underline', value: 'underline'},
                {label: 'Go', value: 'go'}
             ]}
             onChange={(value) => {
                setState(prevState => ({ ...prevState, theme: value }))
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
    
    <Grid item spacing={2} size={12}>
        Простой
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} needPlaceholderWithValue size="m" />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} needPlaceholderWithValue size="l" />
    </Grid>
    
    <Grid item spacing={2} size={12}>
        С крестиком
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="m" />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="l" />
    </Grid>

    <Grid item spacing={2} size={12}>
        Заблокирован
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="m" disabled />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="l" disabled />
    </Grid>
    
    <Grid item spacing={2} size={12}>
        С ошибкой
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="m" error />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="l" error />
    </Grid>
    
    <Grid item spacing={2} size={12}>
        С иконкой слева
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} needPlaceholderWithValue size="m" iconLeft={<Taxicar />} />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} needPlaceholderWithValue size="l" iconLeft={<Taxicar />} />
    </Grid>
    
    <Grid item spacing={2} size={12}>
        С иконкой справа
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="m" iconRight={<Taxicar />} />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="l" iconRight={<Taxicar />} />
    </Grid>
    
    <Grid item spacing={2} size={12}>
        С текстом ошибки
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="m" error errorText="Текст ошибки" />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="l" error errorText="Текст ошибки" />
    </Grid>

    <Grid item spacing={2} size={12}>
        С иконкой очищения, при  наличии значения
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="m" clear />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="l" clear />
    </Grid>

    <Grid item spacing={2} size={12}>
        С кастомным колбэком
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="m" clear onChange={handleNumberChange} />
    </Grid>
    <Grid item spacing={2} size={6}>
        <Input {...componentProps} size="l" clear onChange={handleNumberChange} />
    </Grid>
</Grid>
```

Можно прокинуть нативные html аттрибуты

```jsx harmony
<Input autoComplete="off" autoCorrect="off" autoCapitalize="off" spellCheck={false} />
```
