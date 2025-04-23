# suggest2-detect

Вспомогательный блок, который обеспечивает блоку [suggest2](../suggest2/suggest2.ru.md) независимость от библиотеки [islands-romochka](https://github.yandex-team.ru/lego/islands-romochka). В его функции входит:

* Сбор данных о браузере пользователя и определение его возможностей, например, поддержка SVG.
* Отслеживание глобальных состояний, например, нажатие клавиш.

> **NB** По умолчанию блок `suggest2-detect` не подключен к саджесту. Чтобы его использовать, нужно в BEMJSON-декларации явно примиксовать `suggest2-detect` к блоку [suggest2](../suggest2/suggest2.ru.md) с указанием JS-инициализации.

 ```js
{
    block: 'form',
    tag: 'form',
    mix: [
        {block: 'suggest2-form', js: true}
    ],
    content: {
        block: 'suggest2-form',
        elem: 'node',
        content: [
            {
                block: 'input',
                mods: {size: 's', theme: 'normal'},
                mix: {block: 'suggest2-form', elem: 'input'},
                content: {elem: 'control'}
            },
            {
                block: 'button2',
                mods: {size: 's', theme: 'normal', pin: 'clear-round'},
                type: 'submit',
                mix: {block: 'suggest2-form', elem: 'button'},
                text: 'Найти'
            },
            {
                block: 'popup',
                mods: {autoclosable: 'yes', adaptive: 'no', animate: 'no'},
                js: {directions: 'bottom-left'},
                mix: [{
                    block: 'suggest2',
                    mods: {type: 'simple', theme: 'normal', size: 's'},
                    js: {url: '//suggest.yandex.ru/suggest-ya.cgi'}
                }, {
                    block: 'suggest2-detect', js: true
                }],
                content: {elem: 'content'}
            }
        ]
    }
}
```
