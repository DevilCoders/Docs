# Разработка в Паспорте

## Quick Start

1. Установите `python`
2. Установите [arc](https://doc.yandex-team.ru/arc/setup/arc/install.html) или `subversion`


### Arc

* `(opt)` Поднимите софт и хард лимиты на файлы.
  * `(Ubuntu)`: В `/etc/systemd/user.conf` и `/etc/systemd/system.conf` добавьте:
      ```bash
      DefaultLimitNOFILE=65535
      ```
      В `/etc/security/limits.conf`:
      ```
      * hard nofile 65535
      * soft nofile 65535
      ```
      и перезагрузитесь.
* Установите Fuse
  * `(Ubuntu)`: `sudo apt-get install fuse`
  * `(Mac OS)`: `brew cask install osxfuse` или https://osxfuse.github.io/
* Создайте директори для монтирования каталога Аркадии `mkdir -p arc && cd arc`
* Создайте директории для кода и метаданных `mkdir -p arcadia store`
* Используйте `arc` (из шага 2) для монтирования: `nice arc mount -m arcadia/ -S store/`

[Официальная документация Arc](https://wiki.yandex-team.ru/arcadia/arc/docs/setup/)

### SVN

* Счекаутите папку с паспортным кодом

    `svn cat svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/ya | python - clone`

    `cd arcadia`

    `./ya make -j0 --checkout passport/backend`

## Список проектов

* [adm_api](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/adm_api) - апи паспортной админки
* [api](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/api) - основное паспортное API
* [ch_stat_loader](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/ch_stat_loader) - утилита, считающая в clickhouse и заливающая на stat разные отчеты по логам аккаунт менеджера
* [ci](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/ci) - инструмент для поддержки разработки (форматирование кода, релиз пакетов)
* [clients](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/clients) - паспортные клиенты ко внешним сервисам
* [configs](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/configs) - паспортные конфиги для мониторингов
* [contrib](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/contrib) - внешние библиотеки, необходимые для работы паспортных приложений
* [core](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/core) - библиотека с основной функциональностью паспортного API
* [dbscripts](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/dbscripts) - регулярные задачи в паспортной БД
* [dev_env](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/dev_env) - набор утилит для запуска автотестов над рабочей копией passport-api в деве
* [grants_configurator](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/grants_configurator) - Грантушка
* [library](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/library) - набор переиспользуемых компонент
* [libs_checker](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/libs_checker) - утилита для тестирования файлов данных библиотек (например, Геобазы)
* [logbroker_client](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/logbroker_client) - клиенты логброкера, используемые для транспорта данных паспорта
* [luigid](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/luigid) - демон luigid для запуска периодических задач
* [mobileproxy_nginx](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/mobileproxy_nginx) - nginx-конфиги для мобильного прокси
* [oauth](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/oauth) - OAuth-сервер
* [passport_nginx_config](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/passport_nginx_config) - nginx-конфиги для паспорта и МДА 2.0
* [passport_stress_fake_services](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/passport_stress_fake_services) - моки-заглушки для нагрузочных стрельб Паспорта
* [perimeter](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/perimeter) - сервис для аутентификации пользователей в yandex-team
* [perimeter_api](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/perimeter_api) - апи для управления способами аутентификации в yandex-team
* [pocket_service](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/pocket_service) - обработчик вебхуков для автоматизации процессов CI
* [profile](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/profile) - приложение рассчета паспортного профиля
* [py_adm](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/py_adm) - питоновая админка
* [qa](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/qa) - TUS и автотесты
* [qa_proxy](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/qa_proxy) - прокси к паспортным сервисам, в который ходят автотесты
* [scim_api](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/scim_api) - апи SCIM для федераций
* [social](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/social) - Социализм
* [takeout](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/takeout) - приложение выемки данных по пользователям
* [tasklets](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/tasklets) - код тасклетов для [аркадийного CI](https://docs.yandex-team.ru/ci/)
* [tools](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/tools) - утилиты для выполнения различных adhoc задач
* [tvm_keyring](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/tvm_keyring) - демон автоматического получения TVM2.0 тикетов
* [uaas_proxy](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/uaas_proxy) - прокси для сервиса экспериментов
* [utils](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/utils) - паспортный утиль
* [vault](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/vault) - секретница
* [yapic2](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/yapic2) - сервис для заливки изображений (например, QR-кодов) в MDS

## Общие правила разработки

* Используйте бранчи для разработки либо несколько рабочих директорий SVN.
Бранчи должны иметь имя вида `users/<your_login>/<branch_name>`, например `users/ppodolsky/passp-23051`
* Запускайте [CI Tool](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/ci) перед коммитом
* Группируйте все связанные изменения в один коммит
* Шлите изменения пулл-реквестом, а не прямым коммитом/пушем.
    ```
    ya pr create -m 'Описание изменения'
    ya pr update
    ```
* Читайте проектные `README.md`. Для некоторых проектов или компонент могут быть более строгие требования (например `library/`, `api/`, `core/` или `utils/`)
* Используйте говорящие имена для тестов. Добавляйте комментарии, если тест сложный.
* Тяжелые операции выполняйте при запуске приложения, а не в процессе работы
* Покрывайте тестами как можно большее количество кода
* Комментируйте замеченные недостатки кода с помощью комметариев `ToDo`
* Исправляйте найденные баги. Даже если они посажены не вами.
* Будьте терпеливы

## Styleguide

* Используйте [PEP8](https://www.python.org/dev/peps/pep-0008/),
[PEP257](https://www.python.org/dev/peps/pep-0257/),
[CI Tool](https://a.yandex-team.ru/arc/trunk/arcadia/passport/backend/ci)
и наш стайлгайд
* Логируйте, используя наш [стайлгайд логирования](https://wiki.yandex-team.ru/passport/log-style-guide/)
* Каждый элемент коллекции помещайте на отдельную строку и используйте замыкающие запятые
    ```
    {
        'hello': 'Hello!',
        'world': 'World',
        'inner: {
            'embedded': 'value',
        },
    }

    dict(
        hello='world',
        world='hello',
    )

    my_brand_new_very_long_list_name = [
        'first_item_of_my_list_with_very_long_name',
        'second_item_of_my_list_with_very_long_name',
        'third_pretty_long_item',
    ]
    ```
* Используйте одинарные кавычки для строк
* `X if Y else Z` лучше, чем `X and Y or Z`
* Пишите докстринги без префикса `u`
* Чем короче ваш код, тем лучше. Например `return` лучше чем `return None`

## Споры и ассимиляция опыта коллег

Если обсуждение кода с коллегой зашло в тупик, обратитесь к третьей стороне, например к kmerenkov@

Наиболее важные вопросы не стеснйтесь задавать вслух всем коллегам

Вопросы про общеяндексовые компоненты направляйте в [Аркадийный чат](https://t.me/joinchat/IF7OZUZhbWQqmfezfqrjVw)

## Полезные ссылки

### Общее

* [Вики-страница Паспорта](https://wiki.yandex-team.ru/passport/)

### Техническое

* Стрельба в Паспорт: [код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/passport/regression_shooting) и [задача](https://sandbox.yandex-team.ru/task/386720456/view)
* Стрельба в Секретницу: [код](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/passport/vault_shooting)
