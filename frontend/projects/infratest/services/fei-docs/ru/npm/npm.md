# npm

Сервис развернут для хранения внутренних js пакетов разрабатываемых внутри Яндекса. Так же является зеркалом для [npmjs.com](https://www.npmjs.com/).
Сервис в ABC: [npm-repo](https://abc.yandex-team.ru/services/npm-repo/)

По вопросам поддержки пишите в форму поддержки [форму поддержки](https://wiki.yandex-team.ru/npm/support/),
предварительно поискав свой ответ в нашем [FAQ](https://doc.yandex-team.ru/si-infra/npm/faq.html)

## Синхронизация с внешним npm

Новые версии пакетов из внешнего npm становятся доступны после "карантина" – сейчас это 7 дней с момента публикации.
Подробнее в [документации](https://doc.yandex-team.ru/si-infra/npm/quarantine.html).

## Поддерживаемые операции

- publish
- install
- audit
- login (авторизация по логину из стаффа и [OAuth-токеном](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8aaf2afb26446ee99a7fab5e92057a5) в качестве пароля)
- npm owner
- npm search

##  Пример использования

 1. Конфигурирование
    ```bash
    npm config set registry https://npm.yandex-team.ru
    ```
    ```bash
    $ npm login
    Username: (yourloginhere)
    Password: (<default hidden>)
    Email: (this IS public) (yourloginhere@yandex-team.ru)
    Logged in as yourloginhere on https://npm.yandex-team.ru/.
    ```
 1. Установка пакетов если
    - сконфигурирован внутренний репозиторий:
    ```bash
    npm install [<@scope>/]<name>
    ```
    - не сконфигурирован:
    ```bash
    npm install [<@scope>/]<name> --registry https://npm.yandex-team.ru
    ```

## Аутентификация через Паспорт

Для аутентификации через Паспорт необходимо:

1. Получить [OAuth-токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8aaf2afb26446ee99a7fab5e92057a5)
2. Выполнить логин в npm, в качесте логина использовать логин со стафа, в качестве пароля - полученный OAuth-токен

## Подключение ABC-групп

Сервис умеет работать с правами на основе ABC-групп, почитать можно в [документации](https://doc.yandex-team.ru/si-infra/npm/abc.html)

## Выдача прав через IDM и права на скоупы

Сервис интегрирован с IDM и через IDM поддерживает управление правами, в том числе, и на скоупы, подробнее в [документации](https://doc.yandex-team.ru/si-infra/npm/idm.html)

## Поиск пакетов через UI

Для поиска мы планируем интегрироваться в intranet search, но пока идёт рзработка можно воспользоваться временным решением: [поиск](https://npm.yandex-team.ru/)

## Yadi

Сервис интегрирован с [Yadi](https://wiki.yandex-team.ru/product-security/yadi/). Подробнее в [документации](https://doc.yandex-team.ru/si-infra/npm/yadi.html).
