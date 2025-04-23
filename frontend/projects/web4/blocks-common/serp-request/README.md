# Блок-хелпер для AJAX запросов
См. [Wiki](https://beta.wiki.yandex-team.ru/search-interfaces/ajax/)

Блок является синглтоном, его инстанс должен создаваться исключительно методом
```js
serpRequest = BEM.blocks['serp-request'].getInstance()
```

## Интерфейс
Реализует интерфейс в виде канала `BEM.channel('serp-request')`, который:

### Слушает событие request
См. документацию к методу `_onRequest`

### Инициирует событие success при успешном завершении запроса
С этим событием приходят данные, задаваемые в серверном коде блока `serp-request`

### Инициирует событие error при завершении запроса с ошибкой
С этим событием приходит объект ошибки с полями `type` и `data`, см. пример с колбэком `error`

## Префетч
Используется для предзагрузки необходимых запросов. Включается через параметр `prefetchText`, передаваемый в параметрах события
`request`. При наличии данного параметра, текст текущего запроса заменяется на значение параметра, к запросу добавляется
специальный флаг `prefetch`, а сам параметр попадает в хранилище текстов запросов, по которым в данный момент происходит префетч.
После успешного завершения запроса, текст запроса считается запрефетченным, и в случае повторного вызова запроса с таким текстом,
к запросу добавляется флаг `prefetch`, что позволяет браузеру взять данный запрос из кэша.
Используется, например, в блоке `serp` для префетча запросов из саджеста.

## Примеры использования
Событие `success`:
```js
BEM.channel('serp-request').on('success', function(e, data) {
    console.log('Some request success! We received such data:', data);
});
```

Загрузка блока через AJAX:
```js
BEM.channel('serp-request').trigger('request', {
    key: 'z-advanced-afisha',
    data: { some: 'data for the server method' },
    params: { foo: 'bar' },
    settings: {
        preSearch: true, // использовать ручку, которая не ходит в поиск
        dontUpdateGlobal: true, // не обновлять глобальные параметры, как reqid
        renderOnStaticFail: true // сохранить имя блока в параметр load-blocks на случай смены статики
    },
    success: function(blockData) {
        // ...
    },
    error: function(errorData) {
        // errorData.type - тип ошибки, типы хранятся в константах блока serp-request
        // errorData.data - данные ошибки, зависят от типа
        // ...
    }
});
```

Передача на сервер параметра `reload`:
```js
BEM.channel('serp-request').trigger(
    $.Event('request', { reloadReason: BEM.blocks['serp-request'].RELOAD_INVALID_RESULT }),
    { key: 'z-afisha' }
);
```

Так же параметр `reload` может быть передан через событие `change` блока `location`:
```js
var location = BEM.blocks['location'].getInstance();
location.trigger(
    $.Event('change', { reloadReason: BEM.blocks['serp-request'].RELOAD_TRY_AGAIN }),
    location.getState()
);
```
