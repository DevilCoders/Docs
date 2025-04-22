Stateless компонент, показывает [попап](https://lego.yandex-team.ru/libs/islands/v5.27.0/desktop/popup2/examples/) через showDelay миллисекунд
```(jsx)
const { WithState } = require('utils/WithState');
<WithState state={{ visible: false }}>
    {(state, updateState) => (
        <HoverDropdown visible={state.visible} showDelay={500} onOpen={() => updateState({ visible: true })} onClose={() => updateState({ visible: false })}>
            <HoverDropdown.Anchor><span>Наведи на меня</span></HoverDropdown.Anchor>
            <HoverDropdown.Popup theme="normal" hasTail>Здарова!</HoverDropdown.Popup>
        </HoverDropdown>
    )}
</WithState>
```

Иногда нужно показывать попап при ховере на элемент, но относительно другого элемента
```(jsx)
const { WithState } = require('utils/WithState');
<WithState state={{ visible: false }}>
    {(state, updateState) => (
        <HoverDropdown visible={state.visible} showDelay={500} onOpen={() => updateState({ visible: true })} onClose={() => updateState({ visible: false })}>
            <HoverDropdown.Anchor>
                <span>Длинный длинный анкор, попап будет показан при ховере <HoverDropdown.HoverAnchor><span style={{ color: 'red' }}>на этот элемент</span></HoverDropdown.HoverAnchor> относительно всей строки</span>
            </HoverDropdown.Anchor>
            <HoverDropdown.Popup theme="normal" hasTail>Здарова!</HoverDropdown.Popup>
        </HoverDropdown>
    )}
</WithState>
```

[Тултип](https://lego.yandex-team.ru/libs/islands/v5.27.0/desktop/tooltip/examples/)
```(jsx)
const { WithState } = require('utils/WithState');
<WithState state={{ visible: false }}>
    {(state, updateState) => (
        <HoverDropdown visible={state.visible} showDelay={500} onOpen={() => updateState({ visible: true })} onClose={() => updateState({ visible: false })}>
            <HoverDropdown.Anchor><span>Наведи на меня</span></HoverDropdown.Anchor>
            <HoverDropdown.Tooltip theme="promo" tail={false}>Здарова!</HoverDropdown.Tooltip>
        </HoverDropdown>
    )}
</WithState>
```

```(jsx)
const { WithState } = require('utils/WithState');
<WithState state={{ visible: false }}>
    {(state, updateState) => (
        <HoverDropdown visible={state.visible} showDelay={500} onOpen={() => updateState({ visible: true })} onClose={() => updateState({ visible: false })}>
            <HoverDropdown.Anchor><span>Наведи на меня</span></HoverDropdown.Anchor>
            <HoverDropdown.Tooltip theme="success" tail>Здарова!</HoverDropdown.Tooltip>
        </HoverDropdown>
    )}
</WithState>
```
