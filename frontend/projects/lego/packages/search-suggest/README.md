# Search Suggest (ранее Mini Suggest) & i-mini-bem #

В данном репозитории аж две библиотеки: search-suggest и i-mini-bem. search-suggest зависит от i-mini-bem, но требует только малую часть представленной функциональности.
Данное readme - не документация, а, скорее, лёгкий обзор. Документацию (параметры, аргументы, примеры, события) лучше смотреть в коде.

## i-mini-bem ##
Является пародией на i-bem. Отличительные особенности (как плюсы, так и минусы):

* Не зависит от jQuery
* Поддерживаются браузеры: IE 9+, Android 2+, iOS, FireFox,  ...
* Не имеет разделения на DOM/не DOM блоки
* Не поддерживает полностью всю функциональность i-bem
* Примерно базируется на островах 5.2 (булевые модификаторы)
* Распилено на другие отдельные куски
* Обладает частично-необратимо-изменённым похожим апи
* Namespace `MBEM` вместо `BEM`

Пример, декларация блока:
```javascript
MBEM.decl('block', {
    __constructor: function () {
        this.__base.apply(this, arguments);
    }
});
```

### Функциональность из коробки ###

* Наследование и доопределение блоков (baseBlock и вызовы __base)
* Конструктор блока в `__constructor` (не забывайте звать конструктор родительского блока)
* `params` и `domElem` (включая `getDefaultParams`)
* События блока: `on`, `un`, `trigger`
* `bindTo` и `elem`
* `MBEM.cls` и `MBEM.Observable` (classList не везде поддерживается, да)
* `MBEM.blocks` и `MBEM.decl`
* `MBEM.getBlock`, `MBEM.initBlockFromNode`, `MBEM.createBlock`, `MBEM.getNodeParams` (ожидает атрибут `data-bem`)
* `MBEM.prototype` и `MBEM.staticProto` (prototype можно прям динамически дописывать и дополнять, staticProto - перед декларацией блока)
* `MBEM.channel`, `MBEM.closest`, `MBEM.extend`, `MBEM.arrayFrom` и ещё что-то по мелочи

Блок `search-suggest` использует только это.

### Элемент mods ###

Содержит апи по работе с модификаторами:

* Определение блоков с модификаторами (`decl({block: 'block', modName: 'mod', modVal: 'val'})`)
* Обработчики на изменение модификаторов блока (элементы не поддерживаются; можно писать onSetMod вместо __constructor (а можно вместе))
* `getMod`/`hasMod`/`setMod`/`toggleMod`/`delMod`

### Модификатор _init_auto ###

Инициализирует все блоки с классом `i-bem` на странице по DOMContentLoaded.

### Элемент live ###

Апи для ленивой инициализации блоков.

* `decl` с поддержкой `live` в статичных методах
* `liveBindTo`

### Элемент unbind ###

Содержит метод `unbindFrom`.

### Элемент after-current-event ###

Статичный метод и метод экземпляра `afterCurrentEvent`.

### Элемент bind-doc ###

Методы `bindToDoc` и `unbindFromDoc`.

### Другое ###

Не хватает нужного метода? Можно допилить самому в MBEM.prototype или MBEM.staticProto.
`i-mini-bem` покрыт тестами от `i-bem` (с поправками на изменённое/несуществующее апи).

### Некоторые нюансы по переносу кода с i-bem на i-mini-bem ###

`trigger` изменён: теперь он возвращает не сам блок, а результат выполнения последнего обработчика. В событии можно делать `stopPropagation` и последующие обработчики не будут вызваны.

`un` больше не принимает контекст, а в `on` нет аргумента с `data`.

Нет кеша элементов и кеша модификатора элементов (сами модификаторы элементов выставить можно). Нет elemify.

Нет jQuery, поэтому некоторые вещи вроде `val` и `attr` работать не будут.

`BEM.create` вроде неплохо заменяется на `MBEM.createBlock`.

## search-suggest ##

Является упрощённым подобием `suggest2` для `touch-phone` (десктоп и прочее не поддерживается, разделения на common нет). Шаблонизация через простой метод (без bemhtml/bh).
Рассчитывает на наличие внутри себя инпута и кнопки, попап конструирует сам. Пример:

```
npm run examples
```

Открывать `examples/yaru/index.html` или `examples/serp-expanding/index.html`.

Имеет другое апи, по сравнению в `suggest2`. Необходимо лишь объявить `search-suggest` на `form` с нужными параметрами (урл ручки саджеста и статистика):
```json
{
  "search-suggest": {
    "url": "https://yandex.ru/suggest/suggest-endings?srv&wiz=TrWth&uil=ru&fact=1&v=4&icon=1&mob=1&tpah=1&sn=7&full_text_count=5&bemjson=0&yu=1249095521491842055",
    "counter": {
      "service": "morda_ru_touch",
      "url": "//yandex.ru/clck/jclck",
      "timeout": 300,
      "yandexuid": "1249095521491842055",
      "params": {
        "dtype": "stred",
        "pid": "0",
        "cid": "2873"
      }
    }
  }
}
```
Статистика совместима с `suggest2` - пишет тоже самое и в том же формате. Находится в элементе `counter`.
Поставляется с темой `yaru`, но можно без проблем написать свою. За примером шаблона формы можно обратиться к упомянутому выше `examples/yaru/index.html`. Размещение серверных шаблонов в данном репозитории на данный момент не планируется.

### Expanding ###
Также поддерживается вариант с expanding (`serp-expanding` в примерах). Для его работы нужно подключить модификатор `_expanding_yes`, а также указать соответствующий класс на DOM-ноде. Возможно, пригодятся дополнительные опции `lineHeight` и `maxInputHeight` (оба значения в пикселях).

Протестировано в ос/браузерах:

* Android 2.3+ (нативный, chromium, firefox, uc)
* iOS 7+
* WinPhone 7.5+
* Bada 2


Зачем всё это нужно? Итоговый размер около 8.1 кб (без expanding, js+css + minify+gzip).
