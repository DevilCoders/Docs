##Api-страницы

Контроллеры для вызова через ajax с клиента. Возвращают json. Получение и обработка данных происходит внутри методов контроллера.

Пример:
```javascript
// Внешние зависимости.
const logger = require('@yandex-market/logger');

// Helpers
const {prepareResource, promiseAdapter} = require('@self/platform/app/helpers');

// Модули получения данных
const {getData} = require('@self/platform/modules/data-getters');

// Модули обработки данных
const {filterData} = require('@self/platform/modules/data-formatters');

const JsonApiPage = require('@self/platform/app/pages/abstract/JsonApiPage');

const ApiPage = JsonApiPage.create();

module.exports = ApiPage;

ApiPage.prototype.method = function method() {
    const resource = prepareResource(this.resource, this);

    const dataPromise = getData(resource);

    const filteredDataPromise = dataPromise.then(filterData);

    return promiseAdapter(
        Promise.props({
            data: filteredDataPromise.catch(onDataReject)
        })
    );
}

ApiPage.prototype.anotherMethod = function anotherMethod() {
    // тело метода
}

ApiPage.Error = JsonApiPage.Error.create('ApiPageError', {
    UNHANDLED_PAGE_ERROR: 'Error when trying to get page data'
});

function onDataReject(cause) {
    const error = ApiPage.Error
        .createError(ApiPage.Error.CODES.UNHANDLED_PAGE_ERROR, cause);

    logger.error(error);

    throw ApiPage.Error.CODES.UNHANDLED_PAGE_ERROR;
}
```
