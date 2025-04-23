# Создание нового приложения

> Документация находится в процессе написания

> Данная документация **является ПРИМЕРОМ** создания инфраструктуры для поднятия нового сервиса и может не покрывать ваш кейс

> Данная документация **может устареть**, если в вашей команде есть эксперт по инфраструктуре - посоветуйтесь с ним,
> если нет - самостоятельно прочитайте приложенные конкретные документации перед началом работы

> Данная документация рассчитана на поднятие простых сервисов без доп. требований и интеграций,
> реализованных через докер-контейнер с http приложением.

## Перед началом

1. Узнайте свой [ABC сервис](https://abc.yandex-team.ru/) (будем далее именовать `<abc-service>`).
   Пример - [ABC Путешествий](https://abc.yandex-team.ru/services/portalvteam/resources/?view=consuming&layout=table&supplier=14)
2. Придумайте название и полное название (вместе с префиксом группы проектов) вашего приложения
    - Название будем далее именовать `<short-name>`, например, `example`
    - Полное название будем далее именовать `<name>`, например, `travel-frontend-example`
3. Решите, какие окружения вам нужны (будем далее именовать `<env>`, например, `testing` + `production`)
4. TODO Sandbox - [https://sandbox.yandex-team.ru/admin/groups/TRAVEL-FRONT/general](https://sandbox.yandex-team.ru/admin/groups/TRAVEL-FRONT/general)
5. Подготовьте Docker образ. [Дока про Docker registry на Wiki](https://wiki.yandex-team.ru/docker-registry)

    > В примере будет рассмотрено NextJS приложение

    1. Скопируйте свой [OAuth токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
    2. Авторизуйтесь локально

    ```shell
    $ docker login -u $(whoami) registry.yandex.net
    Password: <OAuth token body>

    Login Succeeded
    ```

    3. Соберите и запушьте образ, он позже будет использован для деплоя **TODO - Информация о базовых образах и неймспейсах в Яндексе**
        ```shell
        docker build -t registry.yandex.net/data-ui/example-app:0.0.1-1 .
        docker push registry.yandex.net/data-ui/example-app:0.0.1-1
        ```

## Шаг 1 - TVM

[Основная инструкция на Wiki](https://ui.yandex-team.ru/core/tvm).
Для того чтобы наше приложение могло слать запросы в другие сервисы, мы должны создать для него TVM приложение,
получить информацию о TVM ID нужных сервисов и попросить разработчиков этих сервисов указать наш TVM ID,
как один из известных источников.

1. [Создать приложения под разные среды в ABC](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/tvm-getting-started)
    - Идём в ваш ABC, жмём Создать сервис для каждого окружения
    - Название на английском, slug - `<name>-<env>` (например, `travel-frontend-example-testing`)
    - Родитель - ваш родительский сервис
2. Настройка
    1. Просим разработчиков нужных сервисов указать наш tvm_id у себя
    2. Когда перейдете к локальной разработке - поднимите локальный tvm
       (у нас есть [генератор локального TVM демона](../libs/codegen/readme.md#a-namelocal-tvma-tvm))
3. Идем в [Секретницу](https://yav.yandex-team.ru) и для каждого приложения создаём `<name>-<env>-tvm`
   (например, `travel-frontend-example-testing`), если в TVM-приложении нет прикрепленной ссылки на секретку
   или вы хотите создать собственную секретку

## Шаг 2 - Сети и доступы

Нам требуется создать под каждое окружение сеть и настроить доступы в неё и из неё.
Все сервисы Яндекса хостятся в рамках [виртуальных сетей (RackTables)](https://racktables.yandex-team.ru/index.php?page=services&tab=projects)
и для любого доступа из нашего нужно заказывать [исключения в Puncher](https://puncher.yandex-team.ru/).

1. Создаём сеть для тестового окружения в [RackTables](https://racktables.yandex-team.ru/index.php?page=services&tab=projects).
   [Дока про создание сети](https://docs.yandex-team.ru/nocdoc/processes/project_id/get_new_project_id/about).
   `TODO - production сеть`
    - Жмём "Новый проект"
    - `Макрос: _<name>_TEST_NETS_ (далее - <network_name>)` - например, `_TRAVEL_FRONTEND_EXAMPLE_TEST_NETS_`
    - `Описание: не критично` - например, `created by <me> - my example service test nets`
    - `Ответственные - ставим группу администрирования из вашего ABC: svc_<abc>_<group>` - например, `svc_portalvteam_administration`
        > **Важно** - Вы должны находиться в этой группе, если вас там нет - заранее попросите вас добавить
    - OK
2. Идём в [Puncher](https://puncher.yandex-team.ru/) и создаём нужные дырки (кнопка `Создать новое правило`)

    > **Ваша сеть может появиться с задержкой до нескольких часов**

    > Данный пример рассчитан на тонкие клиенты, которые работают только с другими внутренними сервисами

    1. Доступ к BlackBox (возможно, уже будет создано в рамках глобальных сетей)
        - `Назначение: нужный адрес BlackBox` - например, `blackbox.yandex-team.ru`
        - `Протокол - TCP, Порты - 80, 443, Срок - Вечное`
        - `Комментарий: В <env> <my service> нужен доступ до <вид> ЧЯ` - например, В тестовом окружении Примеру сервиса нужен доступ до корпоративного ЧЯ
    2. Доступ к нужным АПИ
        - `Назначение: <ваш сервис>` - например, `foo-bar-service.yandex.net`
        - `Протокол - TCP, Порты - 80, 443, Срок - Вечное`
        - `Комментарий: В <env> <my service> нужен доступ до такого-то апи`
    3. Доступ к сети по SSH для вашей команды
        - `Источник: Разработка (<abc>), Администрирование (<abc>)`
        - `Назначение: <network_name>`
        - `TCP - 22, срок - вечное`
        - `Комментарий: Для доступа разработчиков и администраторов до <env> <name>`
    4. Доступ к сети из балансера
        - `Источник: Сеть вашего балансера (узнайте у коллег)` - например, _TRAVEL_YA_FRONT_TEST_NETS_
        - `Назначение: <network_name>`
        - `TCP - 80, 443, срок - вечное`
        - `Комментарий: Доступ от <env> L7-балансера до инстансов <env> <name> в YDeploy`

## BlackBox (если нужен)

Если ваше приложение будет работать с пользователями Яндекса (любыми), вам нужно запросить доступ из него в BlackBox.
Заполняем [форму получения грантов для BlackBox](https://forms.yandex-team.ru/surveys/4901/)

-   `Название сервиса: <name>-<env>`
-   `Ссылка на ABC: ссылка на ваш ABC сервис`
-   `Целевой ЧЯ: зависит от того, с чем будете работать` - например, `Внутренний ЧЯ` для приложений внутри yandex-team.ru
-   `Сети: <newtork_name>, <QYP сеть>` - желательно сразу указать все нужные (можете только `<network_name>`)
    -   `<network_name>` - сеть, в которой будет развернуто наше приложение
    -   `<QYP сеть>` - сеть, в которой развернута ваша [Дев машина в QYP](https://qyp.yandex-team.ru/)
-   `medthod (has_cred): sessionid` - появятся доп. поля, в которые нужно записывать идентификаторы нужных полей через запятую.
    Для понимания, что вам нужно, пробегитесь по табличкам
    -   [attributes](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#db-attributes) - например, `1007, 1008` (фио и логин)
    -   [phone_attributes](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#section_kbk_b5f_2hb_)
    -   [email_attributes](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#section_kbk_b5f_2hb)
    -   `dbfields` - **deprecated**, ничего не пишите
-   `Комментарий - коротко опишите, что для такого-то приложения нужны такие-то атрибуты в таких-то сетях`

## [Yandex Deploy](https://deploy.yandex-team.ru/)

1. Идём в [Yandex Deploy](https://deploy.yandex-team.ru/?my=yes), жмем Create new project
    - Project name: `<name>`
    - ABC Service: `<abc-service>` (поиск по названию)
2. Создаём Stage (Create new stage) под каждое окружение
    - `Stage ID: <name>-testing` - например, `travel-frontend-example-testing`
    - Deploy Unit
        - `Deploy Unit ID` - придумайте название (например, `application`)
        - `Network ID` - выберите сеть ваших сервисов (например, `_YA_TRAVEL_FRONT_TEST_NETS_`)
        - `Location policy`
            - `Deploy unit type: Multi-cluster` **возможно, вам не подойдет**) - TODO Добавить ссылку на доку
            - `Disruption budget: 1`
            - Выбираем сервера (например, `SAS, VLA, MAN`) - ставим везде `Pods quantity: 1`, убираем галки `Per node / Per rack`
        - `Per pod settings`
            - `CPU: 2 (CPU)`
            - `RAM: 2-8 (GB)` - допустим, 3
        - `TVM: Enabled`
            - `Blackbox` - в зависимости от окружения и того, где будет развернуто приложение
            - `Source` - TVM App: TVM ID из созданного приложения, Alias - `app` (например, `1234567 - app`)
            - `Destination` - ставим blackbox с нужным Id (например, `223 - blackbox`) и нужные сервисы (например, `20202020 - api`)
            - `Secret` - выбираем секретку, созданную для tvm-приложения автоматически, либо вами вручную, выбираем поле с tvm-секретом
        - `Monitoring in YASM` - `YASM itype: <пустая строка>`, все галки disabled
        - `Logbroker Tools, Pod Agent` - выбираем поновее
    - Box
        - `Box ID` - придумайте название (например, `application-box`)
        - `resolv.conf: default`
    - Workload - пока не трогаем (ну, переименовать можно)

## Настройка Awacs балансеров

L3/L7 - Создаем балансер, настраиваем инфраструктуру в Nanny

1. ЕСЛИ НЕТ НЕЙМСПЕЙСА - [Создаём неймспейс](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/create/) в Nanny
    - `Id: <name>-<env>`
    - `Category: <your-project-root>/<short-name>/<env>` - например, `travel/example/testing`
    - `Envitonment: <env>`
    - `ABC service id: <abc-service>`
    - `Owners - Logins: Добавьте себя`
    - `Owners - Group Ids: Выберите вашу группу разработчиков в ABC` - например, `Разработка (Фронтенд Яндекс.Путешествий)`
    - После создания неймспейса вам требуется [Создать в нём L3/L7 балансеры](https://wiki.yandex-team.ru/awacs/tutorial/l3-l7/)
2. `Backends -> Create backend` - В данном примере мы создаём по бекенду для каждого кластера,
   например, `SAS, VLA, MAN`. Можно обойтись одним бекендом с указанием нескольких Endpoint`ов
    - `Id: <short-name>-<env>-<cluster>` - например, `example-testing-sas`
    - `Type: YP endpoints set (fast)`
    - `Endpoint set id: <name>.<Deploy Unit ID>` - например, `travel-frontend-example-testing.application`
3. `Upstreams -> Create upstream`
    - `Id: <short-name>-<env>` - например, `example-testing`
    - `Mode: Easy` - [позволяет пользоваться макросами](https://wiki.yandex-team.ru/awacs/upstream-easy-mode)
    - `YAML` - ПРИМЕР КОНФИГА (замените `example-testing`):

```yaml
l7_upstream_macro:
    id: example-testing
    version: 0.2.0
    by_dc_scheme:
        balancer:
            attempts: 1
            backend_timeout: 10s
            connect_timeout: 100ms
            do_not_retry_http_responses: true
            fast_attempts: 2
            max_pessimized_endpoints_share: 0.2
            max_reattempts_share: 0.15
            retry_non_idempotent: false
        dc_balancer:
            attempts: 2
            method: BY_DC_WEIGHT
            weights_section_id: bygeo
        dcs:
            - backend_ids:
                  - example-testing_sas
              name: sas
            - backend_ids:
                  - example-testing_vla
              name: vla
            - backend_ids:
                  - example-testing_iva
              name: iva
        on_error:
            static:
                content: Service unavailable (Generated by L7-balancer)
                status: 504
    headers:
        - create: { target: X-Forwarded-For-Y, func: realip }
        - create: { target: X-Forwarded-Host, func: host }
        - create: { target: X-Real-IP, func: realip }
        - create: { target: X-Request-Id, func: reqid }
        - create: { target: X-Start-Time, func: starttime }
    matcher:
        any: true
```

4. `Certificates -> Order certificate` - просто для примера, можно не делать, при создании домена можно автоматически создать сертификат
    - `ID: <name>-<env>.yandex-team.ru` - например, `travel-frontend-example-testing.yandex-team.ru`
    - `Type: Internal`
    - `Primary domain: такой же, как ID`
    - Submit и подождать некоторое время (обычно около минуты) до активации
5. `Domains -> Create new domain` ([Документация](https://wiki.yandex-team.ru/awacs/tutorial/domains-in-awacs/))
    - `ID: <short-name>-<env>` - например, `example-testing`
    - `Primary FQDNS: Из сертификата`
    - `Upstreams: Choose -> выберите созданный апстрим`
    - `Protocol: HTTP and HTTPS / HTTPS`
    - `Certificates: Use a single -> выберите созданный сертификат`

## DNS

Готовим DNS ([Форма](https://dns.tt.yandex-team.ru/request), [Wiki](https://wiki.yandex-team.ru/traffic/dnsmgr/))

1. Перейти в ваш неймспейс в Nanny ([пример для Travel](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/show))
2. Перейти в L3 Balancers -> Ваш балансер
3. Перейти на его cтраницу в L3 Manager (L3 L3mgr Service ID)
4. Configurations -> Перейти на текущую Active конфигурацию
5. В Virtual servers будет колонка IP - копируем значение (будем называть далее `<l3-ip>`)
6. [Идём в форму DNS Manager](https://dns.tt.yandex-team.ru/request), вводим только AAAA запись

```text
<name>-<env>.yandex-team.ru AAAA <l3-ip>
```

7. Prepare -> видим результат с добавлением одной записи (<name>-<env>.yandex-team.ru AAAA <l3-ip>)
8. Submit
9. Ждём (от пары часов до пары дней)
