# Overlay

## Концепция

Overlay - это тачевый блок для создания таких окон:
* открываются, красиво выезжая с одной из четырех сторон окна браузера
* обычно состоит из навигационной панели и собственно содержимого
* навигационная панель (шапка) состоит из кнопок и текста - заголовка; стандартные кнопки: "назад" и "закрыть"
* открываясь создает запись в истории браузера, поэтому переключаться между открытыми overlay-ями можно с помощью переходов по истории
* кнопка "назад" в навигацонной панели ведет себя как переход назад по истории браузера
* кнопка "закрыть" очищает историю браузера и закрывает все overlay-и
* обычно открывается по тапу на ссылку/кнопку

![Overlay-screen-example](https://jing.yandex-team.ru/files/vttly/overlay-screen-example.png)

## Старый способ использования

Способ подходит для случая, когда контент overlay-я загружается вместе с выдачей до реального использования. Если требуется загрузка контента по условию, она реализуется кастомно в каждом конкретном случае.

### 1. Добавить ссылкам/кнопкам функцию открытия

Пользуемся [supply__overlay](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-touch-phone/supply/__overlay/supply__overlay.priv.js):

```js

link.overlay = {
    // уникальный идентификатор (если не передан - сгенерируется автоматически)
    id: 'my-overlay',

    // блок для отрисовки содержимого
    blocks: 'my-overlay',

    // данные для отрисовки навигационной панели
    navigationBar: {
        theme: 'plain',
        actions: { left: ['back'] }
    }

    /* настройки блока */
    /* настройки overlay */
};
```

### 2. Реализовать блок

Обычно нас в большей степени интересует клиентский js блока:

```js

BEM.DOM.decl('my-overlay', {
    onAfterOverlayOpen: function() {
        // можно загрузить/дозагрузить какой-то контент ajax-ом
    }

    // см. lifecycle-методы: onOverlayOpened, onAfterOverlayOpen, onOverlayClosed, onAfterOverlayClose
});
```

## Динамическая загрузка

Когда контент overlay-я загружается динамически:
* открывается overlay со спиннером
* если контент загружается успешно - все ок
* если происходит ошибка - overlay закрывается автоматически
* для дополнительной обработки ошибки можно указать свою функцию, она будет вызвана если в момент ошибки overlay,
контент которого не удалось загрузить, открыт

### 1. Добавить ссылкам/кнопкам функцию открытия

Пользуемся [supply__overlay-ajax](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-touch-phone/supply/__overlay-ajax/supply__overlay-ajax.priv.js):

#### 1.1 Нет клиентского js у блока

В случае, если у блока (например у адаптера) нет клиентского js, можно использовать следующий код:

```js

link.overlayAjax = {
    params: {
        id: <уникальный_ID_оверлея>, // обязательный параметр
        /* парамерты для запроса контента overlay-я */
    }
};
```

#### 1.2 У блока есть клиентский js и host-блок

##### priv.js

```js

link.overlayAjax = {
    // блок, отвечающий за открытие overlay-я
    host: 'my-block',

    params: {
        /* парамерты для запроса контента overlay-я */
    }
};
```

##### client js

```js

BEM.DOM.decl('my-block', {
    onOverlayAjaxHandlerClick: function(e, params, overlay) {
        function lazyParams() {
            // дополнить params из priv-ов, если необходимо

            return {
                item: {
                    /* настройки overlay: type, closeOnExternalClick и пр. */
                },
                ajaxParams: {
                    request: {
                        /* дополнительные query-параметры запроса */
                    },
                    ajax: {
                        adapter: 'my/stuff'
                        /* параметры для адаптера - см. последний аргумент */
                    },
                    settings: {
                        /* настройки ajax-а */
                    }
                 }
            };
        }

        function onError(isFatal) {
            /**
             * дополнительно обработать ошибку:
             *   - isFatal === true, если ajax-ответ не содержит html
             *   - isFatal === false, если ajax зафейлился (пропала сеть, например)
             */
        }

        overlay.fetchAndOpenOverlay('my-overlay', lazyParams, onError);

        e.preventDefault();
    }
});
```

### 2. Реализовать адаптер

Адаптер возвращает данные для построения целого overlay: шапка + контент.

```js

blocks['adapter-my-stuff__ajax'] = function(context, data, params) {
    return {
        // данные для отрисовки навигационной панели
        navigationBar: {
            theme: 'plain',
            actions: { left: ['back'] }
        },

        content: {
            // данные блока для отрисовки контента
        }
    };
};
```
