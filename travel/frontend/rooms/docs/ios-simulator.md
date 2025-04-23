# Cимулятор iOS

### Чем полезно

Это не эмуляция, а реальный тач iOS с его реальными багами и проблемами.

### Как поставить

#### Запуск эмулятора

1. Установить Xcode (AppStore)
2. Запустить Xcode -> Xcode -> Preferences -> добавить версий iOS какие-надо
3. Xcode -> Open developer tools -> Simulator -> Добавить в панель быстрого доступа, чтобы не выбирать каждый раз
4. Установить [сертификат](https://crls.yandex.net/YandexInternalRootCA.crt), drag-n-drop'ом на симулятор телефона (работает не стабильно, у меня почему-то только с IPhone 11 получилось)

#### Подключение Safari

**порядок важен!**

1. Открыть Safari на IPhone
2. Открыть страницу для дебага
3. Запускаем safari на маке, если запустить Сафари раньше, то подключение к симулятору не заработает
4. Выбираем в панели наверху Разработка -> Имя симулятора -> Страница в симуляторе в safari

Что есть? Devtools есть и так с ним всё понятно.

#### Подключить реальный iPhone по проводу

[Инструкция по подключению](https://medium.com/better-programming/debugging-your-iphone-mobile-web-app-using-safari-development-tools-71240657c487)

Потом при подключении или в настройках указать, что доверяем этому макбуку.

А дальше тот же алгоритм, только открываем страницу не в браузере, а в safari на телефоне.

### Ссылки

-   [Тестирование вёрстки в iOS](wiki.yandex-team.ru/search-interfaces/infra/infratest/hermione-ios-safari/)
-   [Сертификат](wiki.yandex-team.ru/search-interfaces/infra/infratest/hermione-ios-safari/#kakustanovitvnutrennijjsertifikatvsimuljatore)
