Unit tests
==========
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
Unit тесты

- [Соглашения](#соглашения)
- [External libraries](#external-libraries)
- [How to run](#how-to-run)
- [What are unit tests?](#what-are-unit-tests)
- [Useful helpers](#useful-helpers)
- [Unit tests for resources](#unit-tests-for-resources)
  - [Useful helpers](#useful-helpers-1)
  - [Validation tests](#validation-tests)
  - [Request params tests](#request-params-tests)
  - [Response processing tests](#response-processing-tests)
- [Unit tests for widgets and modules](#unit-tests-for-widgets-and-modules)
  - [Useful helpers](#useful-helpers-2)
- [Unit tests for pages](#unit-tests-for-pages)
  - [Useful helpers](#useful-helpers-3)
- [Data for tests](#data-for-tests)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Соглашения
Эта директория предназначена только для следующих вещей:
1. Хелперы, вспомогательные функции для юнит-тестирования, которые используются во многих юнит-тестах.
2. Моки, набор данных, которые используются в нескольких юнит-тестах.
3. Для юнит-тестов на `app/node_modules`, больше мы не создаем там файлы, поэтому ряд тестов живут здесь, новые не создаем.

## External libraries
 * [Jest](https://jestjs.io/docs/en/26.5/getting-started.html) — основной тест-фреймворк для написания и запуска тестов;
 * [Supertest](https://github.com/visionmedia/supertest) — библиотека для осуществления http-запросов и проверки ответов.

## How to run

```bash
make test
```

При запуске тестов выполняется setup-скрипт `helpers/setup`, в котором в том числе глушится вывод в консоль
при использовании компонентов логгирования `stout` и `Terror`.
В целях отладки заглушки можно убирать.

## What are unit tests?

Unit-тесты осуществляют проверку отдельной части кода (модуля, класса, метода). При этом должна быть обеспечена изоляция внешних зависимостей.
> Цель модульного тестирования — изолировать отдельные части программы и показать, что по отдельности эти части работоспособны.

## Useful helpers
 * `difference(<Object> object1, <Object> object2)` — осуществляет рекурсивное сранение объектов, возвращает отличающиеся свойства.
```javascript
    var difference = require('@self/platform/spec/unit/helpers/difference');
    console.log(
        difference(
            {a: {b: 'c'}},
            {a: {b: 'c'}}
        )
    ); // выведет false

    console.log(
        difference(
            {a: {b: 'c'}, e: 1},
            {a: {b: 'D'}, e: 1}
        )
    ); // выведет { a: { b: 'D' } }
```
 * `promisesCustomMatchers` — кастомные матчеры для `jest` для асинхронной проверки промисов. Для использования требуется добавление их перед тест-кейсом:
```javascript
    expect.extend(require('promisesCustomMatchers'));
```
   * `toBeRejectedWith(<Error|{code: <String>, message: <String>}> reason, <Function> done)`
```javascript
    var Response = require('Response');
    var promisesCustomMatchers = require('promisesCustomMatchers');
    var r;

    beforeEach(function () {
        expect.extend(promisesCustomMatchers);
        r = new Response();
    });

    it('Должен произойти reject промиса ', function (done) {
        setTimeout(r.reject.bind(r), 1);
        expect(r).toBeRejectedWith(undefined, done);
    });

    it('Должен произойти reject промиса с ошибкой "err"', function (done) {
        setTimeout(function () {
            r.reject(new Error('err'));
        }, 1);
        expect(r).toBeRejectedWith(new Error('err'), done);
    });

    describe('Работаем с ошибками Terror', function () {
        var Terror = require('terror');
        var MyError = Terror.create('MyError', {
            STRANGE_THING_HAPPENS: 'Something strange happens'
        });

        it('Должен произойти reject промиса с ошибкой с кодом STRANGE_THING_HAPPENS', function (done) {
            setTimeout(function () {
                r.reject(new MyError(MyError.CODES.STRANGE_THING_HAPPENS));
            }, 1);
            expect(r).toBeRejectedWith({code: 'STRANGE_THING_HAPPENS'}, done);
        });

        it('Должен произойти reject промиса с ошибкой с message, содержащим "strange"', function (done) {
            setTimeout(function () {
                r.reject(new MyError(MyError.CODES.STRANGE_THING_HAPPENS));
            }, 1);
            expect(r).toBeRejectedWith({message: 'strange'}, done);
        });

    });
```
   * `toBeRejected(<Function> done)`
   * `toBeResolvedWith(<*> result, <Function> done)`
```javascript
    var Response = require('Response');
    var promisesCustomMatchers = require('promisesCustomMatchers');
    var r;

    beforeEach(function () {
        expect.extend(promisesCustomMatchers);
        r = new Response();
    });

    it('Должен произойти resolve промиса ', function (done) {
        setTimeout(r.resolve.bind(r), 1);
        expect(r).toBeResolvedWith(undefined, done);
    });

    it('Должен произойти resolve промиса со строкой "abc"', function (done) {
        setTimeout(function () {
            r.resolve('abc');
        }, 1);
        expect(r).toBeResolvedWith('abc', done);
    });

    it('Должен произойти resolve промиса с объектом, содержащим свойство "a", равное единице', function (done) {
        setTimeout(function () {
            r.resolve({a: 1, b: 2});
        }, 1);
        expect(r).toBeResolvedWith(jasmine.objectContaining({a: 1}), done);
    });
```
   * `toBeResolved(<Function> done)`.

## Unit tests for resources

Модули, с помощью которых происходит общение с внешними сервисами, реализованы на основе библиотеки [Resource](https://github.yandex-team.ru/nodules/resource).
С помощью unit-тестов можно проверить работоспособность отдельных этапов работы этих модулей:

 * валидация параметров;
 * формирование http-запроса;
 * обработка полученного ответа.

Изоляция от внешних ресурсов может быть осуществлена с помощью установки заглушки на метод `makeRequest`,
 который в оригинальном исполнении осуществляет http-запрос и возвращает его результат, сконвертированный в `dataType` ресурса.

**Важно**: при инстанциировании ресурса первым аргументом в конструктор передаётся его конфиг.
Указанный в самом ресурсе конфиг `cfg` при работе с модулем ресурса напрямую не учитывается.
```javascript
    var MyResource = resourceTestHelpers.getResourceModule('myResource');
    var resourceInstance = new MyResource({
        path: '/path/prefix'
    });
```

Тесты находятся в директории `app/resource`, для каждого метода ресурса пишется отдельный `spec`-файл.

### Useful helpers

> Здесь и далее под `meta` в контексте ресурса понимается объект, содержащий мета-информацию запроса, а именно `responseMeta` от `asker`, расширенный объектами `{code}` (код ответа) и `{headers}` (заголовки):
> * `{Object} meta` meta information
    * `{Object} time` request timers
        * `{Number} network` the time from socket was opened and until the request was completed
        * `{Number} total` total execution time
    * `{Object} options` options which was provided for request creation
    * `{Object} retries`
        * `{Number} used` number of retries used
        * `{Number} limit` retries limit for a given request
    * `{Number} code` HTTP STATUS CODE
    * `{Object} header` HTTP HEADERS

 * `resourceTestHelpers`:
   * `getResourceModule(<String> resource)` — загружает ресурс из директории с ресурсами;
   * `createOriginalErrorExtractor(<Response> resourceCallResult)` — возвращает новый `Response`, который извлечет код оригинальной ошибки из результата вызова ресурса
```javascript
    var resourceCallResult = resourceInstance.methodUnderTest({b: 1}); // ресурс генерит ошибку валидации
    var originalErrorExtractor = resourceTestHelpers.createOriginalErrorExtractor(resourceCallResult);

    it('Код ошибки вызова ресурса должен быть RESOURCE_ERROR', function (done) {
        expect(resourceCallResult).toBeRejectedWith({code: 'RESOURCE_ERROR'}, done);
    });

    it('Оригинальная ошибка вызова ресурса должна быть ValidationError', function (done) {
        expect(originalErrorExtractor).toBeRejectedWith({class: ValidationError}, done);
    });
```
  * `getDeferredRequestParams(<Object> resourceInstance[, <*> returnValue, <Object|{requestOptions: <Object>, meta: <Object>}>])` — ставит заглушку на метод `makeRequest` ресурса и возвращает объект, в который отложенно будут присвоены параметры вызова этого метода с теми мета-данными, которые были переданы
```javascript
    it('Параметр uid должен конвертироваться в строку и передаваться в query-параметре', function (done) {
        var requestParams = resourceTestHelpers.getDeferredRequestParams(resourceInstance);
        resourceInstance
            .methodUnderTest({uid: 123})
            .then(function () {
                expect(requestParams.query.uid).toBe('123');
                done();
            }, done);
    });

    // или, например, так, если ресурс ожидает определенный код ответа:

    it('Если redirectPath не содержит "/" в начале, то должен добавлять его', function (done) {
        var params = _.merge({}, validParams, {redirectPath: 'some_path'});

        var requestParams = resourceTestHelpers.getDeferredRequestParams(resourceInstance, undefined, {
            meta: {code: 302}
        });

        resourceInstance
          .get(params)
          .then(function () {
              expect(requestParams.path).toBe('/some_path');

              done();
          }, done);
    });
```
  * `injectMakeRequestResult(<Object> resourceInstance[, <*> returnValue, <Object> meta])` - подменяет результат выполнения MakeRequest на переданный
```javascript
  it('должен резолвиться с {id: 666}', function (done) {
    resourceTestHelpers.injectMakeRequestResult(resourceInstance, {result: {
        id: 666
    }});

    var result = resourceInstance.methodName(params);
    expect.result.toBeResolvedWith({id: 666}, done);
  });

  // Или так

  it('должен резолвиться с id, но не notId', function (done) {
    resourceTestHelpers.injectMakeRequestResult(resourceInstance, {result: {
        id: 666,
        notId: 777
    }});

    resourceInstance
      .methodName(params)
      .then(function (result) {
        expect.result.id.toEqual(666);
        expect.result.notId.toEqual(undefined);

        done();
      }, done);

  });
```
  * `stubMakeRequest(<Object> resourceInstance[, <*> returnValue, <Object> meta])` - подменяет выполнение MakeRequest
```javascript
  beforeEach(function (done) {
      resourceTestHelpers.stubMakeRequest(resourceInstance, done);

      resourceInstance.getBanners(validParams);
  });
```

### Validation tests

**Что проверяют**: ресурс должен осуществлять проверку переданных параметров и в случае ошибки осуществлять reject с правильным кодом и сообщением.

Поскольку

**Алгоритм**:

 * Осуществить вызов ресурса с невалидным / отсутствующим параметром;
 * Проверить, что результат вызова ресурса содержит ошибку с ожидаемым кодом и сообщением.

**Пример**:
```javascript
    it('Должна происходить ошибка валидации, если не передан параметр ABC', function (done) {
        var resourceCall = resourceInstance.methodUnderTest({b: 1});
        var originalErrorExtractor = resourceTestHelpers.createOriginalErrorExtractor(resourceCall);

        expect(originalErrorExtractor).toBeRejectedWith({class: ValidationError, message: 'ABC'}, done);
    });
```

### Request params tests

**Что проверяют**: при передаче валидных параметров ресурс должен осуществлять запрос к бэкенду с корректно сформированным параметрами (заголовки, тело, query-параметры).

**Алгоритм**:

 * С помощью `resourceTestHelpers.getDeferredRequestParams` получить объект, в который будут присвоены параметры вызова метода `makeRequest`;
 * Осуществить вызов ресурса с валидными параметрами;
 * Осуществить проверку параметров, с которыми был вызван `makeRequest`.

**Пример**:
```javascript
    it('Параметр A должен передаваться в теле запроса, умноженный на 2', function (done) {
        var requestParams = resourceTestHelpers.getDeferredRequestParams(resourceInstance);

        resourceInstance
            .methodUnderTest({A: 2})
            .then(function () {
                expect(requestParams.body.A).toBe(4);
                done();
            }, done);
    });
```

### Response processing tests

**Что проверяют**: корректность обработки ответа бэкенда (преобразование, выборка, валидация).

**Алгоритм**:

 * Установить stub на метод `makeRequest` который будет эмулировать ответ внешенго сервиса;
 * Осуществить вызов ресурса с валидными параметрами;
 * Проверить что результат вызова ресурса соответствует полученным данным.

**Пример**:
```javascript
    it('должен резолвиться с {id: 666}', function (done) {
      resourceTestHelpers.injectMakeRequestResult(resourceInstance, {result: {
          id: 666
      }});

      var result = resourceInstance.methodName(params);
      expect.result.toBeResolvedWith({id: 666}, done);
    });

    // Или так

    it('должен резолвиться с id, но не notId', function (done) {
      resourceTestHelpers.injectMakeRequestResult(resourceInstance, {result: {
          id: 666,
          notId: 777
      }});

      resourceInstance
        .methodName(params)
        .then(function (result) {
          expect.result.id.toEqual(666);
          expect.result.notId.toEqual(undefined);

          done();
        }, done);

    });
```

## Unit tests for widgets and modules

Для написания unit-тестов на виджеты и модули необходимо обеспечить изоляцию:

 * от других виджетов (для виджетов);
 * от ресурсов.

Основной способ запуска тестов на виджеты: хэлпер `setupWidget` из `stoutTestHelpers`.
Возвращает инстанс виждета созданный через `Widget.make`, с которым можно работать как с респонсом.
Для простых случаев проверки результата можно использовать проверку toHaveResult

Стандартные примеры:
```javascript
var Weedget = require(process.cwd() + '/app/widgets/data/Weedget');

it('fifteen bucks, litle man, push dat shit in my hand', function (done) {
  stoutTestHelpers
    .setupWidget(Weedget, {money: 15})
    .then(function () {
      var results = this.getResults();
      expect(results.result).toEqual('some_dope_weed');
      done();
    }, done);
  });
};

// или с проверкой результата целиком
it('fifteen bucks, litle man, push dat shit in my hand', function (done) {
  var widget = stoutTestHelpers.setupWidget(Weedget, {money: 15});

  expect(widget).toHaveResult({result: 'some_dope_weed'}, done);
};

it('if the money doesn\'t show, then you owe me, owe me, owe', function (done) {
  expect(stoutTestHelpers.setupWidget(Weedget, {money: 0}))
    .toBeRejectedWith({class: ValidationError}, done);
  });
};

```

### Useful helpers

 * `stoutTestHelpers`:
   * `stubLogger([<Function> stubObject])` — установить stub на метод логирования в `stout`;
   * `setOriginalLogger` — вернуть оригинальный метод логирования в `stout`;
   * `stubGetWidget([<String> widgetName[, <Widget>stubObject]])` — установить заглушку на метод `stout.getWidget`:
```javascript
    // stout.getWidget всегда будет возвращать базовый объект Widget
    stoutTestHelpers.stubGetWidget();

    // stout.getWidget('MyWidget') будет возвращать базовый объект Widget
    stoutTestHelpers.stubGetWidget('MyWidget');

    // stout.getWidget('MyWidget') будет возвращать объект MockWidget
    stoutTestHelpers.stubGetWidget('MyWidget', new MockWidget());
```
   * `clearWidgetsStubs` — сбрасывает сконфигурированные с помощью `stubGetWidget` заглушки
   * `setOriginalGetWidget` — вернуть оригинальный метод`stout.getWidget`;
   * `setupWidget(<Widget> Widget[, <*>widgetParams[, {Request} request])` — создаёт инстанс виджета с указанными параметрами.
     Если не передан параметр `request`, то в качестве `this.request` виджет получит объект с заглущками на все методы (`getParam`, `getHeader` и т.д.);
   * `stubResource([<ResourceStubParams> stubParams])` — установить заглушку на метод `resource`:
```javascript
    // стаб всех вызовов ресурса
    stoutTestHelpers.stubResource();

    // стаб вызова конкретного ресурса зарезолвленым ответом
    stoutTestHelpers.stubResource({resourceId: 'myResource.method', resolve: {my: 'response'}});

    // стаб вызова конкретного ресурса с ответом в зависимости от параметров вызова
    var spy = stoutTestHelpers.stubResource([
        {resourceId: 'myResource.method', resolve: {my: 'response'}},
        {resourceId: 'myResource.method', params: {unknown: '1'}, reject: 'Unknown parameter'}
    ]);
    expect(spy).toHaveBeenCalled();
```
   * `setOriginalResource()` — вернуть оригинальный метод `resource`;
   * `stubWidget(<Widget> Widget[, <WidgetStubParams> stubParams])` — установить заглушку на метод `resource` прототипа переданного виджета / страницы:
```javascript
    // стаб всех вызовов `this.widget`
    stoutTestHelpers.stubWidget(SomeWidget);

    // стаб вызова конкретного виджета с указанием результатов его работы
    stoutTestHelpers.stubWidget(SomeWidget, {widget: 'MyWidget', result: {my: 'result'}});

    // стаб вызова конкретного виджета с результатом, зависящим от параметров вызова
    stoutTestHelpers.stubWidget(SomeWidget, [
        {widget: 'MyWidget', result: {my: 'response'}},
        {widget: 'MyWidget', params: {unknown: '1'}, reject: 'Unknown parameter'}
    ]);
```
   * `setOriginalWidget(<Widget> Widget)` — вернуть оригинальный метод `widget` в прототип;
   * `stubModule(<Widget> Widget[, <ModuleStubParams> stubParams])` — установить заглушку на метод `module` прототипа переданного виджета / страницы / модуля:
```javascript
    // стаб всех вызовов `this.module`
    stoutTestHelpers.stubModule(SomeWidget);

    // стаб вызова конкретного виджета с указанием результатов его работы
    stoutTestHelpers.stubModule(SomeWidget, {module: 'MyModule', result: {my: 'result'}});

    // стаб вызова конкретного виджета с результатом, зависящим от параметров вызова
    stoutTestHelpers.stubModule(SomeWidget, [
        {module: 'MyModule', result: {my: 'response'}},
        {module: 'MyModule', params: {unknown: '1'}, reject: 'Unknown parameter'}
    ]);
```
   * `setOriginalModule(<Widget> Widget)` — вернуть оригинальный метод `module` в прототип;

## Unit tests for pages

Контроллеры страниц, в которых происходит обработка запроса.
Данными тестами проверяем логику, специфичную для конкретных страниц.
Из-за огромного количества логики в базовых классах, наследуемся от фейков:
```js

    beforeAll(() => {
        HtmlPageFake = require('@self/platform/spec/unit/mocks/stubs/pages/abstract/HtmlPage');
        stoutTestHelpers.stubPage('HtmlPage', HtmlPageFake);
    });
```

Также, следует подменить на заглушки все модули и виджеты.
Притом, логика в контроллерах часто нуждается лишь в некоторых из них,
так что для большинства сработает подмена пустой заглушкой:

```js
    stoutTestHelpers.stubWidget(HtmlSearch);
    stoutTestHelpers.stubModule(HtmlSearch);
```

Пример теста:
```js
    it('Не должен редиректить', (done) => {
        stoutTestHelpers.setupPage(HtmlSearch).then(function () {
            expect(this.redirect).not.toHaveBeenCalled();

            done();
        }, done);
    });

```

### Useful helpers

   * `stubPage(<string> name, <Page> Page)` - переопределяет страницу с определённым именем.
   Готовые стабы можно найти по пути `spec/node_modules/stubs/pages/`
```js
    stoutTestHelpers.stubPage('HtmlPage', HtmlPageFake);
```
   * `setupPage(<Page> Page, <Object> params)` - инстанцирует страницу с переданными параметрами
   в params можно передать кастомные request, response и route
```js
    HtmlSearch = require(process.cwd() + '/app/pages/html/HtmlSearch');

    it('Не должен редиректить, в случае совпадения nid', (done) => {
        let fakeRequest = stoutTestHelpers.createRequestFake({
            params: {nid: 123}
        });

        stoutTestHelpers.setupPage(HtmlSearch, {
            request: fakeRequest,
            route: stoutTestHelpers.createRouteStub()
        }).then(function () {
            expect(this.redirect).not.toHaveBeenCalled();
            done();
        }, done);
    });
```
   * `createRouteStub([<object> config])` - возвращает стаб роута.
   В качестве конфига нужно передавать объект той же структуры, что используется в конфигах приложения, он же RouteOptions для susanin.
   Если конфиг не передан то используется конфиг по умолчанию из `createDefaultRouteConfig`
```js
    stoutTestHelpers.setupPage(HtmlSearch, {
        request: fakeRequest,
        route: stoutTestHelpers.createRouteStub({
            name: 'market:list',
            data: {
                pageData: {
                    method: 'addItems'
                }
            }
        })
    })
```
   * `createDefaultRouteConfig()` - возвращает дефолтный конфиг роута.
```js
    let routeConfig = stoutTestHelpers.createRouteStub();
    routeConfig.name = 'market:list';

    stoutTestHelpers.setupPage(HtmlSearch, {
        request: fakeRequest,
        route: stoutTestHelpers.createRouteStub(routeConfig)
    })
```


## Data for tests

Большие объекты с данными стоит выносить в отдельные файлы.
Чтобы они не подвергались проверке codestyle, директория с данными должна называться `testData`

## Testers

Тестеры – наборы функций-хелперов для высокоуровневого написания тестов на основные сущности, такие как виджеты или страницы.
Решают проблему постоянного копипаста императивного кода для стабов и подготовки тестируемой сущности.
Не предполагают под собой полную замену `stoutTestHelpers`, но предполагают упрощение воспроизведения большинства кейсов, которые чаще всего требуется покрыть.

В каждом типе тестера применяется свой формат инициализирующих параметров и проверяющих результаты матчеров.
В функцию-тестер параметры передаются первым аргументом. Матчеры соответственно последующими аргументами.
Последним аргументом является обратный вызов `done`.

### Resource

Параметры являются как таковыми параметрами вызова ресурса.

#### Validation

```js
const {
    validationErrorExpected,
} = require('resourceTesters')('reviews.shopReviews');

describe('бросает ошибку валидации', () => {
    it('если shopid не числовой', done => {
        validationErrorExpected({shopid: 'asd'}, 'shopid', done);
    });
});
```
#### Prepared request options

```js
const {
    preparedOptionsExpected,
} = require('resourceTesters')('reviews.shopReviews');

describe('Ресурс reviews метод shopReviews', () => {
    it('подготавливает опции, в path которых содержится shopid', done => {
        const params = {shopid: '999'};
        const matcher = jasmine.objectContaining({
            path: jasmine.stringMatching('/shop/999'),
        });
        preparedOptionsExpected(params, matcher, done);
    });
});
```

#### Processed response data

```js
const {
    TestDataFile,
    processedDataExpected,
} = require('resourceTesters')('reviews.shopReviews');
const shopReviewsResponse = require('./testData/reviews.shopReviews');

describe('Ресурс reviews метод shopReviews', () => {
    it('в ответе возвращает отзывы', done => {
        const params = {shopid: '999'};
        const path = __dirname + '/testData/reviews.shopReviews.json';
        processedDataExpected(params, new TestDataFile(path), jasmine.objectContaining({
            opinions: jasmine.arrayContaining([
                jasmine.objectContaining({
                    entity: 'opinion',
                    id: '59626004',
                }),
            ]),
        }), done);
    });
});
```

### Widget

Параметры и матчеры имеют следующую структуру:

```js
const params = {
    user: {}, // пользователь
    widgetParams: {}, // параметры, которые будут переданы в виджет
    stubs: [{ // стабы виджета, синтаксис совпадает с соответствующими функциями stoutTestHelpers
        resourceId: 'resource.method',
    }, {
        module: 'ModuleName',
    }, {
        widget: 'WidgetName',
    }],
};

const matcher = {
    resource: {
        'resource.method': {}, // ожидаемые параметры вызова ресурса
    },
    module: {
        ModuleName: {}, // ожидаемые параметры вызова модуля
    },
    widget: {
        WidgetName: {}, // ожидаемые параметры вызова виджета
    },
};
```

#### Calls widget/module/resource

Проверяет, что в процессе работы виджета были вызваны другие виджеты, модули или ресурсы с ожидаемыми параметрами.

```js
const shopTabsTesters = require('@self/platform/spec/unit/helpers/testers/widgetTesters')('shop/ShopTabs');

describe('ShopTabs', () => {
    it('обращается к ресурсу reviews.shopReviews с shopid', done => {
        const params = {
            widgetParams: {
                shopId: 999,
            },
            stubs: [{
                resourceId: 'reviews.shopReviews',
            }],
        };
        shopTabsTesters.calls(params, {
            resource: {
                'reviews.shopReviews': {
                    shopid: 999,
                }
            }
        }, done);
    });
});
```

#### Has results

Проверяет, что результат работы виджета содержит ожидаемые значения.

```js
const stoutTestHelpers = require('@self/platform/spec/unit/helpers/stoutTestHelpers');
const shopTabsTesters = require('@self/platform/spec/unit/helpers/testers/widgetTesters')('shop/ShopTabs');

describe('ShopTabs', () => {
    it('возвращает результатом структуру табов, содержащую имя и URL', done => {
        const user = stoutTestHelpers.createUserFake(false);
        const params = {
            user,
            widgetParams: {
                shopId: 999,
            },
            stubs: [{
                resourceId: 'reviews.shopReviews',
                resolve: {
                    pager: {
                        total: 777,
                    },
                },
            }],
        };
        shopTabsTesters.hasResults(params, jasmine.arrayContaining([{
            name: 'Товары',
            url: jasmine.anything(),
        }]), done);
    });
});
```

### HtmlPage

Параметры и матчеры имеют следующую структуру:

```js
const params = {
    user: {}, // пользователь
    route: {}, // параметры роута, используются при вызове stoutTestHelpers.createRouteStub
    request: {}, // параметры запроса, используются при вызове stoutTestHelpers.createRequestFake
    stubs: [{ // стабы страницы, синтаксис совпадает с соответствующими функциями stoutTestHelpers
        resourceId: 'resource.method',
    }, {
        module: 'ModuleName',
    }, {
        widget: 'WidgetName',
    }],
};

const matcher = {
    resource: {
        'resource.method': {}, // ожидаемые параметры вызова ресурса
    },
    module: {
        ModuleName: {}, // ожидаемые параметры вызова модуля
    },
    widget: {
        WidgetName: {}, // ожидаемые параметры вызова виджета
    },
};
```

#### Validation

```js
const htmlShopReviewsTesters = require('@self/platform/spec/unit/helpers/testers/pageTesters')('HtmlShopReviews');

describe('валится ошибка валидации', () => {
    it('если передан неверный параметр grade_value', done => {
        htmlShopReviewsTesters.validationErrorExpected({
            request: {params: {shopId: 999, grade_value: 'a'}},
        }, 'grade_value', done);
    });
});
```

#### Error

```js
const htmlShopReviewsTesters = require('@self/platform/spec/unit/helpers/testers/htmlPageTesters')('HtmlShopReviews');

describe('валится ошибка', () => {
    it('если что-то пошло не так', done => {
        htmlShopReviewsTesters.errorExpected({
            request: {params: {shopId: 999, grade_value: 'a'}},
        }, jasmine.anything(), done);
    });
});
```

#### Calls widget/module/resource

```js
const htmlSearchTesters = require('@self/platform/spec/unit/helpers/testers/pageTesters')('HtmlSearch');

describe('Если роут market:shop-search', () => {
    it('страница должна вызывать виджет ShopTabs с shopId из URL', done => {
        const params = {
            route: {
                name: 'market:shop-search',
            },
            request: {
                params: {shopId: 777}
            },
        };
        htmlSearchTesters.calls(params, {
            widget: {
                ShopTabs: {
                    shopId: 777,
                },
            },
        }, done);
    });
});
```

#### Redirects to

Для тестеров такого типа матчер это объект с двумя свойствами:

- Имя роута
- Параметры роута

```js
const htmlCompareTesters = require('@self/platform/spec/unit/helpers/testers/pageTesters')('HtmlCompare');

describe('редирект', () => {
    it('происходит, если URL в старом формате', done => {
        const productId1 = '987';
        const hid = '13959730';

        const params = {
            user,
            request: {
                params: {
                    CMD: `-CMP=${productId1}`,
                    hid: hid,
                },
            },
        };
        htmlCompareTesters.redirects(params, {
            name: 'market:compare',
            params: {
                hid: hid,
                id: [productId1]
            }, done);
    });
});
```
