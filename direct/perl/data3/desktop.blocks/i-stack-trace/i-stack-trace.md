#i-stack-trace#

##Описание##
Блок расширяет функционал для работы со стектрейсом ошибок. Использует npm пакет stacktrace-js.

###Автор###
[ngraf](https://staff.yandex-team.ru/ngraf)

##Задачи##
* [DIRECT-46836](https://st.yandex-team.ru/DIRECT-46836)

##Пример##

###Создание стектрейса из ошибки###

```
    BEM.blocks['i-stack-trace'].fromError(new Error())
```
