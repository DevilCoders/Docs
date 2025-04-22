# react-bem-components
Имплементация BEM Components в React

## Использование в браузере
Необходимо подключить `bem-components` одним из [способов](https://ru.bem.info/libs/bem-components/v2.3.0/#dist)

```js
var bemRegister = require('react-bem-components/lib/register');
var App = require('your-react-application');

modules.require(['BEMHTML', 'i-bem__dom', 'jquery'], function(bh, ibem, $) {
    bemRegister({
        bh: bh,
        ibem: ibem,
        jQuery: $
    });

    React.render(<App>, document.body);
});
```

## Использование на сервере
Для рендеринга компонентов необходим только бандл шаблонов BH, которые можно взять [здесь](https://ru.bem.info/libs/bem-components/v2.3.0/#Подключение-файлов-с-cdn)

```js
var bemRegister = require('react-bem-components/lib/register');
var bh = require('./templates/bem-components.bh');

var Input = require('react-bem-components/lib/Input');

bemRegister({
   bh: bh
});

console.log(React.renderToString(React.createElement(Input, {hasClear: true}))); // <span class="input input_has-clear input_size_m...
```

## Компоненты bem-components
- [Attach](./docs/attach.md)
- [Button](./docs/button.md)
- [Checkbox](./docs/checkbox.md)
- [Dropdown](./docs/dropdown.md)
- ~~Icon~~
- ~~Image~~
- [Input](./docs/input.md)
- [Link](./docs/link.md)
- [Menu](./docs/menu.md)
- [Modal](./docs/modal.md)
- [Popup](./docs/popup.md)
- [Progress](./docs/progress.md)
- [Radiogroup](./docs/radiogroup.md)
- [Select](./docs/select.md)
- [Spin](./docs/spin.md)
- [Textarea](./docs/textarea.md)

## Дополнительные bem компоненты, не входящие в bem-components

Для подключения дополнительных компонентов, можно использовать какие-либо кастомные сборки в сочетании с `bem-components`
и подключать их собранные `js` и `css` файлы описанным выше способом. Для них потребуется создание `react` обёртки с использованием `BemMixin`. Пример использования `BemMixin` можно посмотреть в исходниках готовых компонентов.

В данном разеделе описаны компоненты, вошедшие в сборку [ufo-bem-components](https://github.yandex-team.ru/UFO/ufo-bem-components):

- [Calendar](./docs/calendar.md)

## Создание нового компонента
