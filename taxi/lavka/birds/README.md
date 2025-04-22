# lavka-birds

## Common

`lavka-birds` - это монорепозитарий для нескольких внутренних сервисов Яндекс.Лавки.

---
## Requirements

### Обязательно

*   arc
*   [docker и docker-compose](https://wiki.yandex-team.ru/lavka/services/docker-desktop/)
*   node 16.16.0
*   npm 8.11.0

### Опционально

*   nvm

---

## Quick Start

### Предварительная подготовка

* Установить и настроить `arc` — [документация](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#arc-setup)

* Залогиниться в яндексовый `docker distribution`:
    * Выпустить OAuth-токен для доступа в хранилище: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1
    * Непосредственно залогиниться:
        ```bash
        DOCKER_TOKEN=<здесь токен из предыдущего пункта>
        echo "$DOCKER_TOKEN" | docker login -u <login> --password-stdin registry.yandex.net
        ```
    * Подробнее в [документации](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)

### Установка зависимостей

Можно выкачать зависимости всех сервисов или же зависимости только одного необходимого сервиса

-   ```bash
    # Выкачиваем все зависимости
    npm ci
    ```

    ```bash
    # Если у вас macos, то нужно установить cmake, иначе не заведется falcon
    brew install cmake
    ```

-   ```bash
    # Выкачиваем зависимости одного сервиса
    npm ci --workspace=@lavka-birds/{service_name}
    ```

### TeamCity Releases

Для выкатки сервиса необходимо в селекте веток выбрать ветку, соответствующую сервису, который хотим выкатить.

*   **unstable**
    *   [Выпустить релиз](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_Birds_Customs_CustomUnstable)

    * Для выбора деплоя на `unstable` или `unstable2` нужно нажать `на 3 точки` рядом с кнопкой `Run`
    * В открытом попап, нужно перейти на вкладку `parameters`
    * В `rtc_dest` выставить `unstable` или `unstable2`

*   **testing**
    *   [Выпустить релиз](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_Birds_Customs_CustomTesting)

*   **production**
    *   [Выпустить релиз](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_Birds_Releases_AutoRelease)
    *   [Выпустить hotfix](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_Birds_Releases_Hotfix)
    *   [Докатка релиза](https://wiki.yandex-team.ru/taxi/backend/deploy/#priattachitsjaktekushhemurelizudokatka)

*   [Очередь PR](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Lavka_Birds_PullRequests_PullRequests)
*   [Настройка уведомлений](https://teamcity.taxi.yandex-team.ru/profile.html?item=userNotifications)
    <br/>E-mail уведомления **не поддерживаются**
    <br/>Настройка [telegram уведомлений](https://wiki.yandex-team.ru/taxi/backend/automatization/faq/#teamcity-telegram-notifier)

## Полезные ссылки

*   [Wiki | Lavka Birds](https://wiki.yandex-team.ru/lavka/birds/)
*   [Инструкции по релизу](https://wiki.yandex-team.ru/taxi/backend/deploy)
*   [Clownductor | Как заехать сервисом в облако](https://wiki.yandex-team.ru/taxi-ito/cloudhowto/)
*   [Clownductor | Запрос роли](https://wiki.yandex-team.ru/taxi/backend/architecture/clownductor/poservisnye-roli/zapros-roli/)
*   [Docker | Registry authorization](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization)
*   [Завести отдельную БД для unstable2](https://st.yandex-team.ru/EDAOPS-4961#61b8744f3bfd4c7fe5c167cb)
