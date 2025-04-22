#b-control-input_input-type_range-input#

##Описание##
Реализация b-control для контрола ввода диапазона range-input

###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

##Как пользоваться и расширять##
В качестве action используется любое событие, которое способен триггерить range-input
minMix - mixin который будет навешан на контрол ввода нижней границы диапазона
maxMix - mixin который будет навешан на контрол ввода верхней границы диапазона


##Пример##
`
    {
        block: 'b-control-input',
        action: 'blur',
        value: [{ min: 100, max: 1000 }],
        minMix: { block: 'b-my-block', elem: 'min-input-mixin' },
        maxMix: { block: 'b-my-block', elem: 'max-input-mixin' },
        mods: { 'input-type': 'range-input' }
    }

`
