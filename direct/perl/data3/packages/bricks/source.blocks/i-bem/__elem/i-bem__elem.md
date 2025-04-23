r102563

С помощью этого расширения можно работать с элементами почти так же, как и с обычными блоками, т.е. любой (но необязательно каждый) элемент может иметь свой инстанс.

wiki: http://wiki.yandex-team.ru/users/einstain/bem/i-bemelem

Совместимо с Лего 2.9 и 2.10. На более ранних версиях не тестировалось.

----

ДЕКЛАРАЦИЯ ЭЛЕМЕНТА.

BEM.DOM.decl({

    block: 'menu',
    elem: 'item'

}, {}, {});

Декларация модификатора элемента:

BEM.DOM.decl({

    block: 'menu',
    elem: 'item',
    modName: 'state',
    modVal: 'current'

}, {}, {});

Для модификаторов элементов действуют все те же правила, что и для модификаторов блоков.

----

РАСШИРЕННОЕ АПИ БЛОКА.

Найти все инстансы указанного элемента:

this.elemInstances('item'); // эквивалентно this.findBlocksInside('menu__item');
this.elemInstances(items); // items - jQuery-коллекция

Найти все инстансы указанного модификатора элемента:

this.elemInstances('item', 'state', 'current');

Для поиска одного (первого) инстанса есть хелпер с аналогичным апи:

this.elemInstance('item');

----

Найти элемент снаружи контекста:

{
    block: 'menu',
    content: {
        elem: 'item',
        content: {
            elem: 'link'
        }
    }
}

this.closestElem(this.elem('link'), 'item'); // this => menu

- возвращает jQuery-коллекцию!

----

Обработчики onElemSetMod блока сработают, если инстанс элемента сам установит себе соответствующие модификаторы:

onElemSetMod: { // this => menu
    'item': {
        'state': {
            'current': function() {
                /*...*/
            }
        }
    }
}

this.setMod('state', 'current'); // this => menu__item

----

АПИ ЭЛЕМЕНТА.

Элемент имеет все те же самые хелперы, что и обычный блок, но некоторые из них работают немного иначе. Кроме того, у элементов есть ряд дополнительных хелперов.

----

Вернуть родительский блок:

this.getParent() // эквивалентно this.findBlockOutside('menu') + инстанс блока кэшируется

----

Отложенная инициализация по событию родительского блока:

this.liveInitOnParentEvent('switch', function() {});

Отложенная инициализация по событию блока снаружи текущего элемента (или блока):

this.liveInitOnBlockOutsideEvent('switch', 'menu', function() {});

Отличие заключается в следующем:

{
    block: 'menu', // (1)
    content: {
        elem: 'item', // (a)
        content: {
            block: 'menu', // (2)
            content: {
                elem: 'item' // (b)
            }
        }
    }
}

При использовании liveInitOnBlockOutsideEvent элемент (b) будет проинициализирован по собитию на блоке (1) или (2).
При использовании liveInitOnParentEvent элемент (b) будет проинициализирован только по собитию на блоке (2).

----

Поиск элемента снаружи текущего:

{
    block: 'menu',
    content: {
        elem: 'item',
        content: {
            elem: 'link'
        }
    }
}

this.closestElem('item'); // this => menu__link

При использовании этого хелпера, также как и для обычного блока, можно указать контекст первым параметром:

this.closestElem(ctx, 'item'); // ctx - jQuery-коллекция

----

Поиск элементов и блоков.

Элемент ищет только вложенные в него элементы:

{
    block: 'menu',
    content: [
        {
            elem: 'item',
            content: {
                elem: 'link' // (1)
            }
        },
        {
            elem: 'link' // (2)
        }
    ]
}

this.findElem('link'); // this => menu__item

- будет найден только элемент (1).

Если нужно найти все элементы link, поиск нужно производить от имени блока-родителя:

this.getParent().findElem('link'); // this => menu__item

- будут найдены элементы (1) и (2).

Все это также справедливо для хелпера this.elem и хелперов поиска блоков (this.findBlockInside и др.).

----

Обработчики onSetMod элемента сработают, если родительский блок установит этому элементу соответствующие модификаторы:

onSetMod: { // this => menu__item
    'state': {
        'current': function() {
            /*...*/
        }
    }
}

this.setMod(this.elem('item'), 'state', 'current'); // this => menu

Обработчики onElemSetMod в контексте инстанса элемента не используются.
