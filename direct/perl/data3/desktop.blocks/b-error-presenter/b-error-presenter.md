#b-error-presenter#

##Описание##
Блок для распределения ошибок в рамках своего скоупа по блокам реализующим интерфейс `i-error-view-interface`

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[kabzon](https://staff.yandex-team.ru/kabzon)

###Где используется###
 - p-multiedit2_type_dynamic-media (создание/редактирование группы смарт-баннеров)

###Взаимодействие с другими блоками###
Блок подмешивается к блоку страницы или блоку декоратору, после чего через публичные методы делегируется распределение ошибок
в рамках области видимости блока. Для этого внутри скоупа должны содержаться блоки реализующие интерфейс `i-error-view-interface`
и имеющие в js параметрах блока ключ пути ошибки (например, `{ js: { path: 'groups[0].performance_filters[0].filter_name' } }`)
    
##Пример##

###Шаблон (например, my-page-block.bemhtml)###

```

    {
        block: 'my-page-block',
        mix: { block: 'b-error-presenter' },
        content: [
            // ... какие то блоки
                // можно его и специфицировать
                { block: 'my-error-generic', js: { path: 'groups' } },
                // ... какие то блоки
                    {
                        block: 'label',
                        // для стилизации блока лэйбла при возникновении ошибок
                        mix: { 
                            block: 'my-error-label', // блок должен реализовывать i-error-view-interface
                            js: { path: 'groups[0].performance_filters[0].filter_name' }
                        },
                        content: 'Поле'
                    },
                    {
                        block: 'input',
                        mods: { size: 'xs' },
                        // для выставления модификатор блока поля ввода при возникновении ошибок
                        mix: { 
                            block: 'my-error-input', // блок должен реализовывать i-error-view-interface
                            js: { path: 'groups[0].performance_filters[0].filter_name' }
                        },
                        content: { elem: 'control' }
                    },
                    // для вывода сообщения при возникновении ошибок
                    { 
                        block: 'my-error-message', // блок должен реализовывать i-error-view-interface
                        js: { path: 'groups[0].performance_filters[0].filter_name' }
                    },
                // ... какие то блоки
                // для вывода всех сообщений не нашедших своих блоков вывода
                { 
                    block: 'my-error-message', // блок должен реализовывать i-error-view-interface
                    js: { path: 'groups[0]' }
                },
            // ... какие то блоки
        ]
    }
```

###js (например, my-page-block.js)###

```

    BEM.DOM.decl('my-page-block', {
        onSetMod: {
            js: function() {
                // ... какой-то код
                var errorPresenter = this.findBlockOn('b-error-presenter');
                // ... какой-то код
                    // ... какой-то код
                        // делегирует найденному блоку отобразить ошибку
                        errorPresenter.showErrors({
                          'groups[0].group_name': [{ text: 'error for generic message' }],
                          'groups[0].performance_filters[0].filter_name': [{ text: 'terrible horror' }]
                        });
                    // ... какой-то код
                // ... какой-то код
                    // ... какой-то код
                        // делегирует найденному блоку очистить сообщение об ошибке
                        errorPresenter.clearErrors();
                    // ... какой-то код
                // ... какой-то код
            }
        },
        // ... какой-то код
    });
```
