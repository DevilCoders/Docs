# Структура

Каждый файл (манифест) представляет собой набор точечных прав (разрешений) для каждого из сервисов.
Исключение — файл `user-groups.json`. В нём хранятся групповые роли — наборы точечных прав, объединённых рабочими сценариями.

Манифесты имеют древовидную структуру, со вложенностями.
<b>Немного магии</b>: В каждый конечный узел дерева ролей, при экспорте ролей в IDM, инъектится дополнительная роль - `OWNER`.
Эта роль особенна тем, что:
1) Даёт её владельцу разрешения всех соседних с ней ролей (находящихся на том же уровне вложенности).
2) Участвует в workflow IDM-а, давая возможность владельцу подтверджать выдачу соседних с ней ролей.

Дерево ролей выглядит как 
`Сервисы -- Модели -- Роли`

## Сервис
* name - Имя сервиса
* help - Описание сервиса
* featureLocale - Локаль возможностей
* models - `{ [MODELID]: <Model>, ... }` список возможностей

## Модель
* name - Имя возможности
* help - Описание возможности
* ownerLocale - Имя роли `OWNER`
* ownerHelpLocale - Описание роли `OWNER`
* roles - `{ [ROLEID]: <Role>, ... }` список ролей
* params - `{ [PARAMNAME]: <param1>, ... }` список доп. параметров ролей (можно указывать при запросе роли)

## Роль
* name - Имя роли
* help - Описание роли
* includeRoles - `[ 'rolePath', ... ]` список связанных rolePath ролей

## Пример:
```json
{
    "name": "Сервис выдачи промокодов",
    "help": "",
    "models": {
        "FEATURE": {
            "name": "Промокоды",
            "help": "",
            "roles": {
                "READ": {
                    "name": "Просмотр",
                    "help": ""
                },
                "MANAGE": {
                    "name": "Управление",
                    "help": "Добавление, изменение, удаление"
                }
            },
            "params": {
                "productName": {
                    "name": "Название продукта, в рамках которого будут выдаваться промокоды",
                    "type": "charfield",
                    "required": true
                }
            }
        }
    }
}
```
