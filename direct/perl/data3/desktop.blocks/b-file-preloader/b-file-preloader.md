r103821
#b-file-preloader#

##Описание##
Блок для простейшей предзагрузки файла и только с серверной валидацией

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[belyanskii](https://staff.yandex-team.ru/belyanskii)

###Где используется###
Используется в блоках:

* `b-import-csv`
* `b-import-xls`

##Roadmap & known issues##

Разобраться с методом `processErrors`, который используется из вне не должным образом

##Пример##

BEMHTML:

```

    {
        block: 'b-file-preloader',
        name: 'uploadFileName',
        url: '/url/to/upload',
        data: {
            add: 'params',
            to: 'upload',
            as: 'extra-data'
        },
        timeout: 600000
    }
```

JS:

```

    var filePreloader = ...
    
    filePreloader.on('reset error uploaded', function(event, data) {
        console.log(event.type, data);
    }, this);
```
