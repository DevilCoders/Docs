Обработка событий в библиотеках islands
---------------------------------------

События в блоках могут быть двух типов:
* [DOM](https://en.wikipedia.org/wiki/DOM_events), возникают на DOM-node, генерируются браузером;
* BEM, генерируются JS-кодом блока. В отличие от DOM-событий, BEM-события генерируются не на DOM-элементах,
  а на экземплярах блоков. Элементы блоков не могут генерировать BEM-события.

В фреймворке [i-bem](http://ru.bem.info/articles/bem-js-main-terms/)
DOM и BEM события обрабатываются разными методами.

### DOM-события

Для работы с DOM `i-bem.js` использует jQuery, так что и взаимодействие с DOM-событиями происходит
уже в нормализованном виде.

#### Экземпляр блока, работа с обработчиками событий

| Целевой DOM-узел                                                | Добавить                                    | Удалить
| --------------------------------------------------------------- | ------------------------------------------- | -------
| Любой                                                           | **bindToDomElem**(domElem, event, fn)       | **unbindFromDomElem**(domElem, event)
| `document`                                                      | **bindToDoc**(event, fn)                    | **unbindFromDoc**(event)
| `window`                                                        | **bindToWin**(event, fn)                    | **unbindFromWin**(event)
| Корневой узел блока (`this.domElem`) или его внутренний элемент | **bindTo**([elem], event, fn)               | **unbindFrom**([elem], event)

#### Класс блока, работа с обработчиками live-событий:

| Целевой DOM-узел, делегирующий обработку к `document`           | Добавить                                              | Удалить
| --------------------------------------------------------------- | ----------------------------------------------------- | -------
| Корневой узел блока (`this.domElem`) или его внутренний элемент | **liveBindTo**([to], event, [callback], invokeOnInit) | **liveUnbindFrom**(elem, event, callback)

### BEM-события

#### Экземпляр блока, работа с обработчиками событий

| Описание                                             | Добавить                      | Удалить
| ---------------------------------------------------- | ----------------------------- | -------
| Установка / удаление обработчика BEM-события блока   | **on**(e, [data], fn, [ctx])  | **un**([e], [fn], [ctx])

* **trigger**(e, [data])
    Генерирует BEM-событие блока.

Подробнее о [событиях в клубе БЭМ](http://clubs.ya.ru/bem/replies.xml?item_no=2453).
Все методы с jsdoc-описанием в файле
[i-bem__dom.js](https://github.com/bem/bem-bl/tree/support/1.x/blocks-common/i-bem/__dom/i-bem__dom.js).

### Схема обработки DOM-событий в `islands`

#### Touch-платформа

Согласно [спецификации W3C](http://www.w3.org/TR/touch-events/), на мобильных платформах определены специальные события
курсора: `touchstart`, `touchend`, `touchmove`, `touchcancel`, но поддержка этих событий не реализована в некоторых
браузерах, например [IE Mobile 10.0 и Opera Mini](http://caniuse.com/#search=touchstart).

Islands-библиотеки используют специальный полифилл (основанный на библиотеке [HandJS](https://handjs.codeplex.com))
[i-pointer-events.js](https://github.com/bem/bem-bl/tree/support/1.x/blocks-touch/i-pointer-events/i-pointer-events.js),
который решает проблемы совместимости. Он подключается автоматически на
уровне [blocks-touch](https://github.com/bem/bem-bl/tree/support/1.x/blocks-touch/i-bem/i-bem.deps.js).

На touch-платформах используются следующие DOM-события, по аналогии с desktop

| touch            | desktop
|-----------       | ----------
| pointerdown      | mousedown
| pointermove      | mousemove
| pointerover      | mouseover
| pointerout       | mouseout
| pointercancel    |
| pointerenter     | mouseenter
| pointerleave     | mouseleave
| pointerup        | mouseup
| **tap**          | **leftclick**

Для touch-события `pointercancel` нет `desktop` аналога.

На touch-платформах согласно [W3C спецификации](http://www.w3.org/TR/touch-events/#mouse-events)
также доступны события мыши: `mousedown`, `mouseup`, `click`.
Мобильные браузеры обрабатывают событие `click` с
[задержкой в 300ms](http://updates.html5rocks.com/2013/12/300ms-tap-delay-gone-away).

Библиотека [fastclick](https://github.com/ftlabs/fastclick), которую мы
[используем](https://github.com/bem/bem-bl/tree/support/1.x/blocks-touch/i-fastclick/i-fastclick.js),
 ускоряет срабатывание события `click`, генерируя синтетическое аналогичное событие,
 но блокирует сопровождающие события `mousedown/mouseup`.
Для совместимости с текущей на портале реализацией счетчиков через HTML-атрибут `onmousedown`,
 сделан костыль в **fastclick**, генерирующий событие `mousedown` ( [ISLCOMPONENTS-832](https://st.yandex-team.ru/ISLCOMPONENTS-832) ).

Событие `tap` создано для совместимости при использовании `islands`-библиотек вместе с библиотекой `romochka`
(в ней событие `tap` уже использовалось и библиотека заморожена).

Итак, событие `click` обрабатывается согласно схеме:

* common – `leftclick tap`;
* desktop – `leftclick`;
* touch-уровни – `tap`.

Пример для common-уровня, установка обработчика для корневого элемента блока:

```js
this.bindTo('leftclick tap', function(e) {
    console.log(e.type);
});
```

#### Примечание для DOM live-событий

В live-секции можно использовать только те события, которые всплывают до DOM-node `document`,
иначе код работать не будет.

Все DOM-события перечислены в документах [W3C DOM Level 3Events](http://www.w3.org/TR/DOM-Level-3-Events/#event-types-list)
 и [W3C pointer-events](http://www.w3.org/TR/pointerevents/#list-of-pointer-events).

Не всплывают события:
* [load](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-load)
* [unload](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-unload)
* [resize](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-resize)
* [abort](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-abort)
* [error](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-error)
* [focus](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-focus)
* [blur](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-blur)
* [scroll](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-scroll) ([исключение](http://www.w3.org/TR/DOM-Level-3-Events/#scroll-document))
* [mouseenter](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-mouseenter)
* [mouseleave](http://www.w3.org/TR/DOM-Level-3-Events/#event-type-mouseleave)
* [pointerenter](http://msdn.microsoft.com/en-us/library/windows/apps/dn251894.aspx)
* [pointerleave](http://msdn.microsoft.com/en-us/library/windows/apps/dn251896.aspx)

Эти события можно обработать только в методах `bindTo()` / `unbindFrom()`.


### Рекомендация по использованию BEM и DOM событий
* Внутри блока использовать DOM-события для регистрации взаимодействия пользователя с DOM-деревом: наведение курсора, клики
мыши, нажатие клавиш и т.д. Помнить,  что не все DOM-события нужны.
К примеру, клик мышкой по неактивной кнопке (`_disabled_yes`) рождает DOM-событие `click`,
но не рождает BEM-событие `click`. Потому что для пользователя (визуально) на кнопке никакого клика не произошло.
* Для взаимоотношений между BEM-блоками использовать BEM-события.
* Для уменьшения связности кода можно использовать [каналы i-bem](https://github.com/bem/bem-bl/blob/dev/blocks-common/i-bem/i-bem.js#L23),
 реализующие паттерн «издатель-подписчик». Каналы могут быть с произвольным именем. Можно генерировать события в этих каналах,
подписываться на каналы и отписываться от них.

### jQuery-плагины и зависимости

Библиотека `bem-bl@1.0.0`:

* [jQuery-плагин для события leftclick](https://github.com/bem/bem-bl/tree/support/1.x/blocks-desktop/i-jquery/__leftclick/i-jquery__leftclick.js)
* [jQuery-плагин для события tap](https://github.com/bem/bem-bl/tree/support/1.x/blocks-touch/i-jquery/__tap/i-jquery__tap.js)

В зависимостях блоков, в js-представлении которых используются события `leftclick` или `tap`,
должны быть указанны соответствующие jQuery-плагины:

```js
    {block: 'i-jquery', elems: ['leftclick', 'tap']} // common
    {block: 'i-jquery', elems: 'tap'} // touch
    {block: 'i-jquery', elems: 'leftclick'} // desktop
```

### Ссылки

* [DOM Level 2 Events Specification](http://www.w3.org/TR/DOM-Level-2-Events/)
* [DOM Level 3 Events Specification](http://www.w3.org/TR/DOM-Level-3-Events/)
* [W3C DOM Events Compatibility](http://www.quirksmode.org/dom/w3c_events.html)
* [DOM Events Browser Support](http://www.webbrowsercompatibility.com/dom-events/desktop/)
* [W3C Touch Events Touch Events](http://www.w3.org/TR/touch-events/)
* <a href="http://msdn.microsoft.com/en-us/library/ie/dn433244(v=vs.85).aspx">Internet Explorer Dev Center: Pointer Events</a>
* [W3C Pointer Events Candidate Recommendation](http://www.w3.org/TR/pointerevents/)
* [HandJS](https://handjs.codeplex.com)
