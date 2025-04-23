#i-feeds-errors-dictionary#

##Описание##
Словарь текстов ошибок в фидах - по коду ошибки возвращает "человеческое" описание ошибки

###Автор###
[heliarian ](https://staff.yandex-team.ru/heliarian )

###Где используется###
b-feeds-history


##Пример##

`
    u['i-feeds-errors-dictionary'].getErrorText({
        code: '1201',
        message: 'Some short message from server'
    })

`
