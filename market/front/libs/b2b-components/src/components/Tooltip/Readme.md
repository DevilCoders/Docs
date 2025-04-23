Всплывающий тултип для вывода более подробной информации (подсказок):

```jsx
const {question} = require('../Icon');
const {TooltipWithDropdown} = require('./');

<Container>
    <Text>Город</Text>
    <TooltipWithDropdown
        theme="help"
        to="right"
        toggler={<div><Icon src={question} /></div>}
    >
        <div>Укажите город Московской области</div>
    </TooltipWithDropdown>
</Container>
```

Тултип для вывода ошибок:

```jsx
const {TooltipWithDropdown} = require('./');

<Container>
    <Text>Попробуйте ещё раз</Text>
    <TooltipWithDropdown
        theme="error"
        to="bottom"
        toggler={<Text size="5"><Link>Вологда</Link></Text>}
    >
        <div>Не Московская область!</div>
    </TooltipWithDropdown>
</Container>
```

Простой тултип для информирования, боковое расположение:

```jsx
const {TooltipWithDropdown} = require('./');

<Container>
    <Text>Список городов</Text>
    <TooltipWithDropdown
        theme="primary"
        to="top"
        toggler={<Text size="5"><Link>Каких городов</Link></Text>}
    >
        <div>Городов Московской области</div>
    </TooltipWithDropdown>
</Container>
```
