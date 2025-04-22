# Baobab Viewer
## Описание

## Документация
### Bundle с кнопкой
#### React
Импорт компонента:
```ts
import { BaobabInjectorButton } from '@yandex-int/react-baobab-logger';
```
Встраивание:
```jsx
<BaobabInjectorButton
    version="0.2.14" // версия
    service="ugc" // название сервиса
    positionX="left" // положение по горизонтали: 'left' (по умолчанию) или 'right'
    positionY={0} // положение по вертикали в px от низа видимой части страницы (position: fixed; bottom: Npx) (по умолчанию 0)
    />
```
Название сервиса нужно для будущего определения форматтера, который выводит информативные лейблы для каждой из нод (см. [пример SERP](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/baobab-viewer/src/Formatter/SERPBaobabFormatter.tsx)).

При этом нужно передать логгер в `BaobabRoot`:
```ts
import React from 'react';
import {
    ILoggerProps,
    INodeContext,
    ISenderProps,
    Logger,
    Sender,
    withBaobabRoot,
    BaobabInjectorButton,
} from '@yandex-int/react-baobab-logger';

export const BaobabRoot = withBaobabRoot<{}, INodeContext, ILoggerProps<ISenderProps>>(
    { name: '$page', attrs: { ui: 'desktop', service: 'ugc' } },
    Logger,
    Sender,
    BaobabInjectorButton.useLogger, // передача логгера при инициализации
)(({ children }) => <>{children}</>);
```
#### JS
Вставить скрипт любым способом со следующим URL:
```
https://frontend-internal.s3.mds.yandex.net/baobab-viewer/{VERSION}/button.js
```
где вместо `{VERSION}` - конкретная версия.
и указать в теге `<script>` с `id="BaobabViewerInject"` и data-атрибутами `version`, `service`, `positionX`, `positionY`. Описание каждого атрибута выше.
Например:
```html
<script src="https://frontend-internal.s3.mds.yandex.net/baobab-viewer/0.2.14/button.js" id="BaobabViewerInject" data-service="ugc" data-version="0.2.14" data-position-x="left" data-position-y="41"></script>
```
До того, как загрузился бандл со скриптом, необходимо положить в `window.__baobabLogger` инстанс Logger'а, который будет сообщать о событиях Баобаба.

### Ручная работа с viewer'ом
#### Открытие viewer'а
Достаточно вызвать `window.open` с URL по шаблону `https://frontend-internal.s3.mds.yandex.net/baobab-viewer/{VERSION}/index.html`, где вместо `{VERSION}` - конкретная версия.
```js
var viewer = window.open(url);
```
Поскольку страница в окне не сразу загрузится, мы не занем когда педеавать данные, мы ждем пока не прилетит "сигнал" на готовность.
Для этого ставится обработчик событий postMessage'а:
```js
window.addEventListener('message', function(event) {
    // В event.data находится объект
    var json = event.data;

    // Формат объекта: { action: string, version: string, origin: string }
    // В зависимости от action могут быть дополнительные параметры.

    // Когда viewer готов принимать данные он отправляет postMessage с action=ready
    if (json.action === 'ready') {
        // Отправка данных происходит так же, через postMessage в таком же формате (action: string + доп. параметры)
        viewer.postMessage({ action: 'push_trees', trees: trees }, '*');
    }
});
```

## Поддерживаемые события
Для версии 0.2.7 и выше.
### От viewer'а
* `ready` (`{ version: string, origin: string }`) - viewer готов принимать данные.
### Для viewer'а
* `push_trees` (`{ trees: BaobabTreeItem[], service: string }`) - отправка всех деревьев (обычно используется для выгрузки всех событий, которые произошли перед открытием viewer'а);
* `push_tree` (`{ tree: BaobabTreeItem }`) - отправка одного дерева;
* `add_event` (`{ event: BaobabTreeEvent }`) - отправка пользовательского события;
* `show_node` (`{ id: string }`) - пронавигироваться на ноду с идентификатором id: найти, раскрыть все родительские и подсветить.
### Поддерживаемые service
* `serp`
* `ugc`

## Обновление viewer'а
[Как определять новую версию](https://github.yandex-team.ru/search-interfaces/frontend/blob/master/projects/lego/guidelines/contribs.md#соотношение-type-и-semver-версии-которая-будет-выпущена-в-npm)

0. Создать пулл реквест;
0. Создать dev бету, введя команду `/canary all`. Версия создается одна на PR и c его изменением затирается;
0. В описании PR появятся ссылки на опубликованные dev пакеты;
0. Когда все будет готово, смержить пулл реквест;
0. Выпустится новая продакшен версия с ожидаемой версией;
