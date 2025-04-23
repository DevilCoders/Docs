#b-error-label#

##Описание##
Блок подсветки ошибок.

Релизует интерфейс `i-error-view-interface`.

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[kabzon](https://staff.yandex-team.ru/kabzon)

###Где используется###
Используется в формах редактирования с серверной и клиентсвкой валидацией (пример страница мультиредактирования Смарт-баннеров).
   
###Взаимодействие с другими блоками###
Предоставляет интерфейс для передачи списка ошибок в блок.
    
##Как пользоваться##
Блок можно использовать как `mix` других блоков (например, label для полей ввода) и использовать с прямым доступом как описано ниже в JS примере.

Можно использовать как один из блоков подсветки ошибок под управлением блока `b-error-presenter`. Для этого необходимо
указать путь `path` ошибки в `js` параметрах блока, например, `js: { path: 'groups[0].banners' }`. Подробнее
можно прочитать в `b-error-presenter.md`.

##Пример##

BEMHTML:

```

    {
        block: 'label',
        mix: { block: 'b-error-label', js: { path: 'nested.errors[0].path' } },
        content: iget('Name')
    }
```

JS:

```

    var block = ...

    // подсвечивает ошибки
    block.showErrors([
        { text: 'simple error' },
        { description: 'described error' }
    ]);

    // снимает подсвечивание ошибок
    block.clearErrors();
```
