Представляет собой раскладку для дименшена с чекбоксом и "разворачивалкой"

```(jsx)
<Dimension
    expandable
    expandedState="closed"
    color="blue"
    selectable
    selected
>Size S</Dimension>
<br />
<Dimension
    expandable
    expandedState="closed"
    color="blue"
    selectable
    selected
    size="m"
>Size M</Dimension>
```

По сравнению с `PlusExpander` принимает ещё одно значение в expandedState – `hidden`. Нужно для того, чтобы не было сдвигов дименшенов при отсутствии дочерних строк:
```(jsx)
<Dimension
    expandable
    expandedState="closed"
    color="blue"
    selectable
    selected
>Я могу раскрыться</Dimension>
<br />
<Dimension
    expandable
    expandedState="hidden"
    color="red"
    selectable
    selected
>У меня нет дочерних строк</Dimension>
<br />
<Dimension
    expandable
    expandedState="closed"
    color="yellow"
    selectable
>Но мы на одном уровне</Dimension>
```

Можно передать подсказку и если текст целиком не виден, то по ховеру отобразится тултип.

**_Важно_** чтобы всё работало верно, в контент нужно передавать `inline` элементы. В ином случае `text-overflow` работать не будет и контент некрасиво обрежется.

```(jsx)
<div style={{ width: '400px' }}>
    <Dimension
        expandable
        expandedState="closed"
        color="yellow"
        selectable
        hint="Lorem ipsum dolor sit amet"
    >
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam malesuada volutpat aliquet.
    </Dimension>
</div>
```

По умолчанию контент передаётся в `<label>`, поэтому при клике на текст произойдёт взаимодействие с чекбоксом. Иногда нужно вставить ссылку или другой контент, который сам обрабатывает клики:
```(jsx)
const { Link } = require('lego');
const { WithState } = require('utils/WithState');

<>
<WithState state={{ checked: true }}>
    {(state, updateState) => (
        <Dimension
            expandable={false}
            color="red"
            selectable
            selected={state.checked}
            onSelect={() => updateState({ checked: !state.checked })}
        >По клику на текст чекбокс изменится</Dimension>
    )}
</WithState>
<br />
<WithState state={{ checked: true }}>
    {(state, updateState) => (
        <Dimension
            expandable={false}
            color="blue"
            selectable
            selected={state.checked}
            onSelect={() => updateState({ checked: !state.checked })}
        >
            <Dimension.OutsideCheckboxContent>
                <Link theme="normal">По клику на текст чекбокс НЕ изменится. Нужно кликать на квадратик</Link>
            </Dimension.OutsideCheckboxContent>
        </Dimension>
    )}
</WithState>
</>
```

Можно отрендерить как без `PlusExpander`, так и без чекбокса. Например как в отчёте посещаемость
```(jsx)
<div style={{ maxWidth: '400px' }}>
    <Dimension
        hint="Lorem ipsum dolor sit amet"
    >
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam malesuada volutpat aliquet.
    </Dimension>
</div>
```
