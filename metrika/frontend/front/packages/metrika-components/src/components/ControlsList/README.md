```(jsx)
const { CheckBox } = require('lego');
<ControlsList>
    <CheckBox checked={true} {...{size: 's', theme: 'normal'}}>Google Play</CheckBox>
    <CheckBox checked={true} {...{size: 's', theme: 'normal'}}>Yandex Launcher</CheckBox>
    <CheckBox {...{size: 's', theme: 'normal'}}>Smart-shortcut OEM</CheckBox>
</ControlsList>
```

```(jsx)
const { CheckBox } = require('lego');
<ControlsList direction="horizontal">
    <CheckBox checked={true} {...{size: 's', theme: 'normal'}}>Google Play</CheckBox>
    <CheckBox checked={true} {...{size: 's', theme: 'normal'}}>Yandex Launcher</CheckBox>
    <CheckBox {...{size: 's', theme: 'normal'}}>Smart-shortcut OEM</CheckBox>
</ControlsList>
```
