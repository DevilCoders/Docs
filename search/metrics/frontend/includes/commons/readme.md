# Common frontend components

### Использование

```js
import init from '@metrics/commons';
// название приложения, цветовая схема, пункты меню и т.д.
import config from './config';

const App = Backbone.Router.extend({
    initialize() {
        init.call(this, config, Backbone.history);
    },
    /*
        роутинги
    */
});

window.app = new App();
```

### Локальный запуск тестовой страницы

* в /etc/hosts добавляем строчку
```
127.0.0.1       test.qe-local.yandex-team.ru
```
* `npm start` запускает сервер webpack
* открываем [страницу](https://test.qe-local.yandex-team.ru:8080) в браузере