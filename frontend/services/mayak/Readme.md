# Яндекс.Маяк

### Быстрый старт

-   устанавливаем зависимости:

    ```sh
    $ npm i
    ```

-   Настраиваем `tvm` для локальной разработки:

    `TVM_SECRET` можно посмотреть [тут](https://abc.yandex-team.ru/services/mayak/resources/?show-resource=18026471). Если нет доступа к секрету, то обратитесь к TVM менеджерам проекта.

    ```sh
    $ TVM_SECRET=<tvm_secret> npm run tvm:init
    ```

    Больше подробностей о работе пакета можно посмотреть в документации [@yandex-int/express-tvm](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/express-tvm)

-   запускаем проект:

    ```sh
    $ npm start
    ```

    Обратите внимание, что нужно авторизироваться в тестинге паспорта.

### Деплой приложения:

#### Начало работы с `Docker`:

-   Единожды нужно получить токен для авторизации [тут](https://wiki.yandex-team.ru/docker-registry/#authorization)
-   Иметь на машине установленный `docker`

-   Выполнить команду авторизации в `registry.yandex.net`, которая создаст файл `~/.docker/config.json`:

    ```sh
    $ docker login -u <ТВОЙ_ЛОГИН_НА_СТАФФ> -p <ТОКЕН> registry.yandex.net
    ```

#### Релиз нового `docker` образа:
Сделать коммит с новой версией проекта в package.json

```sh
$ npm run docker-publish-release
```

Результат выполнения операций - новый образ по адресу `registry.yandex.net/mm-interfaces/mayak/<package.json version>`

#### Замена `docker` образа в конфиге YD

[тестинг](https://deploy.yandex-team.ru/project/mayak-testing)/[прод](https://deploy.yandex-team.ru/project/mayak-production)

### Ссылки на приложение:

[тестинг](https://tst.mayak.yandex.ru/)/[прод](https://mayak.yandex.ru/)

### Unit тестирование

[jest docs](https://jestjs.io/docs/en/api)

-   запустить все тесты:

    ```sh
    $ npm run unit
    ```

-   обновить `snapshots`:

    ```sh
    $ npm run unit -u
    ```

-   запустить конкретный тест/папку с тестами:

    ```sh
    $ npm run unit ./path/to/test
    ```

### Настройка мониторингов (Monitorado)

Документация по [monitorado](https://github.yandex-team.ru/toolbox/monitorado)

#### Быстрый старт:

1.  Устанавливаем зависимости:

    ```sh
    $ npm i -g @yandex-int/monitorado --registry=https://npm.yandex-team.ru
    ```

2.  переходим в папку с конфигом `monitorado`:

    ```sh
    $ cd ./.config/monitorado
    ```

3)  [Получаем токен](https://github.yandex-team.ru/toolbox/monitorado#%D0%A2%D0%BE%D0%BA%D0%B5%D0%BD%D1%8B) и кладем в файл `.env`

4)  Смотрим diff:

    ```sh
    $ monitorado diff -v
    ```

5)  Обновляем конфиг:

    ```sh
    $ monitorado exec -v
    ```

### Hermione

-   [official docs](https://github.com/gemini-testing/hermione#prerequisites)
-   [search-interfaces docs](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/#faq)
-   [webdriver api docs](https://webdriver.io/docs/api.html)

#### запуск тестов

переменной окружений `NODE_ENV` можно выставить среду, в которой будут проходить тесты

```sh
% npm run hermione
```

#### Локальная разработка/запуск

Для локальной разработки потребуется локальный [grid](https://github.yandex-team.ru/mm-interfaces/samadhi#local-grid)

```sh
# терминал 1
$ selenium-standalone start
# терминал 2
% npm start
# терминал 3
% npm run hermione:local
```
