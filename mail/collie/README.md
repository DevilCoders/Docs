# Collie

## Описание

Бэкенд контактов. Проект в [abc](https://abc.yandex-team.ru/services/collie/). Замена [адресной книге](https://github.yandex-team.ru/abook/abook-server).
Предназначен для использования серверной частью фронтенда почты, бэкендами ПДД и Яндекс.Коннект для показа и управления контактами пользователя.
Основан на [yplatform](https://github.yandex-team.ru/yplatform/yplatform). Использует [ymod_webserver](https://github.yandex-team.ru/yplatform/ymod_webserver) для реализации HTTP-интерфейса. Сервис реализован как модуль yplatform, загрузка включается через конфиг.
Работает с данными пользователя по uid, требует аутентификации через [TVM2](https://wiki.yandex-team.ru/passport/tvm2/).
Использует асинхронный ввода/вывод, реализовано с помощью [Boost.Coroutine](https://www.boost.org/doc/libs/1_66_0/libs/coroutine/doc/html/index.html).

Презентацию про устройство бекенда контактов можно посмотреть [здесь](https://github.yandex-team.ru/pages/elsid/about_contacts).

## Сборка

### Локальная сборка

Стандартная аркадийная:
```bash
ya make mail/collie
```

### Для продакшена и других окружений

Используется задача [CREATE_MAIL_RELEASE](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/mail/CreateMailRelease) в [sandbox](https://sandbox.yandex-team.ru). Пример черновика задачи можно посмотреть [здесь](https://sandbox.yandex-team.ru/task/272972961/view).

## Запуск

### Локальный запуск

Из корня аркадии
```bash
mail/collie/bin/collie mail/collie/etc/config-local.yml
```

### Для внешних потребителей

Инсталляции для всех окружений находяся в QLOUD, проект
[mail/collie](https://platform.yandex-team.ru/projects/mail/collie).

## API

См. [github.io](https://github.yandex-team.ru/pages/ilya-sidorov/contacts/) или
[wiki](https://wiki.yandex-team.ru/users/elsid/contacts/api/).

## Тесты

### Модульные тесты

Запускаются в автоматической покоммитной сборке.
```bash
ya make -t mail/collie/tests/unit
```

Чтобы проверить покрытие кода тестами:
```bash
./ya make --gcov --coverage-report --coverage-prefix-filter mail/collie -d -t mail/collie
```
Далее находим `coverage.report/index.html` в корне аркадии и открываем в браузере.

### Интеграционные тесты

Используют devpack компонент Collie с зависимостями на Pyremock, Sharpei. abook мокается с помощью Pyremock.
```bash
ya make -tt mail/collie/tests/integration
```

## Разработка

Все изменения должны проходить через review request в [Arcanum](https://a.yandex-team.ru).

### Структура проекта

* [bin/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/bin) - сборка бинарного файла с запуском yplatform;
* [etc/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/etc) - конфигурационные файлы сервиса;
* [package/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/package) - скрипты и конфигурационные файлы; для сборки Docker-образа и пакета;
* [src/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/src) - модуль yplatform;
  * [src/logic/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/src/logic) - бизнес логика;
  * [src/server/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/src/server) - реализация HTTP-интерфейса;
  * [src/services/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/src/services) - реализация транспорта для общения с другими сервисами;
  * [src/directory_sync](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/src/directory_sync) - модуль yplatform для синхронизации с директорий (Я.Коннект);
* [tests/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/tests) - тесты;
  * [tests/integration/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/tests/integration) - интеграционные тесты;
  * [tests/unit/](https://a.yandex-team.ru/arc/trunk/arcadia/mail/collie/tests/unit) - модульные тесты;

Модульные тесты имеют такую же структуру как модуль yplatform. Все файлы тестов начинаются с префикса `test_`. Все вспомогательные файлы без такого префикса, только если это не нужно по смыслу контента.

### Именование файлов

Название должно состоять из последовательности слов в нижнем регистре, разделенных символом `_`. Для C++ расширения файлов:
`.cpp` - для исходного кода
`.hpp` - для заголовочных файлов.

### Style guide

Любое изменение должно быть в том же style guide, что и изменяемый файл. Изменение style guide файла целиком не допускается. Общие правила см. [здесь](https://wiki.yandex-team.ru/%D0%A1%D0%B5%D1%80%D0%B3%D0%B5%D0%B9%D0%A5%D0%B0%D0%BD%D0%B4%D1%80%D0%B8%D0%BA%D0%BE%D0%B2/Codestyle/).
