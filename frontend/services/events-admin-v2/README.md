# events-admin-v2

## Подготовка

Для работы потребуется Node.js 12.

Для начала [устанавливаем Brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/). Затем:

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12 версии
nvm install 12.18.1
```

## Установка и запуск

```bash
# Устанавливаем зависимости
npm run deps

# Запускаем приложение (magicdev запросит ваш пароль, чтобы запустить его на 443 порту).
# По необходимости, вы может задать другой порт, не требующий sudo, в файле .magicdev.json.
npm run dev
```

Проект становится доступен по адресу:
https://localhost.msup.yandex.ru/


## Запуск с локальным API
Api находится в репозитории [montserrat/events-api](https://github.yandex-team.ru/montserrat/events-api)

Запуск API
- Прочитать инструкцию по запуску Админки.
- Запуск с локальной базой `OFF_AUTH=true NODE_ENV=local POSTGRES_URI=postgres://events:events@localhost:5436/events-api PORT=8082 npm run dev`
- Если нет доступа, то необходимо выполнить инсерт в локальную базу `insert into user_roles values ('saaaaaaaaasha', 'admin');`
- Для запуска с тестовой базой необходим `NODE_ENV=testing`

Запуск Админки
- В админке (https://github.yandex-team.ru/montserrat/research-admin) в `configs/default.js` (или local.js) находим и заменяем

```diff
    api: {
-		protocol: 'https',
-       host: process.env.EVENTS_API_HOST || 'events-api-testing.spec-promo.yandex.net',
+       protocol: 'http',
+       host: 'localhost:8082',
        rootPath: 'admin',
        version: 'v1'
    },
```

## Таблицы и формы сущностей
Для форм и таблиц используется модуль сущностей, который работает с json схемой.
В папке `entities/helpers/entities` хранятся хелперы для создания стандартных интерфейсов.
Для добавляения своих сущностей в стор, в корне папок-фич, требуется создать файл `entities-crud-and-schemas`,
в нем описать нужные интерфейсы по примерам существующих, и добавить их подключение в файле `app/store`.
Так же нужно не забыть добавить редьюсер в `app/reducers/index`.

## Вопросы безопасности

### Закрываем хэлсчеки от внешних пользователей

Из коробки стаб предлагает хелсчеки для отслеживания состояния необходимых смежных сервисов (например, доступность чёрного ящика, геобазы и базы данных). Пути, за которыми они скрыты, могут быть использованы для создания HTTP juggler-проверок в Qloud.

> :warning: Для того, чтобы эти пути не стали доступны внешним пользователям на публичном домене, необходимо в Qloud создать путь `/healthchecks/` и направить его в компоненту типа _http-balancer_, в параметре _Servers_ указав `http://any.yandex.ru/`.

### Делимся секретами для локальной разработки с командой

В результате генерации создан не публичный файл _.tvm.json_, который хранит настройки утилиты для раздачи TVM тикетов.

> :warning: Ни в коем случае не публикуйте этот файл в репозиторий! Для того, чтобы поделиться им с командой [заведите хранилище](https://wiki.yandex-team.ru/security/secdist/#formanazavedeniezajavki) в Secdist и [разместите его](https://wiki.yandex-team.ru/security/secdist/#rabotasobychnymifajjlamiproektnajapapka) в нём.

### Деплой
Сборка проекта осуществляется на drone

После окончания сборки нужно задеплоить ее в
[Тестинг](https://deploy.yandex-team.ru/project/events-admin-testing)
[Prod](https://deploy.yandex-team.ru/project/events_admin)

В тестинге настроена релизная интеграция.

## Доступные команды

Команда | Действие
------------ | -------------
deps | Установка зависимостей
dev | Запуск tvmtool и приложения для локальной разработки
build | Запуск production сборки скриптов и стилей
lint | Проверка TypeScript и CSS кода на codestyle
test | Запуск тестов

## Документация

* [Гайды по использованию проектов на основе Project Stub](https://wiki.yandex-team.ru/toolbox/project-stub/)
