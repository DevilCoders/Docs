# Sheltie

## Описание

Бэкенд для импорта и экспорта контактов. Проект в [abc](https://abc.yandex-team.ru/services/sheltie/). Замена ручек /compat/colabook_import.json и /compat/colabook_export [адресной книге](https://github.yandex-team.ru/abook/abook-server).
Предназначен для использования серверной частью фронтенда почты и бекенда календаря
Основан на [yplatform](https://github.yandex-team.ru/yplatform/yplatform). Использует [ymod_webserver](https://github.yandex-team.ru/yplatform/ymod_webserver) для реализации HTTP-интерфейса. Сервис реализован как модуль yplatform, загрузка включается через конфиг.
Работает с данными пользователя по uid, требует аутентификации через [TVM2](https://wiki.yandex-team.ru/passport/tvm2/).
Использует асинхронный ввода/вывод, реализовано с помощью [Boost.Coroutine](https://www.boost.org/doc/libs/1_66_0/libs/coroutine/doc/html/index.html).

## Сборка

### Локальная сборка

Стандартная аркадийная:
```bash
ya make mail/sheltie
```

### Для внешних потребителей

Инсталляции для всех окружений находяся в QLOUD, проект
[mail/sheltie](https://platform.yandex-team.ru/projects/mail/sheltie).

## API

[wiki](https://wiki.yandex-team.ru/Pochta/abook/api/mail).
ручки
```
/compat/colabook_import.json
/compat/colabook_export
```

## Тесты

### Модульные тесты

Запускаются в автоматической покоммитной сборке.
```bash
ya make -t mail/sheltie/tests/unit
```

Чтобы проверить покрытие кода тестами:
```bash
./ya make --gcov --coverage-report --coverage-prefix-filter mail/sheltie -d -t mail/sheltie
```
Далее находим `coverage.report/index.html` в корне аркадии и открываем в браузере.

### Интеграционные тесты

Используют devpack компонент Sheltie с зависимостями на Pyremock. abook мокается с помощью Pyremock.
```bash
ya make -tt mail/sheltie/tests/integration
```

## Разработка

Все изменения должны проходить через review request в [Arcanum](https://a.yandex-team.ru).

### Структура проекта

* [bin/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sheltie/bin) - сборка бинарного файла с запуском yplatform;
* [etc/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sheltie/etc) - конфигурационные файлы сервиса;
* [package/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sheltie/package) - скрипты и конфигурационные файлы; для сборки Docker-образа и пакета;
* [src/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sheltie/src) - модуль yplatform;
* [tests/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sheltie/tests) - тесты;
  * [tests/integration/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sheltie/tests/integration) - интеграционные тесты;
  * [tests/unit/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/sheltie/tests/unit) - модульные тесты;
