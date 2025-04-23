# Автотесты на Public API - будущая единая точка входа в бэкенд со всех фронтов и аппов

[Swagger](http://autoru-api-server.vrts-slb.test.vertis.yandex.net/docs)

```
public-api-client
public-api-tests
```

## Документация

### Как мы пишем тесты и что проверяем

https://wiki.yandex-team.ru/vertis/vsdealers/autoru-api-regress-tests/

### Генерация тестов

[Как генерить тесты из swagger](docs/generate_tests.md)

### Lombok

Проект использует [lombok](https://projectlombok.org/).


## Как запустить проект локально

1. Собрать проект: `mvn clean install -DskipTests`
2. Запустить все тесты: `mvn -pl public-api-tests surefire:test`
3. Запустить все тесты из класса: `mvn -pl public-api-tests surefire:test -D'test=TestClassName'`
4. Запустить все тесты из пакета: `mvn -pl public-api-tests surefire:test -D'include.packages=ru/auto/tests/publicapi/garage/*'`


## Разработка в IntelliJ IDEA

1. Импортируем проект в IDEA и синхронизируем maven (Reload All Maven Projects)
2. Для старых версий IDEA (до 2020.3) - устанавливаем в IDEA [плагин Lombok](https://plugins.jetbrains.com/plugin/6317-lombok)
3. PROFIT. А если нет - приходи к [@timondl](https://staff.yandex-team.ru/timondl)

Для macOS может потребоваться отключить AirDrop:

```
sudo ifconfig awdl0 down
networksetup -setv6automatic Wi-Fi
```

### Max file size

Открываем **Help > Edit Custom Properties**, добавляем:
```
idea.max.intellisense.filesize=3000
```
