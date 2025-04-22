# Быстрый старт

## Подготовка
1. **h2p** авторизовывает пользователей по `ssh` ключам. Для начала работы необходимо настроить ssh:
   1. Сгенерировать `ssh` ключ:

      [инструкция для macOS](https://wiki.yandex-team.ru/security/ssh/macos/#generacijaparykljuchejj)

      [инструкция для linux](https://wiki.yandex-team.ru/security/ssh/linux/#gen)

      [инструкция для windows](https://wiki.yandex-team.ru/security/ssh/windows/#generate-key-pair)
   2. Положить публичный ключ на Стафф. [Тут](https://wiki.yandex-team.ru/security/ssh/linux/#serveryscauth) подробнее написано как это сделать
   3. Добавить ключ в `ssh-agent`:

      `ssh-add -K ~/.ssh/id_rsa`

      {% note info %}

      Это необходимо делать каждый раз при перезагрузке системы! Или добавить в `.bashrc/.zshrc`

      {% endnote %}

2. [Установить утилиту `h2p`](cli.md#install)

## Запрос доступа
Для разделения доступа используется IDM и система `h2p` в нем.
Поддерживаются только сущности, описанные в [карте сервисов](../../service-map.md).

Структура ролей:
* Для доступа в сервис:

  `h2p/<service name>/<provides>`

* Для доступа в MySQL:

  `h2p/mysql/<cluster id>/<database>/(ro|rw)`

  Доступ делится на чтение (`ro`) и чтение+запись (`rw`)

* Для доступа в PostgreSQL:

  `h2p/postgresql/<cluster id>/<database>/(ro|rw)`

  Доступ делится на чтение (`ro`) и чтение+запись (`rw`)

После заказа роли необходимо дождаться ее подтверждения от ответственных. Список ответственных берется из карты сервисов.
Если вы являетесь ответственным - заявка подтвердится автоматически.

## Использование {#use}
{% list tabs %}

- Сервис

  Для доступа к сервису введите команду:

  ```shell
  h2p <service name>-<provides>
  ```
  После этого сервис будет доступен по адресу [http://localhost:3000/](http://localhost:3000/)

  #### Примеры
  * Доступ к случайному инстансу сервиса `glue` к провайдс `webhook`:

    `h2p glue-webhook`
  * Доступ к случайному инстансу сервиса `glue` к провайдс `webhook` в бранче `BRANCH-1` (Canary релиз тоже является [бранчем](../../deploy/specification/canary.md#kak-rabotaet)):

    `h2p glue-BRANCH-1-webhook`
  * Доступ к конкретному аллокейшену сервиса `glue` к провайдс `webhook`:

    `h2p glue-webhook@allocid=52dec1bc-1642-522b-ca23-9141a3fd28b4`

  [_Больше примеров_](cli.md#examples)

- MySQL

  Самый удобный способ подключения - через IDE с использованием ssh-туннеля.

  Конфигурационные файлы отправятся вам на почту при получении роли. [Подробнее](ide.md#import)

- PostgreSQL

  Самый удобный способ подключения - через IDE с использованием ssh-туннеля.

  Конфигурационные файлы отправятся вам на почту при получении роли. [Подробнее](ide.md#import)

{% endlist %}
