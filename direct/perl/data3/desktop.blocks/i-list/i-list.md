#i-list#

##Описание##
Блок поведения списка. Предоставляет интерфейс реагирования на выполнения "действий" над элементами списка.  
Не имеет своего DOM-представления, обязанность построения списка остается на пользователе блока i-list.  
i-list и его элементы `__control` должны быть намиксованы на корень списка и на его элементы соответственно.  
На элементах `__control` слушается DOM событие click, события блоков на этих элементах игнорируются (то есть, к примеру, `disabled: yes` реакцию не предотвратит).  

Для стилизации списка стоит использовать `i-list-style`.  
Контролы для списка в "стандартном" дизайне реализованы в `i-list-controls`.  

##Пример##

В шаблоне

    {
        block: 'some-block-which-uses-i-list',
        mix: { block: 'i-list' },
        content: [
            {
                elem: 'item',
                content: [
                    'Элемент раз',
                    {
                        block: 'link',
                        mix: {
                            block: 'i-list',
                            elem: 'control',
                            elemMods: { action: 'edit' }, // название действия, одновременно является именем события на i-list
                            js: {
                                params: { itemId: 1 } // params из js будут прокинуты в событие под ключом params
                            }
                        },
                        content: 'Правка'
                    }
                ]
            },
            {
                elem: 'item',
                content: [
                    'Элемент два',
                    {
                        block: 'link',
                        mix: {
                            block: 'i-list',
                            elem: 'control',
                            elemMods: { action: 'edit' },
                            js: {
                                params: { itemId: 2 }
                            }
                        },
                        content: 'Правка'
                    }
                ]
            },
            {
                block: 'button',
                mods: { size: 'xs' },
                mix: {
                    block: 'i-list',
                    elem: 'control',
                    elemMods: { action: 'add' }
                    //параметры не обязательны
                },
                content: 'Добавить'
            }
        ]
    }

В js использующего блока

    BEM.DOM.decl('some-block-which-uses-i-list', {
        onSetMod: {
            js: function() {
                this._list = this.findBlockOn(this.domElem, 'i-list');

                this._list.on('add', function(e, data) {
                    //data.params -> { itemId: 1 }
                    //data.target -> dom элемент, по которому кликнули
                });
            }
        }
    })
