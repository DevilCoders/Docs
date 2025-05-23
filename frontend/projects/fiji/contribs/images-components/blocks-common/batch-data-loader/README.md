# batch-data-loader
Блок для создания и управления предзагружаемой очередью из запросов. Для использования необходимо унаследовать свой кастомный блок "Загрузчик" от данного блока.

### Работа с блоком

В общем виде работа с блоком осуществляется следующим образом:

 1. Декларируем js реализацию своего "Блока-загрузчика" `BEM.decl({ block: 'some-block', baseBlock: 'batch-data-loader' }, {});`;
 2. Определяем функцию `_getRequest`, которая возвращает `Promise` созданного AJAX запроса за данными;
 3. Определяем функцию `_convert`, которая обрабатывает ответ запроса в нужном для "Блока-загрузчика" формате (если необходимо);
 4. С помощью `BEM.create('some-block', params)` создаем инстанс "Блока-загрузчика";
 5. Используем полученный инстанс многократно, работая с базовыми методами API.

### Пример

```javascript
// Декларируем "Блок-загрузчик" и определяем базовые методы _getRequest, _convert
BEM.decl({ block: 'data-loader', baseBlock: 'batch-data-loader' }, {
    _getRequest: function(params) {
        return $.ajax({
            url: 'https://' + params.host,
            data: {
                someParam: params.someParam
            },
            type: 'GET',
            timeout: 30000
        });
    },

    _convert: function(data) {
        if (!data) {
            return null;
        }

        var ads = data.premium.ads[0];

        return {
            source: 'direct',
            url: ads.url,
            title: ads.title,
            text: ads.body,
            domain: ads.domain,
            link_head: data.common.linkHead,
            link_tail: ads.linkTail
        };
    }
});

// Создаем инстанс "Блока-загрузчика"
var dataLoader = BEM.create({ block: 'data-loader' });

// Подписываемся на событие загрузки данных
dataLoader.on('loaded error', onLoadComplete);

// Вызываем загрузку очереди
dataLoader.batchLoad([
    { id: '1', host: 'value', someParam: 'value2' },
    { id: '2', host: 'value', someParam: 'value2' }
    { id: '3', host: 'value', someParam: 'value2' }
    { id: '4', host: 'value', someParam: 'value2' }
]);

// Обработчик полученного ответа
function onLoadComplete(e, data) {
    // Для действий с ответом нужно проверить, что текущий ответ принадлежит именно нужному элементу
    if (data.id !== needId) {
        return;
    }

    // Дальнейшая работа с полученными данными
    ...
}
```

#### Методы
##### clear()
**Очистка истории загруженных данных**: удаляет весь кэш загруженных данных. Не прерывает незаконченные запросы!

##### batchLoad(data[])
**Загрузка очереди запросов**: загружает пачку блоков в порядке очереди. Валидирует еще незаконченные соединения - если в новой очереди запрос не встречается - прерывает его.

`data[] {Array}` – Массив объектов с необходимыми данными запроса. Обязательное поля для каждого `id` для идентификации запросов.

##### load(params)
**Предобработка запроса в зависимости от его статуса**: вызывает методы обработки различных статусов запросов. Новый запрос - загружает.

`data {Object}` – Объект с необходимыми данными запроса. Обязательное поле `id` для идентификации запроса.

##### abort(state)
**Остановка запроса**: прерывает запрос по данным его состояния.

`state {Object}` – Статус загруженных данных блока. Обязательное поле `id` для идентификации запроса и `status` - loading|loaded|error|canceled.

##### getLoaded(id)
**Получение состояния загруженного нужного запроса**: возвращает статус запроса блока для указанного ID, если он есть

`id {String}` – Уникальный идентификатор запроса.
