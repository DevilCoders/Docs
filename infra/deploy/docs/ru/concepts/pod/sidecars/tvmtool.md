# TVM tool

На данной странице описано, как настроить TVM в Deploy.
[Описание самого tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/)

## Ресурсы для TVM {#resources}

Для TVM на каждый под будут **дополнительно** (сверх указанного пользователем размера Пода) запрошены следующие ресурсы из квоты ABC-сервиса:

* 950 МБ диска.
* 30 МБ RAM.
* 0.1 CPU.

Пользователь сможет поменять эти лимиты через dctl  — для этого нужно переопределить [соответствующие поля](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=7444694#L317-320) в спецификации стейджа.

## Настройка в режиме get and check {#get-check}

1. Порт, по которому можно ходить в TVM (например по ручкам `/tvm/tickets` или `/tvm/checksrv`).
1. Ping port для TVM (поднимает ручку `/tvm/ping` на всех интерфейсах в отличие от основного).

    {% note warning %}

    Более не используется, все запросы ходят в основной порт.

    {% endnote %}

1. Blackbox для TVM, подробнее про него можно почитать [тут](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/#0-opredeljaemsjasokruzhenijami).
1. TVM приложения в вашем deploy unit (их может быть несколько, чтобы добавить еще одно, надо нажать `Add client`).
1. Ваше TVM приложение.
1. В какие TVM приложения вы хотите ходить (Точек назначения может быть несколько, еще одну можно добавить нажав `Add destination`).
1. Секрет из [секретницы](https://yav.yandex-team.ru), который содержит `client_secret`.

В [proto-схеме](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto) нужно заполнить поле `TDeployUnitSpec.tvm_config`. Назначение полей внутри него описано в схеме.


## Настройка в режиме check only {#check-only}

Пока не реализована: [https://st.yandex-team.ru/DEPLOY-1849](https://st.yandex-team.ru/DEPLOY-1849)

В качестве временного решения можно в `Source` и `Destination` указать одно и тоже приложение.

## Дополнительные настройки {#extra-settings}

`roles_for_idm_slug` — поддержка работы с ролями IDM.
`use_system_certs` — не пытаться читать сертификаты с диска, для конфигураций с маленькой пропускной способностью диска.

```yaml
  tvm_config:
    blackbox_environment: "ProdYaTeam"
    clients:
      - destinations:
          - app_id: 1234
        roles_for_idm_slug: "passporttestservice"
        secret_selector:
          alias: "tvm.secret.1234"
          id: "client_secret"
        source:
          app_id: 1234
    mode: "enabled"
    use_system_certs: false
  tvm_sandbox_info:
    revision: 1234
```

## Что делает настройка TVM tool {#tvm-tool-setup}

В ваш deploy unit будет добавлен дополнительный `box`, в котором будет поднят `workload` с TVM демоном.

В env каждого контейнера будут добавлены две переменные:

* `TVMTOOL_LOCAL_AUTHTOKEN`, с помощью которой можно будет авторизоваться у TVM демона.
* `DEPLOY_TVM_TOOL_URL`, которая равна `"http://localhost:{}".format(client_port)` (при настройках из примера это будет `http://localhost:32272`).

Иными словами, чтобы сходить в TVM, вам нужно сделать запрос аналогичный этому:

```bash
curl "$DEPLOY_TVM_TOOL_URL/tvm/tickets?src=from1&dsts=to1" -H "Authorization: $TVMTOOL_LOCAL_AUTHTOKEN"`
```

## Описание API и примеры запросов к HTTP интерфейсу {#api}

[Смотри в документации TVM](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#httpapitvm-demona)

## История изменений {#changelog}

Есть два вида ченджлога: один касается версии самого сайдкара, а другой — внешних его настроек (на базе runtime version).

### Изменения на базе runtime version {#changelog-runtime}

* С [runtime version 6](../../../reference/patchers-revision.md#new-runtime-version-6) добавлена возможность сбора портометрик с системных сайдкаров [DEPLOY-4649](https://st.yandex-team.ru/DEPLOY-4649).

* С [runtime version 10](../../../reference/patchers-revision.md#new-runtime-version-10) конфигурация TVM прокидывается в ворклоады в переменную окружения `DEPLOY_TVM_CONFIG` без секретов для обеспечения требования безопасности.


## Контакты {#contacts}

Если что-то не работает со стороны TVM, напишите на рассылку [tvm-dev](mailto:tvm-dev@yandex-team.ru) или, для оперативного ответа, спросите в [чате](https://t.me/joinchat/BXoEWEpu5Scc2Af1Rzzd4Q).
