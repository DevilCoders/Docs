r109458

http://wiki.yandex-team.ru/users/einstain/bem/b-toggle

----

Универсальный многоуровневый переключатель панелей.

({
    block: 'b-toggle',
    content: [
        {
            elem: 'menu',
            content: ['tab1', 'tab2', 'tab3']
        },
        {
            elem: 'toggle',
            items: ['panel1', 'panel2', 'panel3']
        }
    ]
})

Элемент menu - это переключатель на основе блока b-menu из Лего. Переключатель опционален, т.е. вместо b-menu вы можете использовать другой переключатель или даже написать свой. Пример переключателя на основе b-form-radio:

({
    block: 'b-toggle',
    content: [
        {
            elem: 'radio',
            content: ['button1', 'button2', 'button3']
        },
        {
            elem: 'toggle',
            items: ['panel1', 'panel2', 'panel3']
        }
    ]
})

Вы можете использовать развернутый вид описания элементов для блока-переключателя. Это может понадобиться, если нужно их доопределить:

{
    elem: 'menu',
    content: [
        {
            block: 'link',
            mods: { pseudo: 'yes' },
            cls: 'my-custom-class',
            content: 'tab1'
        },
        {
            block: 'link',
            mods: { pseudo: 'yes' },
            content: 'tab2'
        }
    ]
}

Элемент toggle - контейнер для панелей. Сами панели - это элементы item. Контент для элемента toggle можно тоже описать в развернутом виде. Для этого нужно вместо поля items использовать поле content:

{
    elem: 'toggle',
    content: [
        {
            elem: 'item',
            elemMods: { state: 'hidden' },
            content: 'panel1'
        },
        {
            elem: 'item',
            elemMods: { state: 'visible' },
            content: 'panel2'
        }
    ]
}

В примере выше продемонстрирована возможность указать текущую панель с помощью модификатора _state. В свернутом виде для этого используется параметр current, задающий индекс (начиная с нуля) панели, которую нужно сделать видимой:

{
    elem: 'toggle',
    current: 1,
    items: ['panel1', 'panel2']
}

Этот индекс должен совпадать с таким же индексом переключателя:

{
    elem: 'radio',
    current: 1,
    content: ['button1', 'button2']
}

По умолчанию текущий элемент переключателя и текущая панель соответствуют индексу 0.

Один блок b-toggle может иметь несколько переключателей, каждый из которых будет отвечать за свой уровень панелей. Для этого элементы переключателя и контейнера панелей необходимо связать js-параметром name (его значение может быть произвольным):

({
    block: 'b-toggle',
    content: [
        {
            elem: 'menu',
            js: { name: 'menu-level' },
            content: ['tab1', 'tab2']
        },
        {
            elem: 'radio',
            js: { name: 'radio-level' },
            content: ['button1', 'button2']
        },
        {
            elem: 'toggle',
            js: { name: 'menu-level' },
            items: [
                {
                    elem: 'toggle',
                    js: { name: 'radio-level' },
                    items: ['tab1 - panel1', 'tab1 - panel2']
                },
                {
                    elem: 'toggle',
                    js: { name: 'radio-level' },
                    items: ['tab2 - panel1', 'tab2 - panel2']
                }
            ]
        }
    ]
})

В нашем примере блок b-menu переключает первый уровень панелей, каждая из который содержит свой, внутренний контейнер панелей, переключаемых с помощью b-form-radio (см. морду http://sprav.yandex.ru)

Если у вас есть только одна панель, которая должна появляться при определенном положении переключателя, то нет необходимости создавать пустые панели. Достаточно элементу toggle указать поле state и js-параметр index, соответствующий индексу нужного элемента переключателя:

({
    block: 'b-toggle',
    content: [
        {
            elem: 'menu',
            content: ['tab1', 'tab2', 'tab3']
        },
        {
            elem: 'toggle',
            js: { index: 2 },
            state: 'hidden',
            items: ['show on tab3']
        }
    ]
})

Блок можно использовать для показа/скрытия одной панели по клику на ссылке (кнопке и т.п.):

({
    block: 'b-toggle',
    content: [
        {
            elem: 'link',
            content: 'click me'
        },
        {
            elem: 'toggle',
            state: 'hidden',
            items: ['some text']
        }
    ]
})

Анимация. Для этого достаточно указать модификатор _animation у элемента toggle:

({
    block: 'b-toggle',
    content: [
        {
            elem: 'menu',
            content: ['tab1', 'tab2', 'tab3']
        },
        {
            elem: 'toggle',
            elemMods: { animation: 'fade' },
            js: { duration: 'fast' },
            items: ['panel1', '2nd panel', 'three']
        }
    ]
})

В примере также продемонстрирован способ управления скоростью анимации (параметр duration опционален).
На данный момент реализовано два типа анимации: fade (jQuery: fadeIn, fadeOut) и slide (jQuery: slideDown, slideUp). Можно добавить свои типы анимации.

Блок b-toggle может быть сколь угодно вложенным сам в себя:

({
    block: 'b-toggle',
    content: [
        {
            elem: 'menu',
            content: ['1', '2', '3']
        },
        {
            elem: 'toggle',
            items: [
                'sun',
                'rabbit',
                {
                    block: 'b-toggle',
                    content: [
                        {
                            elem: 'menu',
                            content: ['a', 'b', 'c']
                        },
                        {
                            elem: 'toggle',
                            items: [
                                'boy',
                                {
                                    block: 'b-toggle',
                                    content: [
                                        {
                                            elem: 'menu',
                                            content: ['i', 'ii', 'iii']
                                        },
                                        {
                                            elem: 'toggle',
                                            items: ['love', 'sex', 'smile']
                                        }
                                    ]
                                },
                                'girl'
                            ]
                        }
                    ]
                }
            ]
        }
    ]
})
