# Бекенд скачивания и обновления

## Разработка:

Установить зависимости:

```
npm ci
```

Запуск девелопер-сервера:

- для внешнего сервера

```
npm run dev
```

- для внутреннего сервера

```
INTERNAL=1 npm run dev
```

## Сборка:

Производится из скрипта сборка докер-образа.

Руками можно собрать просто из ```npm run build```

В Trendbox CI сборка происходит автоматически, при наличии изменений:

- из пул реквестов - registry.yandex.net/messenger-frontend/distibution-server:vX.X.X-pull-NNNN
- из дева - registry.yandex.net/messenger-frontend/distibution-server:vX.X.X-dev-YYYYYYYY
- ~~из релиза чатов - registry.yandex.net/messenger-frontend/distibution-server:vX.X.X~~

## Деплой

Происходит автоматически из trendbox CI

- ~~из пул реквестов - в test~~
- ~~из дева - в test и dev~~
- ~~из релиза - в prod~~

Окружения:

|  | Внутреняя | Внешняя |
| --- | --- | --- |
| Test | [Qloud](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-test) [Logs](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-test?tab=logs-beta) [Dashboard](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-test?tab=dashboard) | [Qloud](https://platform.yandex-team.ru/projects/mssngr/download-front/external-test) [Logs](https://platform.yandex-team.ru/projects/mssngr/download-front/external-test?tab=logs-beta) [Dashboard](https://platform.yandex-team.ru/projects/mssngr/download-front/external-test?tab=dashboard) |
| Dev | [Qloud](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-dev) [Logs](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-dev?tab=logs-beta) [Dashboard](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-dev?tab=dashboard) | [Qloud](https://platform.yandex-team.ru/projects/mssngr/download-front/external-dev) [Logs](https://platform.yandex-team.ru/projects/mssngr/download-front/external-dev?tab=logs-beta) [Dashboard](https://platform.yandex-team.ru/projects/mssngr/download-front/external-dev?tab=dashboard) |
| Prod | [Qloud](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-prod) [Logs](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-prod?tab=logs-beta) [Dashboard](https://platform.yandex-team.ru/projects/mssngr/download-front/internal-prod?tab=dashboard) | [Qloud](https://platform.yandex-team.ru/projects/mssngr/download-front/external-prod) [Logs](https://platform.yandex-team.ru/projects/mssngr/download-front/external-prod?tab=logs-beta) [Dashboard](https://platform.yandex-team.ru/projects/mssngr/download-front/external-prod?tab=dashboard) |

### Домены и сети:

Сети и балансеры:

- [MSSNGR_NETS](https://platform.yandex-team.ru/networks/MSSNGR_NETS?tab=permissions) - Продовая сеть, для конфигов, которые работают с продовыми паспортами и сервисами (dev, alpha, prod)
    - [mssngr-front](https://platform.yandex-team.ru/l7/mssngr-front) - Внешний продовый балансерв, для продов
    - [mssngr-front-internal](https://platform.yandex-team.ru/l7/mssngr-front-internal) - Внутренний продовый балансер, для dev и alpha окружений
- [MSSNGR_TEST_NETS](https://platform.yandex-team.ru/networks/MSSNGR_TEST_NETS?tab=permissions) - Тестовая сеть, для конфигов, которые работают с тестовыми паспортами и сервисами (test)
    - [mssngr-front-test](https://platform.yandex-team.ru/l7/mssngr-front-test) - Внутренний тестовый балансер, для test окружений

|  | Внутреняя | Внешняя |
| --- | --- | --- |
| Test | https://download.messenger.test.yandex-team.ru/desktop/ <br>MSSNGR_TEST_NETS, mssngr-front-test, INTERNAL | https://download.messenger.test.yandex.ru/desktop/ <br>MSSNGR_TEST_NETS, mssngr-front-test, INTERNAL |
| Dev | https://download.messenger.dev.yandex-team.ru/desktop/ <br>MSSNGR_NETS, mssngr-front-internal, INTERNAL | https://download.messenger.dev.yandex.ru/desktop/ <br>MSSNGR_NETS, mssngr-front-internal, INTERNAL |
| Prod | https://download.messenger.yandex-team.ru/desktop/ <br>MSSNGR_NETS, mssngr-front, EXTERNAL | https://download.messenger.yandex.ru/desktop/ <br>MSSNGR_NETS, mssngr-front, EXTERNAL |

### Текущие версии:

| Окружение | Внутреняя | Внешняя |
| --- | --- | --- |
| Test | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-test/updater/version.svg) | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-test/updater/version.svg) |
| Dev | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-dev/updater/version.svg) | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-dev/updater/version.svg) |
| Prod | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-prod/updater/version.svg) | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-prod/updater/version.svg) |

### Проверка переменных окружения:

| Окружение | Внутреняя | Внешняя |
| --- | --- | --- |
| Test | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-test/updater/env/NODE_ENV.svg) ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-test/updater/env/INTERNAL.svg) | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-test/updater/env/NODE_ENV.svg) ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-test/updater/env/INTERNAL.svg) |
| Dev | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-dev/updater/env/NODE_ENV.svg) ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-dev/updater/env/INTERNAL.svg) | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-dev/updater/env/NODE_ENV.svg) ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-dev/updater/env/INTERNAL.svg) |
| Prod | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-prod/updater/env/NODE_ENV.svg) ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/internal-prod/updater/env/INTERNAL.svg) | ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-prod/updater/env/NODE_ENV.svg) ![](https://badger.yandex-team.ru/qloud/mssngr/download-front/external-prod/updater/env/INTERNAL.svg) |
