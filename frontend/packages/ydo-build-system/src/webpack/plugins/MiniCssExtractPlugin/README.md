### Что это
Форк плагина (`dist` папка опубликованного пакета) https://github.com/webpack-contrib/mini-css-extract-plugin версии v2.4.4 с возможностью задать порядок вставки css ассетов в бандл

### Зачем
Чтобы правила из проекта всегда шли после стилей из зависимостей - для переопределения стилей лего компонентов через модификаторы классов. По умолчанию используется порядок импорта.   
В аркадии уже есть форк первой версии - https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/mini-css-extract-plugin, но он не работает с 5 вебпаком.

### Что изменено
1. В функцию `sortModules` добавлена возможность задать функцию сортировки через опцию плагина `modulesSortFn`
2. Убрана валидация и описание параметров для плагина и лоадера через json схему


