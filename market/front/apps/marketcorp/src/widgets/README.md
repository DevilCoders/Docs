# Виджеты

## Описание директорий
* `core/` -- базовые виджеты, не относящиеся к контенту, либо слишком общие.
* `content/` -- виджеты для отображения контента.
* `layouts/` -- виджеты для распределения виджетов по странице, обычно параметризуются другими виджетами.
* `pages/` -- страничные виджеты, имеют суффикс `Page`. Доступ к странице желательно оставлять на этом уровне.
* `parts/` -- целые куски для встраивания в страницы, различные хабы и т.д. Тоже имеют доступ к страничной информации.

## Преобразование квазивиджетов в виджеты
Модули, содержащиеся в `platform.dektop/widgets` будем называть квазивиджетами, так как идеологически они довольно близки к виджетам.

Последовательность шагов для преобразования существующих квазивиджетов в виджеты:
1. `index.js` превращается в `controller.js`.
2. В `controller.js` предоставляется альтернативный экспорт (`legacy`) для работы в квазивиджетом окружении.
3. Меняем в месте использования (квазивиджетном окружении) реквайр на новый (`legacy`).
4. В `controller.js` в качестве дефолтного экспорта делаем контроллер виджета.
5. В `index.js` описываем (`Widget.describe`) наш виджет, включая в него всё необходимое.
6. Если нужно, то, используя `@yandex-market/cia`, обернуть в зону/сенсор в `view.js`.
7. Для старой вьюхи предоставляется альтернативный экспорт (`legacy`).

Для примера можно посмотреть уже переведённые виджеты в `content/`.
