# Вкладка редактирования дерева ТН ВЭД
[ссылка](https://mdm.market.yandex-team.ru/mdm/tnved-categories)

## Описание
Вкладка используется для просмотра и редактирования дерева ТН ВЭД

## Редактирование узла, листа дереве
Основные поля:
- **Тип** - может быть двух видов: ```CODE``` - сам код ТН ВЭД, который используется в бизнес логике, ```GROUP```- группа, служит для структуризации дерева и улучшения навигации по нему, в бизнес-логике не используется
- **Префикс ТН ВЭД** - задается только для ```CODE```, название говорит само за себя

## Особенность работы
При изменении и добавлении узлов типа ```CODE``` может быть запущен перерасчет МСКУ. На перерасчет идут все МСКУ, на категории которых выставлен префикс ТН ВЭД, который является префиксом измененного/добавленного кода.
