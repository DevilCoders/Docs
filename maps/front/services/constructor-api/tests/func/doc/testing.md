# Тестирование Виджета Конструктора
[Дока](https://yandex.ru/support/maps-builder/concept/markers_2.html#markers_2__map_interactiv)

## Когда нужно тестировать
- фиксы, любые изменения в самом Виджете
- тестируется новая версия АПИ и готовится к релизу. После переключения **2.1** в тестинге на новую версию нужно проверить Виджет (не забыть изменить `apiVersion` в [pageObject](../pageObject.js))
- изменения в [constructor-int](https://github.yandex-team.ru/maps/constructor-int) (также проверить [статические карты](https://yandex.ru/support/maps-builder/concept/markers_2.html#markers_2__map_static))
- изменения в других бэкендах, связанных с Виджетом

## Как тестировать
1. Запустить автотесты, подробнее [здесь](../README.md)
2. При необходимости проверить [вручную](../../manual/index.html)