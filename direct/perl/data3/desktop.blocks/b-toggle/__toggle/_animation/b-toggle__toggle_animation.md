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

