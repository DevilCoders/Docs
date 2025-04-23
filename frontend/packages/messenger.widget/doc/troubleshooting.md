## TS ругается на ошибки типов внутри пакета
1) Можно отключить проверку `skipLibCheck: true` в настройках ts.
2) Подключить типы из пакета в себе в проект недостающие типы. Либо через reference (Путь к node_modules у вас может отличаться!)
```
/// <reference path="../../node_modules/@yandex-int/messenger.utils/lib/@types/index.d.ts" />
/// <reference path="../../node_modules/@yandex-int/messenger.sdk/@types/flags.d.ts" />
/// <reference path="../../node_modules/@yandex-int/messenger.sdk/@types/apiv3.d.ts" />
/// <reference path="../../node_modules/@yandex-int/messenger.sdk/@types/fanout.d.ts" />
/// <reference path="../../node_modules/@yandex-int/messenger.sdk/@types/yamb.d.ts" />
```
либо в настройках ts.

## Появляется ошибка `Widget should be initalized *`
Метод `Widget::init` не был вызван, или вызван после обращения к API виджета или UI плагина.
Проверьте порядок инициализации, если инициализации происходит в хуке компонента убедитесь, в том что хук вызвается перед вызовом хука с вызовом `mount`/`setPopupTarget`.

## Падает SSR
Вызван метод `Widget::init`. Добавьте условие, по которому `Widget::init` будет вызваться только в браузере. Так же можно вызывать `Widget::init` в `React.useEffect`.

## Проблемы со скролом в мобильном режиме
Виджет в мобильном попап режиме автоматически отключает скролл в `body` (применяется `overflow: hidden`, а также некоторые хаки для ios). Если из-за этого возникают какие-то проблемы - вы можете реализовать свой `PageScrollController` и передать его в параметры виджета.
