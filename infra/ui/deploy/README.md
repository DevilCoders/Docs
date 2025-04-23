# Yandex Deploy UI

UI для сервиса Yandex Deploy.

Представляет из себя SPA на React.js.
Написан на typescript, имеет старую часть old-code на javascript.

## Быстрый старт

Каждый из модулей можно запускать и отдельно, разумеется. Но если хочется по-быстрому, то можно так:

### Подготовка

Закажите себе сертификат на [crt.yandex-team.ru](https://crt.yandex-team.ru/certificates) c параметрами

- CA name: `InternalCA`
- Тип сертификата: `Для web-сервера`
- Хосты: `localhost.yandex-team.ru`
- ABC-сервис: `Интерфейсы инфраструктурного облака`

На почту придет ссылка в секретницу. Положите значние секрета `***_certificate` в `configs/localhost.yandex-team.ru.crt`, а `***_private_key` в `configs/localhost.yandex-team.ru.key`.

Добавьте в файл `/private/etc/hosts` строку:

```sh
127.0.0.1 localhost.yandex-team.ru
```

### Установка

Переключение версий node и npm:

Версия nodejs закреплена в `.nvmrc`, чтобы переключится на неё, выполните
```sh
nvm use
```
Подробнее о [nvm](https://github.com/nvm-sh/nvm)


Установка всех `node_modules`:

```sh
make install
```

### Запуск

Запуск dev-сервера для ui:

```sh
make start
```

Для локальной разработки используйте переменную окружения `CONFIG_PRESET` (подробнее ниже):

```sh
CONFIG_PRESET=ext-local make start
```

Запуск всего на свете (ui, test, storybook):

```sh
make start_all -j3
```

*`-j3` запускает три потока*

### По необходимости

Запуск тестов:

```sh
make test
```

Запуск storybook:

```sh
make storybook
```

## Структура проекта

### /configs/

На данный момент содержит в папке `presets` json-конфиги со значениями для разных окружений. Выбрать окружение можно, задав переменную `CONFIG_PRESET`. Если `CONFIG_PRESET` не задан, то будет использоваться прод-окружение `ext-prod`. Для локальной разработки необхдимо использовать `ext-local`.

Эти конфиги используется для UI (вгенериваются в index.html на этапе запуска или сборки).

Также внутрь этой папки нужно положить сертификат (см. выше "Подготовка"). Он используется для UI (дев-сервера).

Подробнее в [README.md](./configs/README.md) в этой папке.


### /cypress/

Новые E2E тесты сервиса. Тестируют UI и всё, что из него можно сделать, через браузер.

Тесты написаны для фреймворка [Cypress](https://docs.cypress.io/guides/overview/why-cypress).

Подробнее в [README.md](./cypress/README.md) в этой папке.


### /tests/

Старые E2E тесты сервиса.

Тесты написаны для фреймворка [TestCafe](https://devexpress.github.io/testcafe/documentation/getting-started/).

Подробнее в [README.md](./tests/README.md) в этой папке.

Новые тесты сюда не пишем, только изменяем в случае верстки селекторы.

### /ui/

Собственно сам UI и есть. Стандартное CRA приложение на TypeScript.

Также проинтегрирован Storybook для изолированной разработки, визуального тестирования и документирования компонентов.

Подробнее в [README.md](./ui/README.md) в этой папке.

## Для команды бэкенда

### Роли
Добавить новую роль для системы ролей деплоя можно декларативно в файле `ui/src/models/roles.json`

В поле `roles` добавьте роль с полями вида
```json
"owner": {
   "id": "owner",
   "idmId": "OWNER",
   "title": "Owner",
   "description": "Maintainer rights + delete project + role confirmation"
}
```
Затем в поле `rolesByObject` добавьте эту роль к тем объектам, где она есть: project/stage/box
```json
"rolesByObject": {
      "project": [
         {
            "id": "owner"
         },
         {
            "id": "maintainer"
         },
         // ...
         {
            "id": "<id роли, которую вы добавили>"
         }
      ],
      // ...
```
