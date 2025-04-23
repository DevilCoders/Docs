# ui-components
Общие элементы интерфейса для персональных сервисов

## Cборка
Использование библиотеки предполагает настроенную сборку [webpack](https://github.com/webpack/webpack) с [babel-loader](https://github.com/babel/babel-loader) для препроцессинга `.js` `.jsx` а так же связку [css-loader](https://github.com/webpack/css-loader), [postcss-loader](https://github.com/postcss/postcss-loader), [stylus-loader](https://github.com/shama/stylus-loader) для загрузки стилей

## Использование
```js
// Библиотека целиком
import UI from 'ui-components';
...
<UI.Header title="Hello" />

// Только необходимые компоненты
import Header from 'ui-components/lib/Header';
// То же самое, но без стилей
import Header from 'ui-components/lib/Header/Header.jsx';
...
<Header title="World" />
```

Для подключения только стилей можно воспользоваться `@import`

## Компоненты
- [Avatar](./docs/avatar.md)
- [Header](./docs/header.md)
- [Loader](./docs/loader.md)
- [Member](./docs/member.md)
- [Modal](./docs/modal.md)
- [Suggest](./docs/suggest.md)
