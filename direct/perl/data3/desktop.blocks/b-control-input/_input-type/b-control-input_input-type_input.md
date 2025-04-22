#b-control-input_input-type_input#

##Описание##
Реализация b-control для контрола ввода input

###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

##Как пользоваться и расширять##
В качестве action используется любое событие, которое способен триггерить input
inputMix - mixin который будет навешан на контрол ввода


##Пример##
`
    {
        block: 'b-control-input',
        action: 'blur',
        value: 200,
        inputMix: { block: 'b-my-block', elem: 'input-mixin' },
        mods: { 'input-type': 'input' }
    }

`
