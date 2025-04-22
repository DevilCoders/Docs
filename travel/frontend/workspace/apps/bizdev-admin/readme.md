# Биздев админка

## Предварительные требования

-   NodeJS 18
-   Docker

## Ссылки

-   Стенды
    -   [Тестовый](https://travel-bizdev-admin-testing.yandex-team.ru/)
    -   [Продакшен](https://travel-bizdev-admin.yandex-team.ru/)
-   [Yandex Deploy](https://deploy.yandex-team.ru/projects/travel-frontend-bizdev-admin)
    -   [Тестовый](https://deploy.yandex-team.ru/stages/travel-frontend-bizdev-admin-testing)
    -   [Продакшен](https://deploy.yandex-team.ru/stages/travel-frontend-bizdev-admin-production)
-   Awacs
    -   [Тестовый](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/show/)
        -   [Домен](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/domains/list/bizdev-admin-testing/show)
        -   [Upstream](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/upstreams/list/bizdev-admin-testing/show)
    -   [Продакшен - TODO](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-prod-internal-balancer/show/)
-   RackTables (внутренние сети)
    -   [Тестовый](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_TRAVEL_BIZDEV_ADMIN_TEST_NETS_)
    -   [Продовый](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_TRAVEL_BIZDEV_ADMIN_PROD_NETS_)

## Приступая к работе

### Общее

-   При монтировании укажите флаг `--allow-others` (`arc mount --allow-others arcadia`),
    это требуется для возможности использования `sudo`
-   Установите зависимости - `yarn`

### Подготовка окружения

Запускаем локальный домен и TVM. Генератор спросит токен, возьмите его
[из секретницы](https://yav.yandex-team.ru/secret/sec-01g167q9x5n929qyj0m3tzvb0b/explore/versions)

```shell
yarn g:local
```

Заводим костыльную проксю для BlackBox (потом надо попробовать получить доступ с ноута)

1. Идём в нашу машинку в [QYP](https://qyp.yandex-team.ru), оттуда нам будет нужен домен (например, your-user-dev.sas.yp-c.yandex.net)
2. Коннектимся к ней по SSH, arc mount --allow-others (может вылететь ошибка с fuse - придется патчить его конфиг - **TODO Описать**)
3. Узнаём IP нашей машины (**TODO Упростить эти пляски**), записываем его в `.env.local` (на своем компе), как `LOCAL_BLACKBOX_PROXY_USER_IP=...`
    ```shell
    $ ifconfig | grep "inet6" | grep "global"
    inet6 2a02:6b8:fc00:828f:0:4870:1c44:0  prefixlen 128  scopeid 0x0<global>
    # По идее, подходят оба, я брал второй
    inet6 2a02:6b8:c08:818f:0:4870:b3c3:0  prefixlen 128  scopeid 0x0<global>
    ```
4. На машине запускаем проксю:
    ```shell
    $ yarn g dev remote-blackbox
    domain: your-user-dev.sas.yp-c.yandex.net
    ```
5. Готово, можно выходить из машины

### Стартуем

```shell
yarn dev
```

Переходите на [https://localhost.msup.yandex-team.ru](https://localhost.msup.yandex-team.ru)
