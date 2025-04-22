# Yandex Pay Common Library

Общая библиотека проекта [YandexPay](https://abc.yandex-team.ru/services/yandexpay)

### Тестирование

1. `make build-tests`
2. `make dev-tests`

### Инварианты зависимостей

Не нарушайте слоистую архитектуру и не делайте ссылок из нижних слоев в верхние. Порядок (от верхнего к нижнему):
1. `interactions`
2. `schemas`
3. `entities`
