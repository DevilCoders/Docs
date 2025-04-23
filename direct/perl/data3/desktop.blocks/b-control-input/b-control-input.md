#b-control-input#

##Описание##
Блок b-control, реализованный в виде "какое-то поле ввода триггерящее событие action"
В чистом виде не используется. Реализации для конкретных полей ввода лежат в _input-type


###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

##Пример##

`
    {
        block: 'b-control-input',
        action: 'blur',
        value: [{ min: 100, max: 1000 }],
        mods: { 'input-type': 'range-input' }
    }

`
