# Serpdocs.WebApp

Продакшен версия находится по адресу https://serpdocs.si.yandex-team.ru.
Также доступен по маске *.serpdocs.si.yandex-team.ru

Бета версия: https://beta.serpdocs.si.yandex-team.ru

## Переменные окружения
Для корректной работы приложения нужны следующие переменные окружения

* S3_KEY_ID - идентификатор ключа к S3
* S3_ACCESS_TOKEN - токен для доступа к S3
* QLOUD_OAUTH_TOKEN - OAuth токен для доступа к Qloud (деплой окружений)
* FOREVERDATA_TOKEN - OAuth токен для доступа к foreverdata (песочница)

## Быстрый старт

``` (bash)
git clone git@github.yandex-team.ru:search-interfaces/serpdocs.webapp.git
npm i
npm run build
npm run start:local
```

> Требуется локальная mongodb (см. [как настроить локальную бд](#how-to-mongo))

По умолчанию используется порт 3334. Для того, чтобы его изменить следует указать переменную окружения **NODE_PORT**

### Как настроить локальную БД <a id="how-to-mongo"></a>

**‼️ TODO**: написать. как поставить монгу и залить в нее jsdoc из web4

### Режим запуска

Задается значением переменной окружения **NODE_ENV**
Возможные значения: _local_, _development_, _production_.

| Значение **NODE_ENV** | Описание |
| ------ | ----------- |
| _local_   | локальная база и никакой минификации |
| _development_ | облачная тестовая монга и никакой минимизации |
| _production_    | облачная монга и кое-какая минимизации |

**‼️ TODO**: нужно разобраться со сборкой

## Архитектура.Сервер

Приложение на express [v4.x](http://expressjs.com/en/4x/api.html)

### Middleware

**‼️ TODO**:

### Маршрутизация

[app/routes/index.js](./app/routes/index.js)
Регистрирует и передает в контроллер зарегистрированные маршруты по соглашению.
Соглашение – каждому `pathname` ставится в соответствие пара `controller` + `action`.

**Controller**. Первый компонент `pathname` из `url` – имя контроллера, например, `/constructives` – контроллер с именем `constructives`.
Если `pathname` – корень приложения (`'/'`), то применяется контроллер по умолчанию – `constructives`.

**Action**. В `url` явно не фигурирует, но также следуюет соглашению. Метод по умолчанию – `index`. Если второй компонент `pathname` указан, то его `action` присваивается значение `show`.

**Action для ajax**. В случае ajax запроса, выбирается пара `controller` + `action` по тем же правилам, что и для остальных запросов, но к имени `action` дописывается `'Ajax'`

Примеры:

| method | url | controller | action |
| ------ | ------ | ----------- | ------ |
| GET | `/` | `constructives` | `index` |
| GET | `/abc` | `abc` | `index` |
| GET | `/ctrl1/act1` | `ctrl1` | `act1` |
| GET (ajax) | `/ctrl1/act1` | `ctrl1` | `act1Ajax` |

Значение контроллера и действия сохраняются маршрутизатором в `req.controller` и `req.action` соответственно. После чего вызывается метод `action` контроллера `controller`.

### Controller

Получает данные из модели, если требуется. Выполняет шаблонизацию, отправляет в `res` результат.

### Model

Работает с данными, ходит в mongo, FS, если требуется. Не знает ничего про запросы.

## Архитектура.Клиент

Используется последняя на текущий момент версия [Лего](https://lego.yandex-team.ru/libs/islands/v5.15.0/)
Шаблонизатор – [bh](https://github.com/bem/bh)

Сборка статики на [enb](https://github.com/enb/enb), описана в конфиге [static/.enb/makejs](/static/.enb/makejs)

В сборке нуждаются 3 основные сущности:

1. Страницы. Находятся в папке [/static/pages/](/static/pages/)
1. Частичные представления. Находятся в папке [/static/partial/](/static/partial/)
1. Переиспользуемая статика для всех страниц. Находятся в папке [/static/bundles/](/static/bundles/)

## Deploy

Приложение собирается и выкладывается в [Qloud](https://qloud.yandex-team.ru/projects/search-interfaces/serpdocs/).

* При открытии PR в qloud создаётся окружение по адресу beta-{pullRequestNumber}.serpdocs.si.yandex-team.ru. После закрытия PR окружение удаляется
* При влитии PR в мастер обновляется [бета](http://beta.serpdocs.si.yandex-team.ru)
* При выставлении тега обновляется [продакшен](http://serpdocs.si.yandex-team.ru)

#### Выставление тега

```(bash)
# обновляем package.json и коммитим с выставлением тега
$ npm version minor
# отправляем в master последний коммит и тэг
$ git push --tags
```

Как происходит обновление окружения можно посмотреть [здесь](https://github.yandex-team.ru/search-interfaces/serpdocs.webapp/blob/master/environment/deploy.js)

Удаление окружения после закрытия PR происходит в [updater](https://github.yandex-team.ru/search-interfaces/serpdocs.updater/blob/master/app/services/close_pr.js#L46)


#### Ручная сборка и публикация контейнера

```(bash)
# разработческая бета
$ make docker-publish
```

```(bash)
# общая бета
$ YENV=beta make docker-publish
```

```(bash)
# продакшн версия
$ YENV=production make docker-publish
```
