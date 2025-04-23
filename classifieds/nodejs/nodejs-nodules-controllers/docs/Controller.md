# Controller

Базовый класс контроллера.

Родитель: [Objex](https://github.com/nodules/objex)

## API

### Статические свойства

#### ControllerError

Класс ошибок. Наследник [AbstractControllerError](/docs/AbstractControllerError.md).

Коды ошибок:

 * `ERROR_IN_CONSTRUCTOR_FACTORY` – ошибка при попытке подключения файла контроллера или при создании экземпляра;
 * `UNDEFINED_ACTION` – вызван метод [`Controller#callAction()`](#callaction) для несуществующего действия.

#### new Controller()

`new Controller(data) → {Controller}`

* `{Object} data` — см. [Controller.factory](#factory), за исключением `directory` и `type`,
    так как тип контролера уже известен, раз мы вызываем непосредственно его конструктор.

Вызвать конструктор контроллера напрямую может потребоваться в другом контроллере,
чтобы использовать его функциональность, если наследование по каким-либо причинам неприменимо.

#### create()

`create(type, constructor) → Controller`

* `{String} [type]`
* `{Function} [constructor]`

Метод порождает конструктор наследника контроллера от которого был вызван. Статические свойства и методы *копируются*.

Если в качестве аргумента передается функция–конструктор, то она должна вызывать суперконструктор:

```javascript
var MyPageController = Controller.create('MyPageController', function() {
    MyPageController._super.apply(this, arguments);
});
```

Тип, как и конструктор, необязателен. Доспустимые вызовы:

```javascript
Controller.create('MyController');
Controller.create();
Controller.create(function() { ... });
```

#### setPath()

`setPath(path) → this`

* `{String} path` — путь к каталогу с контроллерами.

Метод устанавливает классу и его наследникам путь к каталогу с реализациям контроллеров.

Возвращает `this`.

#### setViewTypeDirectoryPrefix()

`setViewTypeDirectoryPrefix(prefix) → this`

* `{String} prefix` — добавочный путь для контроллеров, распознаваемых фабрикой по
[`Url#viewType()`](https://github.yandex-team.ru/pages/nodules/libs/Url.html#viewType).

Метод устанавливает добавочный каталог для контроллеров,
которые резолвятся с использованием
[`Url#viewType()`](https://github.yandex-team.ru/pages/nodules/libs/Url.html#viewType).

Возвращает `this`.

#### factory()

`factory(data) → {Controller|null}`

* `{Object} data` — описание требуемого контроллера, следующего формата:

```javascript
{
    /**
     * Запрос
     * @type {http.IncomingMessage}
     * @property {Url} url_
     */
    req: req,

    /**
     * Ответ
     * @type {http.ServerResponse}
     */
    res: res,

    /**
     * Тип (имя файла) контроллера, например: '404' или 'index'.
     * Если отсутсвует, то используется значение 'index'.
     * Инстансу контроллера будет установлено этоже значение поля `type`,
     * только если тип не был указан при создании наследника `Controller`
     * @type {String}
     */
    type: 'settings',

    /**
     * Каталог контроллеров относительно установленного методом `Controller.setPath()`.
     * Не обязательный параметр.
     * @type {String}
     */
    directory: 'pages/desktop',

    /**
     * Роут, для которого создается контроллер.
     * Предполагается объект с интерфейсом совместимым с susanin.Route
     * @type {Route}
     */
    route: foundRoute,

    /**
     * Хэш параметров запроса.
     * Не обязательный параметр.
     * @type {Object}
     */
    params: foundRoute[1]
}
```

В случае ошибки при создании экземпляра требуемого контроллера будет возвращено значение `null`
и залогирована ошибка `ERROR_IN_CONSTRUCTOR_FACTORY`.

В случае успеха метод вернет экземпляр контроллера.

#### action()

`action(descriptor) → {Controller}`

* `{String} descriptor.name` — имя action'а;
* `{Function} descriptor.fn` — `function(* beforeChainResult)`

Объявляет action в прототипе контроллера.

Функция `descriptor.fn` будет выполняться в контексте экземпляра контроллера.

Возвращает `this`.

#### getAction()

`action(name) → {Function}`

* `{String} name` — имя action'а

Возвращает функцию назначенную действию.

#### before()

`before(fn, options) → this`

* `{Function} fn` — `function(null, String actionName) → {*|Promise}`
* `{Object} [options]` – флаги, которые вляют на то, как обработчик будет добавлен в цепочку:
  * `{Boolean} [options.force]` — добавить обработчик, даже если он уже есть в цепочке;
  * `{Boolean} [options.clear]` — очистить цепочку и после этого добавить обработчик;
  * `{Boolean} [options.reverse]` — добавить обработчик в другой конец цепочки (LIFO для before и FIFO для after).

Добавляет функцию `fn` в массив функций, которые вызываются перед выполнением действия.
Функции выполняются в том порядке, в котором были добавлены (FIFO).

Первый аргумент функции `fn` зарезервирован под ошибки, предшествующие `before`, в настоящий момент всегда `null`.

Выполнение функций обернуто в цепочку промисов.
Если функция бросает исключение (`throw`) или отменяет промис (`Promise#reject`), то выполнение
цепочки `before` будет прервано, action не будет вызван, а управление получит цепочка [`after`](#after),
если она не пустая.

Возвращает `this`.

#### after()

`after(fn, options) → this`

* `{Function} fn` — `function({*|null} error, {*} actionResult, String actionName) → {*|Promise}`
* `{Object} [options]` — см. описание в [`before()`](#before).

Добавляет функцию `fn` в массив функций, которые вызываются после выполнения действия,
а также в случае ошибки в action или цепочке `after`.
Функции выполняются в порядке, обратном порядку добавления (LIFO).

Выполнение функций обернуто в цепочку промисов.
Если функция бросает исключение (`throw`) или отменяет промис (`Promise#reject`), то выполнение
цепочки `after` будет прервано.

Возвращает `this`.

### Свойства прототипа

Помимо перечисленных ниже методов включает в себя подмешанные методы
для работы с параметрами из [ControllerParams](ControllerParams.md).

#### callAction()

`callAction(name) → {Promise}`

* `String name` — имя action'а, который нужно выполнить.

Вызывает метод `action_<name>`, который должен вернуть промис или знаачение, которым будет разрешен промис.
Если у экзепляра контроллера нет соответвующего метода, то промис будет раазрешен ошибкой `UNDEFINED_ACTION`.

Если у инстанса контроллера определены методы `before` и `after`,
то они будут выполнены перед выполнением действия и после него, соответственно.

#### getReferer()

`getReferer → {String}`

Возвращает значение заголовка `Referer` или пустую строку, если заголовок отсутствует.

#### getRoute()

`getRoute() → {Route}`

Возвращает роут, который был передан конструктору контроллера (или методу [Controller.factory](#factory)) при создании.

#### createBadRequestError()

`createBadRequestError(reason) → {ControllerError}`

* `{String|String[]} [reason="unknown reason"]` — причина ошибки, будет подставлена в сообщение об ошибке.

Если `reason` — массив строк, то он используется, как массив имен параметров запроса. Каждый из параметров будет проверен,
те из них, что отсутствуют в запросе, попадут в сообщение об ошибке, как часть сообщения: `"Required params is absent: <names>"`.
Все переданные имена будут доступны в поле `error.data.requiredParams`, а отсутсвующие в `error.data.absentParams`.

Пример использования:

```javascript
var ControllerError = require('nodules-controllers').Controller.ControllerError;

Gate_Tank.action({ name: 'fire', fn: function() {
    var REQUIRED_PARAMS = [ 'lon', 'lat' ];

    if ( ! this.hasParams(REQUIRED_PARAMS)) {
        throw this.createBadRequestError(REQUIRED_PARAMS).log();
    }

    return {
        action: 'fire',
        target: this.getParams(REQUIRED_PARAMS)
    };
});
```

Возвращает экземпляр [`ControllerError`](#controllererror) с кодом `BAD_REQUEST`.

#### createEmptyResponseError()

`createEmptyResponseError(reason) → {ControllerError}`

* `{String} [reason="unknown reason"]` — причина ошибки, будет подставлена в сообщение об ошибке.

Возвращает экземпляр [`ControllerError`](#controllererror) с кодом `EMPTY_RESPONSE`.
