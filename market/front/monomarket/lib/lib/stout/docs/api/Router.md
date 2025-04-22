Router
=====

Роутер, наследует от [Susanin](https://github.com/nodules/susanin).

___

#### <a name="route" />Объект роут
Объект описывает запрос, принимаемый сервисом.

**Пример роута:**
```js
{
    "name": "root",
    "pattern": "/",
    "data": {
        "method": "GET",
        "pageName": "Index", // уникальное имя в рамках проекта {@see Route.buildURL}
        "pageData": { // будет передано в качестве данных страницы `page.data`.
            "template": "index.yate"
        }
    }
}
```
___

#### <a name="Router" />{Router} new Router(routes) ####
Создает роутер.

**Параметры:**
<br />`{Array} routes` - Массив [роутов](#route).
___

#### <a name="buildURL" />{String} Router#buildURL(name [, params]) ####
Генерирует URL для роута с именем `name` и параметрами `params`.

**Параметры:**
<br />`{String} name` - Имя [роута](#route).
<br />`{String} params` - GET-параметры, с которыми будет сгенерирован URL на основе паттерна.
___
