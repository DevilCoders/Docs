# Архитектура
API состоит из двух компонентов:
* Бэкенд - объект, предоставляемый приложением, и содержащий методы в удобном для реализации в приложении виде
* Фронтенд - обертка над бэкендом, обеспечивающая удобство работы в коде СЕРПа.
  
Важное отличие от API в web4 - фронтенд реализован в синхронном стиле.
Бэкенд гарантированно подгружается на момент инициализации, поэтому необходимость в асинхронных вызовах отпала,
к тому же это позволило сделать код более компактным.

**web4:**
```javascript
Ya.AppsApi.whenAvailable('query', function(query) {
     query.setText('alarm!')
}, this)
```
**Бабуля:**
```javascript
if (Ya.AppsApi && Ya.AppsApi.query) {
    Ya.AppsApi.query.setText('alarm!');
}
```
  
# Бэкенд
Бэкенд доступен в виде объекта `window.YandexApplicationsAPIBackend`.
В Бабуле используются следующие методы:

Название | Поддерживается с версии
-------- | -----------------------
`setQueryText(text)` | 4.50
`openVertService(service, url)` |  4.50 
`isPageVisible()` | 5.30
`openRelatedQuery(requestDataJson)` | 5.50

# Фронтенд
Фронтенд доступен в виде объекта `Ya.AppsApi`.
Методы разделены по фичам аналогично с web4, но доступны напрямую в объекте,
в отличие от web4, где используется метод `.whenAvailable()`.

Необходимо учитывать:
* в ранних версиях приложения некоторые фичи могут быть недоступны;
* приложение может работать на Android 4.4, в котором используется старое WebView, не поддерживающее методы ES6.

Для того, чтобы поддержать новую фичу, доступную в бэкенде, нужно добавить свойство в объект [_features](https://github.yandex-team.ru/serp/granny/blob/8af67374b834d0ac9ae015fc3212f32b4c25eb17/blocks/yandex-apps-api/yandex-apps-api.js#L5-L24).

Определение:
```javascript
_features: {
    ...
    feature: {
        featureMethod: 'backendMethod'
    }
    ...
}
```

Вызов:
```javascript
    // Фича будет добавлена, если все её методы поддерживаются в приложении
    if (Ya.AppsApi && Ya.AppsApi.feature) {
        Ya.AppsApi.feature.featureMethod()
    }
```

## События
API поддерживает ряд общих событий, доступных через бэкенд.
Чтобы поддержать новое событие, доступное в бэкенде, нужно добавить свойство в объект [_events](https://github.yandex-team.ru/serp/granny/blob/8af67374b834d0ac9ae015fc3212f32b4c25eb17/blocks/yandex-apps-api/yandex-apps-api.js#L26-L30).

Определение:
```js
_events: {
    ...
    feature: {
        featureEvent: 'backendEvent'
    }
    ...
}
```

Вызовы:
```js
if (Ya.AppsApi && Ya.AppsApi.feature) {
    // Подписка на событие
    Ya.AppsApi.feature.on('featureEvent', function() {
        console.log('alarm!');
    });

    // Отписка от события
    Ya.AppsApi.feature.un('featureEvent');
}
```

## Изменение запроса на странице

API используется для возможности менять текст запроса в омнибоксе Приложения.

`Ya.AppsApi.query.setText(text)` → `YandexApplicationsAPIBackend.setQueryText(text)`

* `{String} text` — текст запроса 

### Пример
```js
if (Ya.AppsApi && Ya.AppsApi.query) {
    Ya.AppsApi.query.setText('alarm!');
}
```

## Открытие вертикальных сервисов

API используется для поддержки переключения сервисов по инициативе верстки.

`Ya.AppsApi.verticalServices.open(service, url, newtab)` → `YandexApplicationsAPIBackend.openVertService(service, url, newtab)`

* `{String} service` — идентификатор сервиса из [словаря](https://github.yandex-team.ru/lego/islands-romochka/blob/262a1910726b784320e94d6fdf6be3d6c6cece31/common.blocks/i-services/i-services.i18n/ru.js)
* `{String} url` — url открываемой страницы
* `{Boolean} [newTab]` — открыть страницу в новой вкладке браузера (используется только в iOS, по умолчанию false)

### Пример
```js
if (Ya.AppsApi && Ya.AppsApi.verticalServices) {
    verticalServices.open('images', data.url, data.newTab);
}
```

### Использование
Чтобы указать вертикаль для перехода по ссылке, нужно добавить в контекст конструктора поле `appsApi`:

```javascript
{
    ...
    appsApi: blocks['yandex-apps-api__vertical-service'](data, 'images')
    ...
}
```

## Открытие связанного запроса

Используется для перехода по ссылкам на связанные запросы (с обновлением запроса на всех вертикалях).

`Ya.AppsApi.openRelatedQuery(json)` → `YandexApplicationsAPIBackend.openRelatedQuery(json)`

* `{String} json` — JSON-объект в виде строки, состоит из двух полей, `query` (обязательное, текст нового запроса)
и `url` (опциональное, содержит фрагмент url'а, из которого мы достаем параметры и добавляем их в url нашего серверного
запроса, если их там уже не было).

### Пример
```javascript
if (Ya.AppsApi && Ya.AppsApi.openRelatedQuery) {
    Ya.AppsApi.openRelatedQuery(JSON.stringify({ query: linkText, url: current.search }))
}
```
