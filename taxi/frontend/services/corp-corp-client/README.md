# Яндекс.Такси - Корпоративный Клиент

Фронт для корпоративных клиентов Яндекс Такси, Драйва, Еды и потенциально прочих.

## Локальное развёртывание

#### Ожидания к окружающей среде для разработки

-   macOS или Linux
-   node.js 10 с родной версией npm. Желательно устанавливать node.js через nvm.
-   Есть рутовый доступ.

#### Порядок действий:

1. Клонируем из [монорепы фронтенда](https://github.yandex-team.ru/taxi/frontend-monorepo)
2. Переходим там в `services/corp-corp-client`: `cd services/corp-corp-client`
3. Устанавливаем зависимости: `npm i`
4. Добавляем алиасы доменов в `/etc/hosts`:
    ```
     127.0.0.1  corp-client.{yourLogin}.local.yandex.ru
    ```
5. Идём в https://crt.yandex-team.ru/certificates. Жмём "Заказать сертификат". В всплывающем окне указываем: CA name - InternalCA, Тип сертификата - Для web-сервера, Хосты - `*.{yourLogin}.local.yandex.ru` (`*.{yourLogin}.local.yandex.kz` / `*.{yourLogin}.local.yandex.com`), ABC-сервис - Сервисы Такси. Тут важно, что домен первого уровня должен быть `yandex.<ru|com|kz>`, чтобы браузер нормально отправлял куки сессии Паспорта.
6. Скачиваем .pem файл с сертификатом
7. Кладём .pem файл в `services/corp-corp-client` под именем `server.pem`
8. Запускаем командой `npm start`
9. Дожидаемся пока соберётся и выведет URL, на котором запустилось.
10. Открываем по выведенному в консоли URL. При первом заходе произойдёт редирект на тестовый паспорт, можно воспользоваться тестовой учёткой corp-test/stas1989 или rusiks1/tpQ-JVC-tBk-XN7 или завести себе тестовый аккаунт по [этой инструкции](https://wiki.yandex-team.ru/taxi/backend/logistics/instructions/Zavedenie-testovogo-KK/). Лучше не лениться и создать себе отдельный аккаунт чтобы не конфликтовать с коллегами. После входа вас средиректит на страничку без порта, необходимо дописать порт 8443, чтобы корп. кабинет открылся.

#### Работа с библиотекой компонент @yandex-taxi/go-web-components

Библиотека лежит в отдельном [пакете](https://github.yandex-team.ru/taxi/frontend-monorepo/tree/master/packages/go-web-components) в монорепе, и устанавливается, как зависимость, через npm.

В процессе работы над задачами может потребоваться вносить изменения в библиотеку, для упрощения разработки библиотеку можно слинковать командой `npm run link:dev` в папке проекта (также можно вызвать `npm run init:dev`, которая сразу переставит зависимости и все слинкует). После этого библиотека будет указана симлмнком в `node_modules`. Далее в отдельной консоли надо открыть папку библиотеки и вызвать там `npm run tsc:watch`, это запустит тайпскриптовый компилятор в режиме динамической пересборки. Таким образом при внесении изменений в библиотеку, она пересобирется тайпскриптом, это в свою очередь тригернет вебпак и изменения прорастут в дев сборку, запущенную через `npm start`.

При деплое в `unstable` библиотека линкуется, таким образом ее не надо публиковать при каждом изменении, пока идет разработка.

При сборке непосредственно релиза будет использоваться уже версия из npm, таким образом изменения, сделанные в библиотеке необходимо опубликовать, это делается через [сборку в тимсити](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Infranaim_Frontend_PublishPackage?branch=go-web-components&focusLine=0&buildTypeTab=overview&mode=builds#all-projects). Сборка апнет версию пакета и опубликует его во внутренний npm.

Однако есть проблема с тем, что новую версию библиотеки нужно апнуть в [зависимостях корп кабинета](https://github.yandex-team.ru/taxi/frontend-monorepo/blob/master/services/corp-corp-client/package.json) иначе поставится версия из `package-lock.json`. Таким образом есть как минимум два варианта:
- Перед мерджем ПР, в котором есть изменения библиотеки, вынести их в отдельный ПР и замерджить сначала его, затем опубликовать библиотеку, и в основном ПР апнуть ее версию, после этого делать его мердж. Требует больше телодвижений, но более безопасный способ, тк в мастере всегда код с актуальной версией библиотеки.
- Замерджить ПР, опубликовать библиотеку, затем сделать отдельный ПР с обновлением версии библиотеки, который можно сделать позже перед релизом, этот способ проще, но требует не забывать обновлять библиотеку перед релизом, иначе что-то может отвалится из-за того что в релиз поедет более старая версия библиотеки.

## Логгирование ошибок фронта
Идем в [error.yandex-team.ru](https://error.yandex-team.ru/projects/corp-client), далее фильтруем по окружению

## TVM и Эксперименты 3.0

Чтобы, во время разработки, сервер ходил в сервис экспериментов, нужно:
1. скачать файл [.tvm.json](https://yav.yandex-team.ru/secret/sec-01f61ytbj9mptjk726hq4t94rb/explore/version/ver-01f61ytbjm5psybaspydkmhqv1)
2. положить его в свою home директорию под таким же именем (посмотреть ее можно в переменной $HOME)
3. перезапустить сервер `npm start`

##### P.S.

Авторизовываться в тестовом паспорте лучше в отдельном браузере/инкогнито, т.к. при авторизации в тестовом паспорте затираются кукисы продакшн паспорта.

## Зависимости проекта

| Название                   | testing URL                               | production URL                        | testing URL(UI)                                | production URL (UI)                            | Comment                                                                                                                      |
| -------------------------- | ----------------------------------------- | ------------------------------------- | ---------------------------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Бункер                     | http://bunker-api-dot.yandex.net/v1       | http://bunker-api.yandex.net/v1       | https://bunker.yandex-team.ru/taxi-corp-client | https://bunker.yandex-team.ru/taxi-corp-client | Для отправки нод Бункера в продакшн надо жать "Опубликовать" в интерфейсе. Интерфейс один и тот же для продакшна и тестинга. |
| Геобаза                    | ???                                       | ???                                   | ???                                            |
| API корпоративного клиента | http://cabinet-api.taxi.tst.yandex.net/   | http://cabinet-api.taxi.yandex.net/   |                                                |
| API Yandex Trust           | https://trust-test.yandex.ru              | https://trust-test.yandex.ru          |                                                |                                                | Используется для привязки карт в [лайт-кабинете](https://business.taxi.yandex.ru/light)                                      |
| API Логистики              | http://b2b-authproxy.taxi.tst.yandex.net  | http://b2b-authproxy.taxi.yandex.net  |                                                |                                                | Используется интерфейсами заказа доставки                                                                                    |
| Авторизационный прокси     | https://ya-authproxy.taxi.tst.yandex.net/ | https://ya-authproxy.taxi.yandex.net/ |                                                |                                                | Используется для [лайт-версии кабинета](https://business.taxi.yandex.ru/light)                                               |

## Сборка для тестирования или продакшна

-   [**unstable**](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_Infranaim_Frontend_NewFlowTest?branch=corp-corp-client&mode=builds#all-projects)
-   [**testing/production**](https://teamcity.taxi.yandex-team.ru/buildConfiguration/YandexTaxiProjects_FrontendMonorepo_Stable?branch=corp-corp-client&buildTypeTab=overview&mode=builds#all-projects)

## В облаках

| Окружение | URL                                                                             |
| --------- | ------------------------------------------------------------------------------- |
| unstable  | https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_corp-client_unstable/   |
| testing   | https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_corp-client_testing/    |
| prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_corp-client_pre_stable/ |
| stable    | https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_corp-client_stable/     |

## Адреса окружений

-   development (локальная разработка)
    -   yandex.ru - `https://corp-client.${USER}.local.yandex.ru:8443`
    -   yandex.kz - `https://corp-client.${USER}.local.yandex.kz:8443`
    -   yandex.com - `https://corp-client.${USER}.local.yandex.com:8443`
    -   yango - `https://corp-client-yango.${USER}.local.yandex.com:8443`
-   unstable - https://corp-client.taxi.dev.yandex.ru
-   testing - https://corp-client.taxi.tst.yandex.ru
-   stable - https://business.taxi.yandex.ru
-   yandex.com stable - https://business.taxi.yandex.com
-   yandex.com unstable - https://corp-client.taxi.dev.yandex.com
-   yandex.kz stable - https://business.taxi.yandex.kz
-   yandex.kz unstable - https://corp-client.taxi.dev.yandex.kz
-   yango stable - https://business.yango.yandex.com
-   yango testing - https://business.yango.taxi.tst.yandex.com
-   yango unstable - https://business.yango.taxi.dev.yandex.com

## Логи

Продакшн: https://kibana.taxi.yandex-team.ru/app/kibana#/discover?_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-15m,to:now))&_a=(columns:!(_source),filters:!(),index:f8e70880-c75c-11e9-8a12-ddb2ef5a51ea,interval:auto,query:(language:kuery,query:'ngroups:%20taxi_corp-client_stable%20AND%20level:%20FATAL'),sort:!(!('@timestamp',desc)))

Анстейбл: https://kibana-unstable.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&_a=(columns:!(_source),index:'1b270220-71a3-11e9-a814-fbbb90422dbb',interval:auto,query:(language:kuery,query:'host:taxi-corp-client*'),sort:!(!('@timestamp',desc)))

Тестинг: https://kibana.taxi.tst.yandex-team.ru/app/kibana#/discover?_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&_a=(columns:!(_source),index:'1b270220-71a3-11e9-a814-fbbb90422dbb',interval:auto,query:(language:kuery,query:'host:taxi-corp-client*'),sort:!(!('@timestamp',desc)))

## Документация

-   [wiki описание тарифов](https://wiki.yandex-team.ru/taxi/korporativnoe-taksi/#interfejjs)
-   [wiki API](https://github.yandex-team.ru/taxi/backend/tree/develop/taxi-corp/corp_cabinet/protocol_1_0/schema/docs)

_В unstable окружение попадут все задачи в лейблом `deploy:unstable`. Возможно наличие конфликтов между ветками_

## Переводы

1. Идём по ссылке https://nda.ya.ru/3SjQY7 чтобы получить oAuth токен доступа для Танкера.
2. Сохраняем ег в tanker-token.txt в корне проекта
3. Обновляем список переводов командой `npm run i18n:extract:client` или `npm run i18n:extract:light`.
4. Выгружаем новые ключи командой `npm run i18n:add:client`. При этом новые ключи будут добавлены в Танкер автоматически. Старые не будут меняться. Скрипт выведет в консоль список добавленных ключей.
5. Передаём менеджеру список этих ключей чтобы заказать переводы. Желательно заскринить все места, где эти переводы будут, чтобы переводчики понимали контекс

Если хочется поредактировать ключи вручную, можно сделать это в [Танкере](https://tanker.yandex-team.ru/?project=taxi&branch=master&keyset=corp-client)

Более подробно этот процесс описан в доке: https://wiki.yandex-team.ru/taxi/backend/logistics/instructions/Kljuchi-v-Tankere-redaktura-i-perevody/

## Генератор типов

Все типы бекенда лежат в пакете `corp-types`

-   [Документация](https://github.yandex-team.ru/ktnglazachev/taxi-typings), просто дописываем нужный путь в конфиг `types.config.json`
-   Запуск `npm run typings`

## Technical Roadmap

-   Перенести corp-modules/cargo в отдельный пакет
-   Избавиться от HOC для работы с бэкендом
-   Переписать оставшийся на JS код на Typescript
-   Избавиться от stylus и заменить его CSS / JSS
-   Избавиться от react-select, заменив его на селект из MaterialUI
-   Перейти на переводы react-intl
-   Раскидать модули из corp-modules по отдельным пакетам в зависимости от их ответственности
-   Выделить сервисы Такси, Драйва, Еды как плагины к единому ядру
-   Выделить лайт-версию в отдельный сервис
-   Выделить публичные страницы в отдельный сервис
-   Постепенно избавиться от redux-query, заменив его на связку провайдера либы сетевых запросов + либы управления состоянием, скорее всего на основе Recoil
-   Перейти на webpack 5
-   Положить зависимости из глобального package.json в те места, которые их непосредственно используют
-   Придумать как ускорить сборку. Скорее всего - путём использования webpack dll или распараллеливанием.
-   Привести в порядок тайпинги сущности Order
-   Перейти на генератор тайпингов
-   Что-то порешать с npm. В текущей конфигурации постоянно теряются пакеты на верхнем уровне, типа typescript и eslint. Как решение - переход на седьмую версию с поддержкой workspaces
-   Порешать проблему с warnings от реакта по поводу дабл-рендера при использовании Recoil
