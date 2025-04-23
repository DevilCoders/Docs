# Логирование ошибок

## Клиентские ошибки
Для сервисов Картинки и Видео используется библиотека для логирования ошибок [error-counter](https://github.yandex-team.ru/RUM/error-counter)

По умолчанию логируются необработанные ошибки, которые достигли обработчика `window.onerror`.
Для логирования обработанных клиентских ошибок предусмотрен метод ``window.Ya.Rum.logError``.

Пример использования:

```js
try {
 ...
} catch(e) {
    window.Ya.Rum.logError({
        block: 'location',
        source: 'pushStateError'
    }, e);

}
```

Во внутренней сети отправленные клиентские ошибки в том числе отображаются в консоли браузера.


## Серверные ошибки
Для логирования серверных ошибок Report Renderer экспортирует объект `Util` с методом `reportError`.

Реализован метод с обвязкой `reportMessage` в файле [handled-error.common.js](https://a.yandex-team.ru/arc_vcs/frontend/projects/fiji/sakhalin/blocks-common/handled-error/handled-error.common.js).

Чтобы отправить серверную ошибку необходимо:
1. Импортировать функцию `reportMessage`
    ```
    const { reportMessage } = require('sakhalin/blocks-common/handled-error/handled-error.common');
    ```
2. Вызвать с параметрами сообщения и объектом дополнительных опций. Пример:
    ```
    reportMessage('Page not found', {
        page: data.page,
    });
    ```

## Как смотреть ошибки
Все ошибки попадают в ErrorBooster [Картинок](https://error.yandex-team.ru/projects/images) и [Видео](https://error.yandex-team.ru/projects/video).

Фильтровать можно по любым полям отправляемых в ошибке. Некоторые примеры описаны ниже.
Также можно составлять комплексные фильтры через использование логических операторов.

1. Фильтация по типу окружения:
   * `runtime === browserjs` - клиентские
   * `runtime === nodejs` - серверные
2. Фильтрация по платформе:
   * `platform === desktop`
3. Фильтрация по типу ошибки:
   * `source === uncaught` - необработанные
   * `source === client` - обработанные

