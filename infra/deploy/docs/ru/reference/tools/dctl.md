#  dctl

Инструкция по управлению сущностями Я.Деплоя, используя консольную утилиту dctl. В разделе [Деплой stage'а](#deploy-stage) описан типичный сценарий деплоя с возможностью отследить статусы деплоящихся сущностей по нисходящей: от stage до пода. Остальные разделы описывают команды dctl с подробностями, где это необходимо.

##  Токен доступа {#token}

В штатном режиме токен не нужен для работы с dctl. Токен будет получен силами клиента автоматически (через SSH) и помещён в файл `~/.dctl/token`. Однако если эта логика по какой-то причине не сработала, токен можно передать в переменной окружения `DCTL_YP_TOKEN` (название переменной окружения сложилось исторически. На самом деле dctl ходит с этим токеном не только в YP, но и, например, в Yandex.Vault).

Токен можно получить по [адресу](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=688c92864835447b9ed74221f44420b7) (откроется вкладка с вашим токеном, никому её не показывайте).

Если токен не был получен автоматически то стоит проверить что в переменной окружения `LOGNAME` указан ваш логин со staff и убедиться что SSH ключ доступен, `ssh-add -l`.

##  Куда нужен сетевой доступ для использования dctl? {#firewall-rules}

Если вы работаете с `dctl` с рабочего ноутбука, дополнительно настраивать доступы не требуется.
В противном случае, нужно заказать доступы:

* До YP. Проще всего скопировать правило [https://puncher.yandex-team.ru/?id=5e4e534144cfcff7403f7827](https://puncher.yandex-team.ru/?id=5e4e534144cfcff7403f7827)

Полный список приёмников, адреса 8090 (GRPC), 8443 (HTTPS):

```
_YPMASTERSNETS_
iva.yp.yandex.net
man-pre.yp.yandex.net
man.yp.yandex.net
myt.yp.yandex.net
pre.yp.yandex.net
sas.yp.yandex.net
vla.yp.yandex.net
xdc.yp.yandex.net
```

* До `oauth.yandex-team.ru` для получения OAuth-токенов.

##  Сборка dctl {#build}

Рекомендуем использовать `dctl` через `ya dctl`. Для этого:

* Установите `ya` из аркадии как указано в [документации](https://docs.yandex-team.ru/devtools/intro/quick-start-guide#ya-setup);
* Запустите `dctl`:

```bash
ya dctl
```

Можно также собрать `dctl` из аркадии

```bash
cd <arcadia>
ya make -j0 --checkout infra/dctl
cd infra/dctl
ya make
cd bin
```

##  Обновление ya dctl {#update}

Чтобы обновить `ya dctl` необходимо сделать:

```bash
ya dctl upgrade
```

##  Кластеры и окружения {#clusters}

Для указания кластера используется параметр `-c`. Возможно также указание следующих кластеров:

* локационные сущности (репликасет, ендпоинтсет, под): sas, man, vla, iva, myt
* кросс-локационные сущности (стейдж, мультрикластерный репликасет): xdc

Дефолтные значения для кластера:

* list локационных объектов: все продакшен-кластера
* get/list/put кросс-локационных объектов: xdc

В остальных случаях кластер должен быть указан явно.

##  Деплой stage'а {#deploy-stage}

Для деплоя stage'а необходимо подготовить файл, содержаший описание stage'а в yaml или json формате, соответствующий схеме: [https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=4996458#L26](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=4996458#L26). Пример: [https://a.yandex-team.ru/arc/trunk/arcadia/infra/dctl_specs/stage.yml](https://a.yandex-team.ru/arc/trunk/arcadia/infra/dctl_specs/stage.yml).

Вместо написания с нуля можно скачать описание уже существующего stage командой `dctl get stage <stage id>` и внести правки в него.

* `dctl put stage my_stage.yaml`. Эта команда создаст stage из `my_stage.yaml` в кластере `xdc`. Поддерживаемые кластера - `xdc` (продакшен, значение по умолчанию), `man-pre` (престейбл).
    * `--rewrite-delegation-tokens` (*необязательный*) - если необходимо [перевыписать delegation-токены](#delegation-token) в спеке стейджа для секретных переменных.
* `dctl status stage test-stage -w`. Мониторим статус stage'а. Здесь:
    * `test-stage` - `id` созданного stage'а
    * `-w` - необязательный флаг для периодического рефреша экрана (watch)
      Ждём, пока выводимая таблица перестанет быть пустой, это значит, что  stage-контролер (`stagectl`) начал обработку stage'а. Таблица содержит компоненты stage'а с агрегированным статусом. В столбце `Pods` содержатся счётчики подов для каждого компонента: `ready/in_progress/total`. Столбцы `RS` и `MCRS` (для каждого компонента заполнен только один из них) содержат `id` репликасета/мультрикласетрного репликасета, соответствующего данному компоненту. Более подробное описание команды [ниже](#stage-status).
* (*Необязательный шаг*) `dctl get test-stage --keep-ro-fields`. Получаем stage as-is из YP. Здесь интересно поле `status` в корне. Это сырой статус stage'а из YP.
* `dctl status rs <rs-id> -w` или `dctl status mcrs <mcrs-id> -w`. Мониторим статус RS/MCRS. Здесь:
    * `<rs-id>`/`<mcrs-id>` - `id` RS/MCRS, полученные на шаге 2
    * `-w` - необязательный флаг для периодического рефреша экрана (watch)
      В этой таблице представлены счётчики подов, сгруппированные по ревизиям. Более подробное описание команды [ниже](#mcrs-status).
* (*Необязательный шаг*) `dctl get rs <rs-id> --keep-ro-fields` или `dctl get mcrs <mcrs-id> --keep-ro-fields`. Опциональный шаг. Получаем RS/MCRS as-is из YP. Здесь вновь интересно поле `status` в корне - это подробный статус сущности.
* `dctl list pod <rs-id|mcrs-id>`. Получаем список подов для RS/MCRS. Здесь:
    * `<rs-id|mcrs-id>` - id RS/MCRS, полученные на шаге 2
    * `-c` - кластер, можно указать несколько
    * `-w` - необязательный флаг для периодического рефреша экрана (watch)
      В этой таблице можно следить за агрегированными статусами подов. Если под долго не становится `Ready`, переходим к шагу 7. Более подробное описание команды [ниже](#list-pods).
* `dctl get pod <pod-id> --keep-ro-fields` Получить под as-is из YP. Корневое поле `status` содержит подробную информацию о процессе деплоя пода. Здесь можно найти ошибки от YP/pod-агента/node-агента с подробной информацией о причине ошибки.

##  Копирование stage'а {#copy-stage}

Для создания похожих стейджей существует также специальная команда `copy`, которая позволяет создать новый стейдж на основе старого. Операция `copy` автоматически перевыписывает delegation-токены для нового стейджа. Она эквивалентна такому набору команд: `get + edit + put --rewrite-delegation-tokens`.

Чтобы скопировать stage, используется следующая последовательность:

1. `dctl get stage old_stage > my_stage.yaml`. Получаем спеку уже имеющегося стейджа.
1. При необходимости редактируем `my_stage.yaml` — если в новом stage'е необходимо использовать какие-то другие пути или иные параметры.
1. `dctl copy stage my_stage.yaml new_stage_id`. В результате из спеки будет создан stage с именем `new_stage_id` и перевыписанными секретами.

##  Список подов {#list-pods}

`dctl list pod <rs-id|mcrs-id> -w`

* `<rs-id|mcrs-id>` - id RS или MCRS, поды которых необходимо получить
* `-с` - кластера для получения подов. По дефолту это `man`, `sas`, `vla`, `iva`, `myt`. Если необходимы тестовый кластер (`man-pre`), его нужно указывать явно
* `-w` - необязательный флаг для периодического рефреша экрана (watch)

Опишем некоторые столбцы возвращаемой таблицы:

* `Target` - целевая ревизия пода `TPod.spec.pod_agent_payload.spec.revision`
* `Current` - текущая ревизия пода `TPod.status.agent.pod_agent_payload.status.revision`
* `Pod` - статус пода `TPod.status.agent.pod_agent_payload.status.in_progress` или `TPod.status.agent.pod_agent_payload.status.ready`
* `Time` - время последнего изменения статуса пода
* `State` - статус под-агента `TPod.status.agent.state`
* `Volumes` - статус вольюмов для Current ревизии
* `Workloads` - статус ворклоадов для Current ревизии
* `Boxes` - статус боксов для Current ревизии

####  Статус MCRS {#mcrs-status}
`dctl status mcrs <mcrs-id> -w`

* `mcrs-id` - id MCRS
* `-w` - необязательный флаг для периодического рефреша экрана (watch)

Опишем некоторые столбцы возвращаемой таблицы:

* `Cluster` - кластер
* `Rev` - текущая ревизия подов
* `Pods` - счётчики подов для данного MCRS в кластере `Cluster` с текущей ревизией `Rev`. Представлены три счётчика: первый соответствует подам в статусе `Ready`, второй - в статусе `InProgress`, третий - сумма `Ready` и `InProgress` подов. Далее для обозначения такой тройки используем `ready/in_progress/total`
* `TotalPods` - счётчики подов для данного MCRS в кластере по всем ревизиям
* `CtlStatus` - статус контроллера, обрабатывающего данный MCRS в кластере `Cluster`

##  Статус stage'а {#stage-status}

`dctl status stage <stage-id> -w`

* `stage-id` - id stage'а
* `-w` - необязательный флаг для периодического рефреша экрана (watch)

Опишем некоторые столбцы возвращаемой таблицы:

* `SpecRev` - ревизия спеки stage'а
* `ComponentID` - id компонента
* `DeployStatus` - статус компонена `ComponentID`. Соответствует полям `ready` и `in_progress` из `TComponentStatus`.
* `Pods` - счётчики подов для компонента `ComponentID`  в формате `ready/in_progress/total`. Соответствует полю `progress` из `TComponentStatus`.
* `Clusters` - кластера, в которых разворачиваются поды. Если компонент деплоит репликасеты, то в этих кластерах развёрнуты также и репликасеты, если же компонент деплоит мультикластерный репликасет, то в этих кластерах развёрнуты только поды, а мультикластерный репликасет развёрнут в xdc-кластере (для продакшена).
* `RS` - id репликасетов (которые развёрнуты в кластерах `Clusters`), если компонент деплоит репликасет, иначе `None`.
* `MCRS` -id мультикластерного репликасета, если компонент деплоит мультикластерный репликасет, иначе `None`
* `ES` - id эндпоинтсетов (которые созданы в кластерах `Clusters`)

##  Как заполнить поле tvm_config в спеке стейджа {#tvm-config}

Поле `tvm_config` служит для генерации [конфига для tvmtool'а](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/).

Начнём с примера:

```yaml
tvm_config:
  blackbox_environment: Test
  client_port: 2
  clients:
    - destinations:
      - abc_service_id: '2222'
        alias: d1
        app_id: 2222222
        secret_selector:
          alias: secret-alias-from-secrets-spec
          id: TVM_SOURCE_1
      source:
        abc_service_id: '1111'
        alias: s1
        app_id: 1111111
```

`blackbox_environment` соответствует [BbEnvType](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#opisanieformatakonfiganajsonschema) в tvmtool-кофиге.

`client_port` - порт, на котором запущен `tvmtool`.

`source` - описание tvm-приложения, из которого будем ходить в tvm-приложения `destinations`. Подробнее про поле [alias](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#ispolzovaniepsevdonimov).

`secret_selector` - [селектор секрета](../../how-to/secrets.md#selector) для tvm-приложения `source`.

##  Как выписать delegation-токен для секрета {#delegation-token}

Работа по автоматическому выписыванию delegation-токенов в dctl ведётся в тикете: [https://st.yandex-team.ru/DEPLOY-1424](https://st.yandex-team.ru/DEPLOY-1424).

"Ручной" вариант выписывания delegation-токенов описан [вот тут](../../how-to/secrets.md#dctl).

{% note info %}

Обращаем внимание, что секрет выписывается для пары `stage` и `deploy_unit`, т.е. при копировании stage или при создании еще одного `deploy_unit`, надо выписывать дополнительные `delegation_token`.

{% endnote %}

##  Создание драфтов для стейджей с двойными апрувами {#drafts}

Если в стейдже включена политика апрува, то редактировать стейдж напрямую нельзя. Необходимо сначала создать и опубликовать драфт с изменениями. Результатом публикации будет релизный тикет, включающий дифф изменений. Этот тикет нужно поапрувить и только после этого закоммитить. Пример того, как создать и опубликовать драфт для стейджа из dctl:

```bash
ya dctl get stage my-stage > s.yaml
# редактируем s.yaml
ya dctl publish-draft stage s.yaml --message "Draft for release 1.0"
```

Команда `ya dctl publish-draft stage s.yaml` вернёт url релизного тикета, который нужно поапрувить и закоммитить из UI.
Необязательный параметр `--message` в команде `publish-draft` будет подставлен в заголовок созданного релизного тикета (по дефолту `Publish from dctl`). Заголовок релизного тикета используется далее при коммите тикета в стейдж: он подставляется в комментарий к ревизии стейджа, если этот комментарий не указан явно.

##  Примеры других команд {#other-commands}

Получение
* stage'а `dctl get stage <stage-id>`
* RS `dctl get rs <rs-id>`
* MCRS `dctl get mcrs <mcrs-id>`
* подсета `dctl get ps <ps-id>`
* эндпоинтсета `dctl get es <es-id>`
* пода `dctl get pod <pod-id>`
  Необязательные флаги:
  `--format pb/yaml` - формат возвращаемого объекта(протобаф или yaml). По умолчанию - yaml
  `--keep-ro-fields` - получить объект полностью с read-only полями (например, status)
  `--limit` - количество объектов, которое необходимо получить. По умолчанию - 100
  Список
* stage'ей `dctl list stage`. Команда возвращает stage'и текущего пользователя. Для получения stage'ей без фильтра по пользователю необходимо добавить флаг `-a`
* MCRS `dctl list mcrs`. Команда возвращает MCRS текущего пользователя. Для получения MCRS без фильтра по пользователю необходимо добавить флаг `-a`
* RS `dctl list rs`. Команда возвращает RS текущего пользователя. Для получения RS без фильтра по пользователю необходимо добавить флаг `-a`
* эндпоинтсетов `dctl list es` Команда возвращает ES текущего пользователя. Для получения ES без фильтра по пользователю необходимо добавить флаг `-a`
* подов для RS/MCRS `dctl list pod <rs-id|mcrs-id>`
* эндпоинтов для ES `dctl list ep <es-id>`
  Cоздание/обновление
* stage'а `dctl put stage my_stage.yaml`
  **Создавать и обновлять RS/MCRS руками не имеет смысла. Ваши обновления будут затёрты Stage Controller'ом**

Удаление
* stage'а `dctl remove stage <stage-id>`
  **Удалять RS/MCRS руками не имеет смысла. Они будут пересозданы Stage Controller'ом**

##  Changelog {#changelog}

#### 07.04.2021 (svn revision: 7985423)
* Добавлен фильтр stage'ей по проекту (DEPLOY-3187) `dctl list stage --project <project-id>`

* Убрали взаимоисключающие параметры `['stage', 'all', 'recipe_id']` для
  `list release_rule` - теперь можно использовать фильтры `--stage` и `--recipe-id` без фильтра по пользователю:

  `dctl list release_rule --all --recipe-id <recipe-id> --stage <stage-id>`

* Убрали взаимоисключающие параметры `['stage', 'all']` для
  `list approval_policy` - теперь можно использовать фильтр `--stage` без фильтра по пользователю:

  ` dctl list approval_policy --all --stage <stage-id>`

