# Репозиторий с общими JS модулями службы разработки сервисов Яндекс.Лавки

-   [abc](https://abc.yandex-team.ru/services/lavkajstoolbox/)
-   [staff](https://staff.yandex-team.ru/persons/yandex_rkub_taxi_5151_8501_dep41202_dep48321_dep64819)
-   [arcanum](https://a.yandex-team.ru/projects/lavkajstoolbox)
-   [monitoring (juggler/solomon/etc)](https://monitoring.yandex-team.ru/projects/lavkajstoolbox)

---

## Требования

-   nvm или установленный в окружении Node.js 12.22.0 с npm
-   ты должен быть в группе
    [abc:lavkajstoolbox:development](https://abc.yandex-team.ru/services/lavkajstoolbox/?scope=development)

---

## Быстрый старт

-   Ставим зависимости для разработки:

    ```bash
    npm run dev:install
    ```

-   Создаем новый пакет:

    ```bash
    jstool gen-package --name MY_PACKAGE
    ```

-   Добавляем корневую внешнюю зависимость:

    ```bash
    npm i NPM_PACKAGE
    npm run postinstall
    jstool audit fix-package-lock
    ```

-   Добавляем корневую зависимость от "packages" пакета:

    ```bash
    npm i -D file:packages/MY_PACKAGE
    npm run postinstall
    ```

-   Добавляем зависимость для "packages" пакета:

    ```bash
    # tst-b зависит от tst-a
    npx lerna add --scope @lavka-js-toolbox/tst-b @lavka-js-toolbox/tst-a
    ```

-   Если что-то поломалось и редактор не может найти модуль:
    ```bash
    npm run postinstall
    # если не помогло, то
    npm run dev:install
    ```

---

## Публикация пакета в npm

Пакеты [автоматически публикуются](https://nda.ya.ru/t/5ugebpIb4tQHnt) в npm после слияния с `trunk`-ом

---

## Команды пакета

-   Компилируем пакет `MY_PACKAGE`:

    ```bash
    jstool pkg compile --name MY_PACKAGE
    ```

-   Для тестирования можем опубликовать "canary" версию пакета `MY_PACKAGE` в npm:

    ```bash
    jstool pkg canary --name MY_PACKAGE
    ```

-   Проверяем пакет (ie linter, prettier, etc...):

    ```bash
    jstool pkg validate --name MY_PACKAGE
    ```

-   Тестируем пакет:

    ```bash
    jstool pkg test --name MY_PACKAGE
    ```

-   Запускаем произвольную команду из директории пакета:
    ```bash
    jstool pkg exec --name MY_PACKAGE -c 'MY_COMMAND'
    ```

---

## Команды моно-репы

-   Компилируем все пакеты:

    ```bash
    jstool compile
    ```

-   Проверяем синтаксис пакетов:

    ```bash
    jstool validate
    ```

-   Тестируем все пакеты:
    ```bash
    jstool test
    ```
