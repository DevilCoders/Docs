## SWAGGER

Путь:

1. [Локальный запуск](http://localhost:8080/swagger-ui/index.html).
2. [Тестинг](http://adv-shop-integration.tst.vs.market.yandex.net/swagger-ui/index.html)
   (нужно создать правила в [puncher](https://puncher.yandex-team.ru), если еще нет)
3. [Прод](http://adv-shop-integration.vs.market.yandex.net/swagger-ui/index.html)
   (нужно создать правила в [puncher](https://puncher.yandex-team.ru), если еще нет)

## Локальные тесты

Чтобы тесты запускались локально, необходимо указать
в ```Edit Configurations... -> Edit configuration templates... -> JUnit -> Working directory``` путь до папки, где лежит
текущий idea-project.

## Локальный запуск

Можно почитать в документации
по [Microservice Java Framework](https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/?from=%2Fmarket%2Fdevelopment%2Fdeveloper-experience%2Fmj%2F)

## Используемые сервисы

1. [Кластер БД](https://yc.yandex-team.ru/folders/fooguk0p7o84oruhmbdc/managed-postgresql?section=list)

## Все ключи ошибок, возвращаемые из сервиса

[Error Keys](https://a.yandex-team.ru/arc_vcs/market/adv/shop-integration/src/main/java/ru/yandex/market/adv/shop/integration/constant/ErrorKeys.java)
