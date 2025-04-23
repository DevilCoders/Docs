##Page
Главные контроллеры страниц. Занимаются получением всех необходимых данных и их подготовкой.

Пример описания страницы:
```javascript
// Внешние зависимости
const logger = require('@yandex-market/logger');

// Helpers
const {prepareResource, promiseAdapter} = require('@self/platform/app/helpers');

// Модули получения данных
const {getData} = require('@self/platform/modules/data-getters');

// Модули обработки данных
const {filterData} = require('@self/platform/modules/data-formatters');

function Page() {
	const resource = prepareResource(this.resource, this);

	const dataPromise = getData(resource);

	const filteredDataPromise = dataPromise.then(filterData);

	this.push(promiseAdapter(
		Promise.props({
			data: filteredDataPromise.catch(onDataReject)
		})
	), 'Page');
}

module.exports = HtmlPage.create(Page);

Page.Error = HtmlPage.Error.create('PageError', {
    UNHANDLED_PAGE_ERROR: 'Error when trying to get page data'
});

function onDataReject(cause) {
    const error = Page.Error
        .createError(Page.Error.CODES.UNHANDLED_PAGE_ERROR, cause);

    logger.error(cause);

    throw Page.Error.CODES.UNHANDLED_PAGE_ERROR;
}
```
