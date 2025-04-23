# Supply

## Что такое supply?

Однажды нам нужно было сделать так, чтобы любой кликабельный элемент конструктора мог открывать свой контент в iframe. Причем для любого элемента делаться это должно единообразно.

Немного подумав, мы решили сделать что-то очень похожее на миксины. В нашей терминологии они называются supply.

Они принимают на вход **bemjson**, и **API** произвольного блока, ищут там знакомые поля, и, если находят, то каким-либо образом оборачивают или модифицируют первоначальный блок.

Различные supply нужны для того, чтобы похожие задачи на серпе решались одинаково. Это значит, что supply используются в большом количестве разнообразных мест и их код должен быть оптимальным, максимально качественно покрыт тестами и примерами.

## Как использовать supply?

### Произвольный supply

Например, чтобы добавить к кликабельному блоку возможность открывать свой контент в стандартном `iframe` нужно сделать вот что:
```js
blocks['my-block'](context, dataset) {
    var bemjson = { block: 'my-block', content: dataset.value };

    return blocks['supply'](context, dataset, ['enframed'], bemjson);
};

/**
 * @typedef {Object} MyBlock
 *
 * @mixes Enframed
 *
 * @property {String} value - some Value
 */
```

После этого блок `my-block` начнет понимать параметры `enframed`, и стандартным образом обрабатывать поля для фрейма. Различные виды `supply` – это элементы блока `supply`.

### Готовые наборы различных supply

Часто нам нужны примерно одинаковые наборы supply (`url-and-counter`, `ajax`, `target`, `enframed`, `previewed`) для различных элементов. Для этой цели у нас есть заранее собранные пресеты, они хранятся под модификатором [for](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/supply/_for).

Например, навесить стандартный список `supply` для кликабельных элементов с урлом (кнопка, ссылка, и т.д.) можно следующим образом:
```js
blocks['my-block'] = function(context, dataset) {
  var bemjson = { block: 'my-block', content: dataset.value };

  return blocks['supply_for_link'](context, dataset, { 'url-and-counter': { token: 'link' } }, link);
};

/**
 * @typedef {Object} MyBlock
 *
 * @mixes SupplyForLink
 *
 * @property {String} value - some Value
 */
```

## Как сделать новый supply?

### Одиночный supply

Если у вас появилась задача добавить возможность какого-либо поведения некоторому набору блоков, значит вам нужно сделать новый supply. Порядок действий в этом случае такой:

#### Шаг 1

Создаём новый `supply`. На файловой системе он должен лежать отдельно. Например, в `supply/__my-supply/supply__my-supply.priv.js`

#### Шаг 2

Пишем код, документацию и `@typedef`, который в последствии будет микситься ко всем использующим новый `supply` блокам. Если у нового `supply` будут клиентские стили/скрипты, то создаем бандл.

**Например**
```js
/**
 * Мой самый крутой supply.
 *
 * @param {Context} context
 * @param {MySupply} model - Вообще-то сюда приходит Dataset произвольного блока, но мы
 *     смотрим только на те поля, о которых знаем.
 * @param {Bemjson} bemjson - Bemjson того объекта к которому применяем supply,
 *     результат работы supply - это правки в этом bemjson.
 */
blocks['supply__my-supply'] = function(context, model, bemjson) {
    if(!model.mySupply) return;

    context.reportData.pushBundle('my-supply');

    /* ... */

    _.bemMix(bemjson, { block: 'my-supply',  js:{ url: bemjson.url, text: bemjson.text } })
};

/**
 * @typedef {Object} MySupply
 *
 * @property {Object} mySupply - параметры нового supply.
 * @property {String} mySupply.importantArg -  очень важный аргумент нового supply.
 */
```

#### Шаг 3

Прописываем зависимость от нашего нового supply в [deps.js](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/supply/supply.deps.js) блока `supply`.

После этого он станет доступен для использования обычным способом (см. Как использовать произвольный supply).

#### Шаг 4

Если этот supply необходим в одном или нескольких пресетах (например, это стандартная функциональность для всех ссылко-подобных элементов), то стоит внести его в соответствующие `supply_for` (в сам метод и в документацию). После чего он автоматически станет доступен всем элементам, использующим данный пресет.

**Замечание:** supply может не только рабоотать как микс, но и модифицировать переданный BEMJSON. Такой supply должен обязательно вернуть модифицированный BEMJSON.

### Supply for...

Очень редко, может появляться новый класс блоков **(скорее всего это не ваш случай)**, которые объединяет похожесть их supply-ев. В таком случае вы можете сделать новый supply_for.

#### Шаг 1

Создаем новое значение модификатора for в блоке `supply`. На файловой системе оно должно быть отдельным файлом, например: `supply/_for/supply_for_awesome-blocks`.

#### Шаг 2

Пишем сам код, документацию и `@typedef`. `@typedef` должен быть составным и содержать в себе только mix-ы других supply.

**Например**
```js
 /**
 * Supply который применяет сразу несколько supply, характерных для офигительных элементов.
 *
 * @param {Context} context
 * @param {Object} dataset - Исходные данные, пришедшие в блок где используется supply
 * @param {Object} options - Объект, ключи которого - названия отдельных supply, которым нужно пробросить параметры,
 *      а значениями являются соответственно сами параметры.
 * @param {Bemjson} bemjson - Bemjson дерево, получившееся на выходе блока, в котором используется supply
 */
blocks['supply_for_awesome-blocks'] = function(context, dataset, options, bemjson)  {
    if(!model.mySupply) return;

    context.reportData.pushBundle('my-supply');

    /* ... */
};

/**
 * @typedef {Object} SupplyForAwesomeBlcoks
 *
 * @mixes Enframed
 * @mixes MySupply
 */
```

#### Шаг 3

Прописываем зависимость от нашего нового `for` в [deps.js](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/construct/blocks-common/supply/supply.deps.js) блока `supply`.

После этого он станет доступен для использования обычным способом (см. Готовые наборы различных supply).
