# Написание тестов

Gemini может использовать те же PageObject-ы что и hermione, но без их автоматического поиска, надо подключать вручную. Из PageObject-ов пока используются только статические селекторы - в gemini пока нет нужных методов для поиска внутри выбранного элемента.

## Работа с браузером и подготовительные действия

Gemini работает с браузером по упрощённому протоколу. Команды создаются и передаются в очередь webdriver-а вручную. Сложность в том что доступны не все команды, и нет возможности нормально дожидаться окончания действий браузера. Стандартный порядок взаимодействия выглядит так: передаём пачку команд и ждём пока появится элемент, который мы хотим заскриншотить. Это немного ограничивает нас во взаимодействии с интерактивными элементами типа `annexSelect`/`annexSuggest`.

* [Руководство по написанию тестов](https://gemini-testing.github.io)

* [Доступные команды webdriver-а](https://gemini-testing.github.io/doc/tests.html#available-actions)
