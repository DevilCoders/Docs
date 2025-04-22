#b-error-message#

##Описание##
Блок вывода ошибок к контролам.

Релизует интерфейс `i-error-view-interface`.

###Авторы### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[kabzon](https://staff.yandex-team.ru/kabzon)

###Меинтейнеры###
[cyn](https://staff.yandex-team.ru/cyn)

###Где используется###
Используется в формах редактирования с серверной и клиентсвкой валидацией (пример страница мультиредактирования Смарт-баннеров).
   
###Взаимодействие с другими блоками###
Предоставляет интерфейс для передачи списка ошибок в блок.
    
##Как пользоваться##
Блок можно вставлять непосредственно на страницу и использовать с прямым доступом как описано ниже в JS примере.

Можно использовать как один из блоков вывода ошибок под управлением блока `b-error-presenter`. Для этого необходимо
указать путь `path` ошибки в `js` параметрах блока, например, `js: { path: 'groups[0].banners' }`. Подробнее
можно прочитать в `b-error-presenter.md`.

##Пример##

BEMHTML:

```

    {
        block: 'b-error-message',
        js: { path: 'nested.errors[0].path' }
    }
```

JS:

```

    var block = ...

    // показывает ошибки
    block.showErrors([
        { text: 'simple error' },
        { description: 'described error' }
    ]); 

    // сбрасывает ошибки
    block.clearErrors();
```
