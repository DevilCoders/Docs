# bem-page-object

Инструмент для работы с селекторами
* Позволяет создавать селекторы с использованием [bem-sdk](https://github.com/bem/bem-sdk)
* Позволяет хранить селекторы в виде отдельных структур
* Избавляет от копипасты селекторов
* Упрощает изменение селекторов
* Работает с любыми тестовыми фрэймворками, поддерживающими css-селекторы
* Не зависит от типов шаблонизаторов

### Пример использования

Создаем сущность `serp-item` и указываем её внутренние блоки и элементы, с которыми будем взаимодействовать в тестах

```
var PO = {},
    pageObject = require('bem-page-object'),
    Entity = pageObject.Entity;

    PO.serpItem = new Entity('.serp-item');

    // Внутри serp-item есть сниппет .serp-item__snippet
    PO.serpItem.snippet = new Entity('.serp-item__snippet');

    // Также внутри serp-item есть ссылка .serp-item__snippet
    PO.serpItem.itemLink = new Entity('.serp-item__link');

    // serp-item может иметь различные модификаторы
    PO.serpItem0 = PO.serpList.serpItem.mods({ pos: 0 });
    PO.serpItemHovered = PO.serpList.serpItem.mods({ hovered: 'yes' });
    PO.secondSerpItem = PO.serpList.serpItem.nthChild(2);


    //инициализация структуры pageObject
    PO = pageObject.create(PO);

```

### Вспомогательные методы для построения css селекторов
#### descendant
Нужен при необходимости указать вложенные селекторы без увеличения вложенности свойств page object'а.
Например, для селектора `.more .link`, можно было бы сделать так:
```
PO.more = new Entity('.more');
PO.more.link = new Entity('.link');
// PO.more.link() === '.more .link';
```
с descendant будет так:
```
PO.moreLink = new Entity('.more').descendant(new Entity('.link'));
// PO.moreLink() === '.more .link';
```
Таким образом, если селектор `.more` не используется нигде самостоятельно, то можно не описывать его в структуре page object.

#### adjacentSibling
Позволяет создавать правила `.a + .b`
```
PO.titleAdjacentSibling = new Entity('.title').adjacentSibling(new Entity('.path'));
PO = helpers.create(PO);
// PO.titleAdjacentSibling() === '.title + .path'
```

#### generalSibling
Позволяет создавать правила `.a ~ .b`
```
PO.titleGeneralSibling = new Entity('.title').generalSibling(new Entity('.subtitle'));
// PO.titleGeneralSibling() === '.title ~ .subtitle'
```

#### child
Позволяет создавать правила `.a > .b`
```
PO.titleChild = new Entity('.title').child(new Entity('.price'));
// PO.titleChild() === '.title > .price'
```

#### mix
Позволяет создавать миксованные блоки. Бросает ошибку, если в блоках есть совпадающие элементы.
```
PO.alert = new Entity({block: 'alert'});
PO.popup = new Entity({block: 'popup'});
PO.popup.title = new Entity({block: 'popup', elem: 'title'});
PO.alertPopup = PO.alert.mix(PO.popup);
// PO.alertPopup.title() === '.alert.popup .popup__title'
```

А вот так выбросит исключение:
```
PO.alert = new Entity({block: 'alert'});
PO.alert.title = new Entity({block: 'alert', elem: 'title'});
PO.popup = new Entity({block: 'popup'});
PO.popup.title = new Entity({block: 'popup', elem: 'title'});
PO.alertPopup = PO.alert.mix(PO.popup);
// Error: Одинаковые элементы в сущностях: title
```

При использовании вспомогательных методов (mods, pseudo ...), исходный элемент остается неизменным.

#### nth-child, firstChild, lastChild
Позволяет создавать правила `:nth-child(3)`, `:first-child`, `:last-child`
```
var serpItem = new Entity('.serp-item');
PO.serpItem10 = serpItem.nthChild(10);
// PO.serpItem10() === '.serp-item:nth-child(10)'

PO.firstSerpItem = serpItem.firstChild();
// PO.firstSerpItem() === '.serp-item:first-child'

PO.lastSerpItem = serpItem.lastChild();
// PO.lastSerpItem() === '.serp-item:last-child'
```

#### nthType, firstOfType, lastOfType
Позволяет создавать правила `:nth-of-type(3)`, `:first-of-type`, `:last-of-type`
```
var serpItem = new Entity('.serp-item');
PO.serpItem10 = serpItem.nthType(10);
// PO.serpItem10() === '.serp-item:nth-of-type(10)'

PO.firstSerpItem = serpItem.firstOfType();
// PO.firstSerpItem() === '.serp-item:first-of-type'

PO.lastSerpItem = serpItem.lastOfType();
// PO.lastSerpItem() === '.serp-item:last-of-type'
```


###Получение css-селектора после инициализации

В процессе инициализации page-object обходит нашу структуру сущностей и создает подобную сруктуру из селекторов.
Инициализированная структура становится неизменной, чтобы не было возможности модифичировать ее в коде теста.

```
// Получение селекторов
PO.serpItem();  // .serp-item

PO.serpItem.snippet(); // .serp-item .serp-item__snippet

PO.serpItemHovered(); // .serp-item_hovered_yes

PO.serpItemHovered.snippet(); // .serp-item_hovered_yes .serp-item__snippet

PO.secondSerpItem.snippet() // .serp-item:nth-child(2) ..serp-item__snippet
```

### Использование в тестах

Page object можно использовать в любой тестовой библиотеке, поддерживающей css-селекторы (gemini, webdriver.io и т.д.)

Просто импортируем инициализированный Page object и используем.

#### Page Object + webdriver.io

```
var PO = reqiure('path_to_my_PO');

it('Размеры: маленькие', function() {
    return browser
        .click(PO.iAdvSearch.sizes())
        .click(PO.popups.customSizes.small())
        .waitForLoad()
        .waitForUrl(function(url) {
            return new URI(url).hasQuery('isize', 'small');
        }, 'Включены средние размеры')
        .waitForUrl(function(url) {
            return !new URI(url).hasQuery('isize', 'large');
        }, 'Выключены большие размеры');
});
```
