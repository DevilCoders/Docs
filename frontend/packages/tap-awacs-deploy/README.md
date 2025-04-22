# tap-awacs-deploy

Утилита позволяет добавлять/удалять конфиги апстримов для балансера в awacs. Для похода в awacs api используется [тулза от @romanovich](https://a.yandex-team.ru/arc/trunk/arcadia/junk/romanovich/balancersupport51).


## Создание и обновление upstream

```bash
AWACS_TOKEN={TOKEN} tap-awacs-deploy deploy \
    --balancer tap-testing \
    --upstream-id search-app-editor-testing-index
    --spec-file ./.config/awacs/testing-index.yml
    --order 1000
    --param "APP_VERSION=${APP_VERSION}"
```

Параметры:

-   **balancer** – название awacs балансера. Если команда запускается в Trendbox CI, то у робота `robot-tap` должен быть доступ на редактирование балансера.
-   **upstream-id** – название апстрима, должно быть уникальное в рамках балансера для всех приложений.
-   **spec-file** – путь до файла с yaml когфигом апстрима. Поддерживается шаблонизация через параметр `param`.
-   **param** – переменная для шаблонизации yaml конфига. Можно указать несколько переменных в одной команде `--param "FOO=1" --var "BAR=2"`.
-   **order** – вес апстрима среди всех апстримов балансера.


## Удаление upstream

```bash
AWACS_TOKEN={TOKEN} tap-awacs-deploy remove \
    --balancer tap-testing \
    --upstream-id search-app-editor-testing-index
```

Параметры:

-   **balancer** – название awacs балансера. Если команда запускается в Trendbox CI, то у робота `robot-tap` должен быть доступ на редактирование балансера.
-   **upstream-id** – название апстрима, который нужно удалить.


## Получение yaml спецификации upstream

```bash
AWACS_TOKEN={TOKEN} tap-awacs-deploy get-spec \
    --balancer tap-testing \
    --upstream-id search-app-editor-testing-index
```

Параметры:

-   **balancer** – название awacs балансера. Если команда запускается в Trendbox CI, то у робота `robot-tap` должен быть доступ на редактирование балансера.
-   **upstream-id** – название апстрима.


## Получение списка upstream на балансере

```bash
AWACS_TOKEN={TOKEN} tap-awacs-deploy list-upstreams \
    --balancer tap-testing
```

Параметры:

-   **balancer** – название awacs балансера. Если команда запускается в Trendbox CI, то у робота `robot-tap` должен быть доступ на редактирование балансера.
