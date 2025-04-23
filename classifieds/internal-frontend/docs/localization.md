# Локализация

Локали вынесены в простые js словари, для вычисляемых значений используются шаблонные строки (локаль - функция, в которую передаем нужные значения).

```javascript
module.exports = {
    areaInfoTitle: 'Площадь',
    areaInfo: ({ value }) => `${value} м² общая`,
    ...
}
```

При необходимости плюрализации используем `internal-core/utils/pluralize.js`
```javascript
const pluralize = require('internal-core/utils/pluralize');

module.exports = {
    plural: ({ rooms }) => `${rooms} ${pluralize(rooms, 'комната', 'комнаты', 'комнат')}`,
}
```

Файлы локалей храним рядом с компонентом, именуем **i18n.js**
При необходимости мультилокалей будем использовать webpack и именовать файлы в виде **ru.i18n.js** - **en.i18n.js**
