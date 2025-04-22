```(jsx)
const { TextInput, Button, Tumbler, CheckBox } = require('lego');

<ControlsBar size='s'>
    <TextInput {...{size: 's', theme: 'normal'}} />
    <Button {...{size: 's', theme: 'normal'}}>say hi</Button>
    <Tumbler {...{size: 's', theme: 'normal'}} />
    <CheckBox checked={true} {...{size: 's', theme: 'normal'}}>лицензионное соглашение</CheckBox>    
</ControlsBar>
```
