#composite#

##Описание##
Блок - collectionView. Отображает коллекции данных.

Блок берет на себя клиентскую и серверную шаблонизацию данных, а также добавление, удаление и обновления элементов в списке.

###Автор###
[eemelin](https://staff.yandex-team.ru/eemelin)
[alkaline](https://staff.yandex-team.ru/alkaline)


##Как пользоваться и расширять##

Блок может расширяться новыми возможностями для управления элементами списка, например,  virtual-scroll.
Расширяя API следует помнить о событиях, эммитируемых блоком, при действиях с элементами, например, before:update


###Пример 1###

Простейший способ применения

`
    block: 'composite',
    itemView: { block: 'b-inner' },
    collection: [
        { id: 1, name: 'item1' },
        { id: 2, name: 'item2' },
        { id: 3, name: 'item3' }
    ]

`
###Пример 2###

С шаблоном обвязки списка

`
    block: 'composite',
    layout: { block: 'b-some', elem: 'wrap' },
    itemView: { block: 'b-inner' },
    collection: [
        { id: 1, name: 'item1' },
        { id: 2, name: 'item2' },
        { id: 3, name: 'item3' }
    ]

`

###Пример 3###

С шаблоном обвязки списка и элемента

`
    block: 'composite',
    layout: { block: 'b-some', elem: 'wrap' },
    itemView: { block: 'b-some', elem: 'item-tpl' },
    collection: [
        { id: 1, name: 'item1' },
        { id: 2, name: 'item2' },
        { id: 3, name: 'item3' }
    ]

`
###Пример 4###

С шаблоном обвязки списка и элемента и кастомным полем для указания идентификатора

`
    block: 'composite',
    layout: { block: 'b-some', elem: 'wrap' },
    itemView: { block: 'b-some', elem: 'item-tpl' },
    idAttr: 'item_id',
    collection: [
        { item_id: 1, name: 'item1' },
        { item_id: 2, name: 'item2' },
        { item_id: 3, name: 'item3' }
    ]

`

###JS API###

####Добавление строки/строчек####

Добавление одного элемента
`
add(data)
`
Добавление нескольких элементов
`
add([data1, data2, data3])
`
Вставка элемента/элементов по индексу
`
add(data, {
    at: 1
})
`
Вставить элемента/элементов с дополнительной информацией
`
add(data, {
    itemOptions: {
        elemMods: { sate: 'is-new' },
        someFlag: true
    }
})
`

####Обновление строки/строчек####

Обновление одного элемента
`
update(id, data)
`
Обновление нескольких элементов
`
update({
    id1: data1,
    id2: data2
})
`
Обновление одного элемента с дополнительной информацией
`
update(data, {
    itemOptions: {
        elemMods: { state: 'is-updated' }
    }
})
`
Обновление нескольких элементов с дополнительной информацией
`
update({
    id1: data1,
    id2: data2
}, {
    itemOptions: {
        elemMods: { state: 'is-updated' }
    }
})
`

####Удаление строки/строчек####

Удаление одного элемента
`
remove(id)
`

Удаление нескольких элементов
`
remove([id1, id2, id3])
`

####Замена строк####

Заменить одним элементом
`
reset(data)
`
Заменить несколькими элементами
`
reset([data1, data2, data3])
`
Заменить элементом/элементами с дополнительной информацией
`
reset(data, {
    itemOptions: {
        elemMods: { state: 'is-reseted' }
    }
})
`

####Очистка списка####
`
clear()
`
