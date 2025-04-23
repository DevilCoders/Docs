# PageActionBuild

Миксин добавляет [`action_build`](#action_build) к прототипу контроллера страницы ([`Page`](Page.md) и его наследников).

## Пример

```javascript
var controllers = require('nodules-controllers'),
    Page = controllers.Page,
    PageActionBuild = controllers.PageActionBuild,

    MyServicePage = Page.create()
        .mixin(PageActionBuild, 'b-page');
```

## API

### Динамически подмешиваются в прототип

#### action_build()

`action_build() → {Promise}`

Действите получения данных и полной отрисовки страницы.

После получения данных обрабатывает флаги `data.isRedirect` и `data.is404`:

* если установлен флаг `data.isRedirect`, то производится редирект на адрес `data.redirectTo`;
* если установлен флаг `data.is404`, то устанавливается код ответа `404`.

После проверок (если не был произведен редирект), то выполняется шаблон `b-page`.