Доопределение леговского `TextInput`, добавляет `error` и `className`
```(jsx)
const { TextInput } = require('./TextInput');
<TextInput size="s" theme="normal" error text="" />
```

```(jsx)
const { TextInput } = require('./TextInput');
<TextInput size="s" theme="normal" error="Необходимо ввести имя" text="" />
```
