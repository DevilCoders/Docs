# Сервисы монорепо

В этой папке находится код, который использует возможности `lerna` и `npm` для управления жизненным циклом, но конечным
продуктом является не `npm`-пакет, а не некий (микро)сервис.

Все подпапки оформлены пакетами с `private=true`. При этом `lerna` за ними следит, ставит `git`-теги и пушит их, но не
публикует эти "пакеты" в `npm`.
Мы используем `npm`, чтобы фиксировать зависимости, прогонять интеграционные тесты (в том числе в рамках `lerna`),
писать `build`-скрипты.
