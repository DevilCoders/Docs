# scroll-spy
Сервис и блок-микс для отслеживания видимости основного блока при скролле.

Блок покрыт тестами, можно не бояться дополнять его и рефакторить.

## Пример использования как микс
BEMJSON:
```js
{
    block: 'test',
    mix: {
        block: 'scroll-spy',
        js: { visibilityConditions: { area: 0.05, x: 0.1, y: 0.2 } }
    }
}
```

Здесь в качестве параметра `visibilityConditions` передаются условия, при достижении которых блок считается видимым.
Блок считается видимым при достижении всех условий, здесь это процент видимости по площади - 5%, по x - 10%, по y - 20%.

JS:
```js
BEM.DOM.decl('test', {
    onSetMod: {
        js: function() {
            this.findBlockOn('scroll-spy').onFirstBecameVisible(this._onVisible, this);
        }
    },
    
    _onVisible: function() {
        console.log('Этот элемент стал видимым');
    }
});
```

## Методы сервиса

Под методами сервиса подразумеваются статические методы блока `BEM.blocks['scroll-spy']`

### getElemVisibility
```
/**
 * Извлечь степень видимости элемента по осям и площади
 *
 * @param {DomElem} domElem
 *
 * @returns {ScrollSpy.ElemVisibility}
 */
```

### getIntersection
```
/**
 * Найти пересечение двух прямоугольников
 *
 * @param {ScrollSpy.Rect} rect1
 * @param {ScrollSpy.Rect} rect2
 *
 * @returns {ScrollSpy.Intersection}
 */
```

### watchVisibility
```
/**
 * Начать отслеживать видимость элемента. События происходят по событию скролла окна
 *
 * @param {DomElem} domElem
 * @param {ScrollSpy.WatchCallback} callback
 * @param {Object} [ctx] - Контекст вызова колбэка
 *
 * @returns {ScrollSpy}
 */
```

### stopWatchingVisibility
```
/**
 * Остановить отслеживание видимости элемента
 *
 * @param {DomElem} domElem
 * @param {ScrollSpy.WatchCallback} [callback]
 * @param {Object} [ctx] - Контекст предполагаемого колбэка
 *
 * @returns {ScrollSpy}
 */
```

### isElemWatched
```
/**
 * Находится ли элемент под наблюдением?
 *
 * @param {DomElem} domElem
 * @param {ScrollSpy.WatchCallback} callback
 * @param {Object} [ctx] - Контекст предполагаемого колбэка
 *
 * @returns {Boolean}
 */
```

### notifyBecameVisible
```
/**
 * Единожды сообщить, что элемент стал видимым.
 * Если элемент виден при добавлении колбэка - вызов происходит тут же
 *
 * @param {DomElem} domElem
 * @param {ScrollSpy.EventListener} callback
 * @param {Object} [ctx]
 * @param {ScrollSpy.ElemVisibility} [conditions] - Условия, при которых элемент считается видимым
 *  Условие считается выполненным, если текущая видимость будет больше или равной по всем полям
 */
```

### checkVisibilityConditions
```
/**
 * Проверить соответствие показателей видимости условиям.
 * Возвращает true или false в случае выполнения/невыполнения условия или null, если не было сравнений полей
 *
 * @param {ScrollSpy.ElemVisibility} conditions Можно заполнять не все поля
 * @param {ScrollSpy.ElemVisibility} visibility
 *
 * @returns {Boolean|null}
 */
```

### checkWatchedElem
```
/**
 * Принудительно проверить видимость отслеживаемого элемента
 *
 * @param {DomElem} domElem
 */
```
