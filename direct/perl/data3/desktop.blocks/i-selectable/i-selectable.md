r102588
## i-selectable ##

## Описание ##
Блок, предоставляющий api хранения и установки выбранности элементов и отображения выбранности на DOM, через блоки b-selectable-control.
Хранит в себе произвольные элементы, в виде пар "ключ - значение", а также соответствующие этим элементам блоки.
Элементы можно задать либо через js-параметры блока i-selectable, либо задавая параметры прямо на b-selectable-control.
При обновлении состояния блока b-selectable-control обновляется состояние элемента, и наоборот.
Не каждый элемент i-selectable обязан иметь соответствующий b-selectable-control
Если какие-то b-selectable-control появились после инициализации блока (например, при аяксовой отрисовке), нужно уведомить i-selectable о новых блоках:

    this._selectable = this.findBlockOn(this.domElem, 'i-selectable');
    this._selectable.considerItemNodes();

## Автор ##
[alkaline](https://staff.yandex-team.ru/alkaline)

## Примеры ##

### Со сбором данных из dom ###

    // some-block.bemhtml
    {
        block: 'some-block',
        mix: { block: 'i-selectable' },
        content: [
            {
                block: 'checkbox',
                mods: { size: 'xs' },
                mix: [
                    {
                        block: 'b-selectable-control',
                        mods: { type: 'checkbox' },
                        js: {
                            key: 1,
                            data: { param1: 1 }
                        }
                    }
                ]
            },
            {
                block: 'checkbox',
                mods: { size: 'xs', checked: 'yes' },
                mix: [
                    {
                        block: 'b-selectable-control',
                        mods: { type: 'checkbox' },
                        js: {
                            key: 2,
                            data: { param1: 3 }
                        }
                    }
                ]
            }
        ]
    }

    // some-block.js
    onSetMod: {
        js: function() {
            this._selectable = this.findBlockOn(this.domElem, 'i-selectable');
            this._selectable.getSelected() == [{ param1: 3 }]; //потому что второй чекбокс чекнут
            this._selectable.setSelected({ 1: true, 2: false });
            this._selectable.getSelected() == [{ param1: 1}];
            //после щелчка по второму чекбоксу
            this._selectable.getSelected() == [{ param1: 1 }, { param1: 3 }];
        }
    }

### С указанием данных в параметрах ###

    // some-block.bemhtml
    {
        block: 'some-block',
        mix: {
            block: 'i-selectable',
            js: {
                items: {
                    1: { data: { param1: 1 }, isSelected: true },
                    2: { data: { param1: 2 }, isSelected: false }
                }
            }
        },
        content: [
            {
                block: 'checkbox',
                mods: { size: 'xs' },
                mix: [
                    {
                        block: 'b-selectable-control',
                        mods: { type: 'checkbox' },
                        js: { key: 1 }
                    }
                ]
            },
            {
                block: 'checkbox',
                mods: { size: 'xs' },
                mix: [
                    {
                        block: 'b-selectable-control',
                        mods: { type: 'checkbox' },
                        js: { key: 2 }
                    }
                ]
            }
        ]
    }

    // some-block.js
    onSetMod: {
        js: function() {
            this._selectable = this.findBlockOn(this.domElem, 'i-selectable');
            this._selectable.getSelected() == [{ param1: 1}]; //как в параметрах
        }
    }
