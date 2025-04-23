#b-overflow-luxury-scroll

##Описание
Делает контнент скроллируемым по вертикали, необходимую высоту нужно задавать снаружи.
Лакшери заключается в наличии двух градиентов (от белого до прозрачного) на элементах по краям сверху и снизу,
которые проявляются когда пользователь отскролил от соответствующего края.
Высоту элементов можно задать через js-параметр `bleachHeight`, по умолчанию она равна `20`;

Выглядит [вот так](https://jing.yandex-team.ru/files/cyn/Chastnye_sdelki_2018-01-30_00-24-05.png)

###Меинтейнеры
[cyn](https://staff.yandex-team.ru/cyn)

##Пример
```(js)
BEM.DOM.append($('body'), BEMHTML.apply({
    block: 'b-overflow-luxury-scroll',
    js: { bleachHeight: 25 },
    attrs: { style: 'height: 200px' },
    content: u._.range(100).map(function(i) {
        return { tag: 'div', content: 'строка ' + i }
    })
}))
```
