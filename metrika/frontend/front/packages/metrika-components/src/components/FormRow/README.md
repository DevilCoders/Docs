Строка с минимальным набором параметров
```(jsx)
const { TextInput } = require('lego');

<FormRow size="s">
    <FormRow.Label>
        label
    </FormRow.Label>
    <FormRow.Control>
        <TextInput size="s" theme="normal" placeholder="а это контрол" />
    </FormRow.Control>
</FormRow>
```

Контрол на всю ширину
```(jsx)
const { TextInput } = require('lego');

<FormRow size="s" fullWidth={true}>
    <FormRow.Label>
        label
    </FormRow.Label>
    <FormRow.Control>
        <TextInput size="s" theme="normal" placeholder="а это контрол" />
    </FormRow.Control>
</FormRow>
```

Вертикальное положение лейбла и контролов
```(jsx)
const { TextInput, Button, CheckBox } = require('lego');
const { ControlsBar } = require('components');

<FormRow size="s" direction="vertical">
    <FormRow.Label>
        <span>это </span>
        <span>составной </span>
        <span>label</span>
    </FormRow.Label>
    <FormRow.Control>
        <ControlsBar size="s">
            <TextInput {...{size: 's', theme: 'normal'}} placeholder="а это составной" />
            <CheckBox {...{size: 's', theme: 'normal'}}>контрол</CheckBox>
            <Button theme="action" size="s">круто</Button>
        </ControlsBar>
    </FormRow.Control>
</FormRow>
```

Вертильный список, например внутри правой части. Отступы меняются в зависимости от пропса `size`
```(jsx)
const { TextInput, Button, CheckBox } = require('lego');
const { ControlsBar } = require('components');

<FormRow size="s">
    <FormRow.Label>
        Название
    </FormRow.Label>
    <FormRow.Control>
        <FormRow.List>
            <TextInput {...{size: 's', theme: 'normal'}} placeholder="Введите имя" />
            <CheckBox {...{size: 's', theme: 'normal'}}>Хэшированные данные</CheckBox>
        </FormRow.List>
    </FormRow.Control>
</FormRow>
```
