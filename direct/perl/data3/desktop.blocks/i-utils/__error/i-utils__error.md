#i-utils__error#

##Описание##
Утилиты для работы со вложенной структурой ошибок.

Основная задача утилит делать из иерархического объекта ошибок плоский хэш с ключами-путями и значениями-списками ошибок.

###Автор### 
[coffeeich](https://staff.yandex-team.ru/coffeeich)
[kabzon](https://staff.yandex-team.ru/kabzon)

##Пример##

###Вложенная стурктура серверных ошибок###

```

    var flat = u.error.flattenServer({
        "groups": {
            "generic_errors": [{"text": "error 1"}],
            "array_errors": [
                {
                    "generic_errors": [{"text": "error 2"}],
                    "object_errors": {
                        "banners": {
                            "array_errors": [
                                null,
                                {
                                    "object_errors": {
                                        "creative": [
                                            {
                                                "text": "Геотаргетинг задан неправильно",
                                                "description": "Геотаргетинг группы шире списка стран её cмарт-баннеров"
                                            }
                                        ]
                                    }
                                }
                            ]
                        }
                    }
                }
            ]
        }
    });

    console.log(flat);

    /*
    {
        "groups": [{"text": "error 1"}],
        "groups[0]": [{"text": "error 2"}],
        "groups[0].banners[1].creative": [
            {
                "text": "Геотаргетинг задан неправильно",
                "description": "Геотаргетинг группы шире списка стран её cмарт-баннеров"
            }
        ]
    }
    */
```

###Вложенная стурктура клиентских ошибок###

```

    // вариант 1: указание ведущего префикса ключей groups
    var flat = u.error.flattenClient([
        {
            "group_name": [{ "text": "Необходимо указать название группы"}],
            "performance_filters": [{ "text": "Добавьте в группу фильтры"}]
        }
    ], 'groups');

    console.log(flat);

    /*
    {
        "groups[0].group_name": [{ "text": "Необходимо указать название группы"}],
        "groups[0].performance_filters": [{ "text": "Добавьте в группу фильтры"}]
    }
    */

    // вариант 2: указание ведущего префикса ключей boom
    var flat = u.error.flattenClient([
        {
            "group_name": [{ "text": "Необходимо указать название группы"}],
            "performance_filters": [{ "text": "Добавьте в группу фильтры"}]
        }
    ], 'boom');

    console.log(flat);

    /*
    {
        "boom[0].group_name": [{ "text": "Необходимо указать название группы"}],
        "boom[0].performance_filters": [{ "text": "Добавьте в группу фильтры"}]
    }
    */

    // вариант 3: без указания ведущего префикса ключей, но уже объект
    var flat = u.error.flattenClient({
        groups: [
            {
                "group_name": [{ "text": "Необходимо указать название группы"}],
                "performance_filters": [{ "text": "Добавьте в группу фильтры"}]
            }
        ]
    });

    console.log(flat);

    /*
    {
        "groups[0].group_name": [{ "text": "Необходимо указать название группы"}],
        "groups[0].performance_filters": [{ "text": "Добавьте в группу фильтры"}]
    }
    */
    
    // вариант 4: без указания ведущего префикса ключей совсем
    var flat = u.error.flattenClient([
        {
            "group_name": [{ "text": "Необходимо указать название группы"}],
            "performance_filters": [{ "text": "Добавьте в группу фильтры"}]
        }
    ]);

    console.log(flat);

    /*
    {
        "[0].group_name": [{ "text": "Необходимо указать название группы"}],
        "[0].performance_filters": [{ "text": "Добавьте в группу фильтры"}]
    }
    */
```

###Утилита для построения путей (для сохранения "следа" пути при вложенностях в шаблонах)###

```

    // вариант 1: указание базового пути
    var pathBuilder = u.error.createPathBuilder('groups');

    pathBuilder('performance_filters', 1, 'condition'); // 'groups.performance_filters[1].condition'
    pathBuilder(0, 'performance_filters', 1, 'condition') // 'groups[0].performance_filters[1].condition'

    // вариант 2: без указания базового пути
    var pathBuilder = u.error.createPathBuilder();

    pathBuilder('performance_filters', 1, 'condition'); // 'performance_filters[1].condition'
    pathBuilder(0, 'performance_filters', 1, 'condition') // '[0].performance_filters[1].condition'
```
