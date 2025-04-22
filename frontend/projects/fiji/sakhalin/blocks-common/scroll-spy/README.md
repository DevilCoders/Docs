# scroll-spy

Копипаст из https://github.yandex-team.ru/serp/web4/blob/73a79b49a5f839ce3376a801c435cd2c8213682e/blocks-common/scroll-spy/README.md

Сервис и блок-микс для отслеживания видимости основного блока при скролле.

Блок покрыт тестами, можно не бояться дополнять его и рефакторить.

Можно звать на ревью и консультироваться у [andre487](http://staff/andre487)

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
 * @param {DomElem} domElem
 *
 * @returns {ScrollSpy.ElemVisibility}
 */
```

### getIntersection
```
/**
 * Найти пересечение двух прямоугольников
 * @param {ScrollSpy.Rect} rect1
 * @param {ScrollSpy.Rect} rect2
 * @returns {ScrollSpy.Intersection}
 */
```
