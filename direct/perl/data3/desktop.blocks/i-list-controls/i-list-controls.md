#i-list-controls#

##Описание##
Коллекция элементов списка в "стандартном" дизайне.  
Все элементы поддерживают работу со списком, подмешивая на себя `i-list__control`  

##Пример##
С использованием i-list-controls пример списка из i-list может быть реализован следующим образом:

    {
        block: 'some-block-which-uses-i-list',
        mix: { block: 'i-list' },
        content: [
            {
                elem: 'item',
                content: [
                    'Элемент раз',
                    {
                        block: 'i-list-controls',
                        elem: 'edit',
                        params: { itemId: 1 }
                    }
                ]
            },
            {
                elem: 'item',
                content: [
                    'Элемент два',
                    {
                        block: 'i-list-controls',
                        elem: 'edit',
                        params: { itemId: 2 }
                    }
                ]
            },
            {
                block: 'i-list-controls',
                elem: 'add'
            }
        ]
    }

