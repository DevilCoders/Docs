#i-controls-overseer#

##Описание##
Фасад к контролам b-control

###Автор###
[alkaline](https://staff.yandex-team.ru/alkaline)
[eemelin](https://staff.yandex-team.ru/eemelin)

###Взаимодействие с другими блоками###
b-control - live подписывается на событие actionRequested

##Как пользоваться##
Миксуется на блок в котором находятся контролы.
Так как подписка live, используйте ключ of чтобы фильтровать контролы.

Использование (подробнее в примере):

1) Создает Микс на блоке-хозяине.
2) Маркируем контролы Микс-фильтром.
3) Подписывемся в JS (рекомендуется использовать i-subscription-manager)

##Пример##

Микс на блоке-хозяине
`
mix()(function() {
    return {
        block: 'i-controls-overseer',
        js: {
            of: { block: 'owner', elem: 'control' }
        }
    }
})
`

Микс-фильтр
`
{
    block: 'b-control-add',
    mix: {
        block: 'owner',
        elem: 'control'
    }
}
`

Подписка
`
this._subscriptionManager = BEM.create('i-subscription-manager');

this._subscriptionManager.wrap(this.findBlockOn('i-controls-overseer'))
    .on('add', this._onAddRequest, this);
`
