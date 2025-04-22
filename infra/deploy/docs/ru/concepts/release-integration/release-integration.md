# Релизная интеграция

![release-integration](../../_assets/concepts/release-integration.png)

Релизная интеграция в Я.Deploy — это обеспечение принципов [CI/CD](https://en.wikipedia.org/wiki/CI/CD) в нашем облаке.
В каких случаях вы можете захотеть её в своём проекте:

1. Чтобы настроить выкладку сервиса по клику после нажатия кнопки **Release** в Sandbox — без ручной правки ресурса во всех деплой юнитах.
1. Чтобы настроить автовыкладку новых релизов — без написания какого-то кода с логикой поверх Я.Deploy.
1. Чтобы обеспечить пайплайн «мой артефакт — всем желающим», когда вы собираете релизы своего общего компонента, а другие команды по клику или автоматикой выкладывают его в свои сервисы.
1. Чтобы удобно прокатывать релизы по цепочке testing — prestable — stable.

Релизная интеграция описывается тремя моделями:

1. [Релиз](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/release.proto) — объект, который создаётся [вручную](#release-docker) для Docker-образов в [Docker registry](https://wiki.yandex-team.ru/docker-registry/) и автоматикой для релизнутых задач в Sandbox, если они унаследованы ([пример](https://a.yandex-team.ru/arc_vcs/sandbox/projects/deploy/SampleReleaseToYaDeploy2/__init__.py)) от соответствующего [mixin](https://a.yandex-team.ru/arc_vcs/sandbox/projects/common/ya_deploy/release_integration.py).
1. [Релизное правило](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/release_rule.proto) — это инструкция, которую создаёт пользователь. В правиле содержится информация (селектор) о том, какие релизы надо выкатывать, инструкции (патчи), к каким частям вашего стейджа должен быть применён релиз, и идентификатор рецепта выкладки. В качестве целей изменения могут использоваться [porto-слои](../pod/podagentpayload/resources/layer.md), [статические](../pod/podagentpayload/resources/staticresource.md) или динамические ресурсы, а также docker-образ, если сервис выкладывается при помощи образа.
Кроме того, в правиле можно выставить флаг `auto_commit_policy`, который определяет, должны ли релизы выкатываться автоматически. При его включении будет использоваться политика выкладки maintain active trunk. Она будет обновлять стейдж на самый свежий возможный релиз, пропуская все невыехавшие старые.
1. [Тикет на выкладку](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/deploy_ticket.proto) — объект выкладки, создаётся автоматикой при появлении нового релиза для каждого релизного правила, которому этот релиз подходит. Тикет содержит в себе информацию о том, какой именно применяется релиз, к чему и каким правилом. При коммите пользователем или автоматикой этот тикет пропатчит в соответствии с условиями спецификацию стейджа, запустив тем самым выкладку.

## UI {#ui}

### Релизное правило {#rule}

Все релизные правила для стейджа отображены на вкладке **Deploy Tickets** в UI, в выпадающем списке **Select or create rule**.
Изначально там пусто, но доступны кнопки, позволяющие создать правило, в зависимости от источника артефакта - Sandbox-ресурса, или Docker-образа.

![release-integration](../../_assets/concepts/release-rule-list.png)

Нажав на кнопку создания правила, можно заполнить всю информацию о правиле:

1. Название релизного правила. Название правила должно быть уникальным среди вообще всех релизных правил. По умолчанию оно генерируется на основе имени стейджа, но если для одного стейджа создаётся несколько правил, имеет смысл придумать какие-то понятные имена, чтобы различать правила.
1. Типы релизов. В Sandbox бывают релизы четырёх видов: `unstable`, `testing`, `prestable`, `stable`. Можно выбрать любую их комбинацию и тогда правило будет создавать тикеты на выкладку только заданных видов релизов. Так, в примере на скриншоте мы создаём правило только для testing релизов.
1. Флаг автокоммита. Если он включен, тикеты данного правила будут автоматически применяться к сервису, не дожидаясь ручного подтверждения пользователем.
1. Вид релизного правила. Бывают правила, которые применяют Sandbox-релизы, и правила, которые применяют Docker-релизы. На скриншоте приведён пример Sandbox-правила.
1. Тип Sandbox-задачи, которая создаёт релизы.
1. Тип Sandbox-ресурса, который надо взять из релиза.
1. Название слоя или статического ресурса, который этим ресурсом необходимо обновить.
1. Название патча. Название должно быть уникально в пределах релизного правила и как правило нужно, когда вы хотите применить релиз частично (то есть, наложить только несколько патчей из релизного правила) или когда сервис отображает ошибку применения релиза — название патча поможет вам найти источник проблемы.

{% note info %}

Патчей (пункты 6-8) может быть несколько, если ваш Sandbox-релиз собирает несколько ресурсов и вы хотите одновременно обновлять несколько ресурсов и/или слоёв.

{% endnote %}

Для Docker описание патчей выглядит иначе:
1. Вместо типа Sandbox-задачи здесь выбирается имя Docker-образа.
1. Box, чей образ необходимо обновить.
1. Имя патча. Семантика такая же, как и у Sandbox-правил.

### Тикеты {#tickets}

Тикеты на выкладку автоматически создаются для каждого релиза, который попадает под данное правило. О создании релизов читайте [ниже](#release-creation).

Для каждого стейджа с настроенной релизной интеграцией отображаются его тикеты. Есть возможность каждый закоммитить или отменить, а также поставить апрув, если настроена политика апрувов. Если какой-то тикет сейчас применяется, это будет также отражено. Чтобы изменить сразу несколько тикетов, используйте массовые операции, выделяя нужные тикеты или патчи.
Со страницы тикетов для стейджа можно для каждого тикета перейти на страницу релиза, где собраны все тикеты этого релиза.

Релизные правила с автокоммитом будут применяться автоматически, а вам останется только следить за прогрессом.

## CLI {#cli}

### Релизное правило {#release-rules}

Первым делом необходимо создать релизное правило, которое будет описывать применение релизов:

**ya tool dctl put release_rule** [release_rule.yml](https://paste.yandex-team.ru/1025307)
Описанное в примере правило следит за стабильными релизами таска `SAMPLE_RELEASE_TO_YA_DEPLOY_2` и применяет их к стейджу `torkve-test-stage`, обновляя ресурс `server-binary` в `DeployUnit1` ресурсом типа `SAMPLE_RELEASE_INTEGRATION_STATIC` из релиза.


### Создание релизов {#release-creation}

После этого необходимо обновить код своего таска `SAMPLE_RELEASE_TO_YA_DEPLOY_2`, [унаследовав](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/deploy/SampleReleaseToYaDeploy2/__init__.py?rev=6383023#L26) его от специального mixin.

* Если нужен экспорт только в Я.Деплой, то нужно использовать `ReleaseToYaDeployTask2` (для sdk2-задач).
* Если нужен экспорт и в Nanny, и в Я.Деплой, нужно использовать `ReleaseToNannyAndYaDeployTask2`.

{% note warning %}

Порядок перечисления базовых классов важен, `ReleaseToYaDeployTask2` должен идти **первым**.

{% endnote %}

Затем необходимо указать в таске способ получения токена доступа к [YP](https://wiki.yandex-team.ru/yp/). Необходимо использовать роботный токен, чтобы избежать поломки релизной интеграции из-за увольнения пользователя владельца токена. Варианты:

1. Использовать yav:
    * Положить [YP-токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f8446f826a6f4fd581bf0636849fdcd7) в [yav](https://yav.yandex-team.ru/) в поле `yp-token`;
    * [Включить в таске получение секретов из yav](https://wiki.yandex-team.ru/sandbox/yav/);
    * Задать атрибут таска `YP_TOKEN_YAV_SECRET_ID = 'sec-***'`.
1. Использовать [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault): создать Vault с именем `yp_token`, доступ до которого есть у таска;
1. Определить у таска метод `get_yp_oauth_token` и взять секрет из произвольного места.

Почему необходимо указывать токен доступа к YP, ведь в Nanny всё и без этого работало?
В sandbox нет разделения прав на ресурсы, поэтому любой пользователь может собрать любой ресурс и зарелизить его (поправив список releasers, что тоже может сделать любой пользователь). Это даёт возможность покатить такой ресурс всем, кто включил себе автокоммит. Чтобы этого избежать, требуется использование OAuth-токена.

Теперь после очередного запуска таска и релиза его в стейбл можно будет увидеть и новый релиз:

```bash
0 ➜ ya tool dctl list release --sandbox-task-type SAMPLE_RELEASE_TO_YA_DEPLOY_2
+----------------------+------------------------------------+-------------+-----------+--------+--------+
|          ID          |            SandboxTask             | DockerImage | DockerTag | Author | Status |
+----------------------+------------------------------------+-------------+-----------+--------+--------+
| sample-release-2ykcP | SAMPLE_RELEASE_TO_YA_DEPLOY_2 (18) |             |           | guest  | Pending |
-----------------------+------------------------------------+-------------+-----------+--------+---------
```

### Создание релиза командой `ya upload` {#ya-upload}

Чтобы создавать релизы в Деплое через команду `ya upload`, нужно:
1. Завести свой собственный тип ресурса в sandbox, добавив себя и тех, кто должен его релизить, в `releasers` ресурса, и пометив ресурс как `releaseable`;
1. Создать [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault) с именем `yp_token`, доступ до которого будет у пользователя, выполняющего релиз.
1. Позвать приведённую ниже команду
```bash
ya upload <file-path-to-upload> --release {unstable,testing,prestable,stable} --type <resource-type> --owner <sandbox-group>  --release-subject 'My shiny binary new version'
```

### Создание релизов из общих тасков {#common-tasks}

В таске `YA_PACKAGE` поддержан экспорт sandbox-ресурсов (только tar-архивов: deb и rpm не поддерживаются) и докер-образов в Я.Деплой. Чтобы его использовать, нужно:

1. Добавить [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault) с именем `yp_token`, доступ до которого будет из запускаемого таска `YA_PACKAGE`;
1. Выставить у таска `YA_PACKAGE` параметр `release_to_ya_deploy: true`;
1. В зависимости от того, что является результатом сборки: docker-образ или sandbox-ресурс, выполнить описанные ниже действия.

Далее для экспорта docker-образов достаточно зарелизить собранный таск.

Для экспорта sandbox-ресурсов потребуется:

1. Завести свой собственный тип ресурса в sandbox, добавив себя и тех, кто должен его релизить, в `releasers` ресурса;
1. Указать данный тип ресурса в параметре `resource_type` таска `YA_PACKAGE`;
1. Зарелизить таск после сборки.

### Создание релизов для docker-образов {#release-docker}

Для docker нет автоматики, которая бы автоматически создавала релизы для каждого запушенного образа, но пользователь может создавать их сам с помощью dctl:

```
0 ➜ ya tool dctl release docker --title "Optional title" --description "Optional long description" -t 0.2.112 image/name
```
Здесь `0.2.112` — это тег образа, а `image/name` — имя образа (без адреса реестра registry.yandex.net).
Опционально можно указать заголовок и описание релиза, которые будут видны в UI вашего стейджа. Если их не указать, они будут сгенерированы автоматически.

### Создание релизов через API {#release-api}

Релизы являются обычным объектом в модели данных YP и могут создаваться через API [YP](https://wiki.yandex-team.ru/yp/). [Схема данных объекта Release](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/release.proto?rev=6694900#L93). Сейчас пользователей API, работающих с релизами напрямую немного, поэтому в нём могут быть неконсистентности. Поэтому просьба: перед тем, как запускать на постоянку процесс, работающий с API создания релизов, проговорить сценарии и подводные камни с коллегами из ABC-сервиса [https://abc.yandex-team.ru/services/drug](https://abc.yandex-team.ru/services/drug). В будущем эту просьбу мы уберём.

Детали создания релизов через API

1. Объект TSandboxRelease [(поле resources)](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/release.proto?rev=6694900#L57) может содержать [sandbox-ресурсы](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/release.proto?rev=6694900#L35), относящиеся к разным sandbox-таскам. Этот сценарий не поддерживается при создании релиза другими способами, но работает при создании релиза через API.

### Тикет {#ticket}

В соответствии с релизным правилом будет создан и тикет:

```bash
0 ➜ ya tool dctl list deploy_ticket --release-rule torkve-test-release-rule
+--------------------------------------------------+-------------------+-------------------------+--------------------------+---------+
|                        ID                        |       Stage       |         Release         |       ReleaseRule        |  Status |
+--------------------------------------------------+-------------------+-------------------------+--------------------------+---------+
| sample-release-id-2ykcP-torkve-test-release-rule | torkve-test-stage | sample-release-id-2vc0o | torkve-test-release-rule | Pending |
+--------------------------------------------------+-------------------+-------------------------+--------------------------+---------+
```

Поскольку мы не задали в релизном правиле политику автокоммита, оно может быть применено только вручную. Для этого используется команда `commit`:

```bash
0 ➜ ya tool dctl commit deploy_ticket --message "Manually committed by torkve as an example" --reason "EXAMPLE_COMMIT" sample-release-id-2ykcP-torkve-test-release-rule
```

`--message` и `--reason` — это необязательные человеко- и машиночитаемые соответственно описания коммита.

В момент коммита тикет автоматически обновит спецификацию стейджа и выкладка начнётся.
За ходом применения конкретного тикета можно следить при помощи команды `status`:

```bash
0 ➜ ya tool dctl status deploy_ticket -w sample-release-id-2ykcP-torkve-test-release-rule
+--------------------------------------------------+--------+------------+
|                     TicketId                     | Action |   Status   |
+--------------------------------------------------+--------+------------+
| sample-release-id-2ykcP-torkve-test-release-rule | COMMIT | InProgress |
+--------------------------------------------------+--------+------------+
```

## Как применяются релизные правила {#rules-apply}

Релизное правило проверяет для каждого релиза, подходит ли он под все критерии создания тикета. Для Sandbox это:

* тип задачи;
* типы ресурсов в задаче (обязаны присутствовать все перечисленные);
* тип релиза (любой из разрешённых);
* атрибуты ресурса. Это словарь, например `released: "stable", ttl: "inf"`. Необходимо, чтобы был хотя бы один ресурс, содержащий все атрибуты, заданные в правиле.

Для Docker:

* имя docker-образа;
* тип релиза (любой из разрешённых).

Любой из критериев в релизном правиле можно не указывать, но если не заданы типы ресурсов для sandbox-правила, то они будут взяты из патчей (см. ниже).

При совпадении релиза с условиями создаётся тикет на выкладку, содержащий в себе указание на релиз и список патчей из релизного правила.
При этом каждый патч содержит в себе указание:

* **Для Sandbox**:
1. Какой артефакт надо взять из релиза. Если в релизе несколько артефактов этого типа, всегда будет использоваться первый.
1. Тип и адрес изменяемого артефакта в спеке стейджа.
    1. [Статический ресурс](../pod/podagentpayload/resources/staticresource.md) или [слой](../pod/podagentpayload/resources/layer.md), тогда он содержит:
        * Имя deploy unit.
        * Идентификатор статического ресурса или слоя в этом deploy unit.
    1. [Динамический ресурс](../dynamic-resources.md), тогда он содержит:
        * Идентификатор динамического ресурса.
        * Имя деплой-группы ресурса.
* **Для Docker**:
1. Имя deploy unit.
1. Идентификатор бокса.

В момент коммита тикета заданные патчи пытаются примениться к соответствующим местам стейджа. Если по какой-то причине их применить не удаётся — например, если заданный deploy unit или ресурс не существует — то коммит считается неуспешным и вся операция не выполняется.

Важное отличие Docker и Sandbox релизов заключается в том, что если в Sandbox — это всегда задача, которая собирает ≥1 артефакта и эти артефакты могут использоваться как угодно, то в Docker релиз сам по себе уже всегда является единственным артефактом: образом операционной системы. По этой же причине в Docker-патчах указывается только имя бокса, а не какого-то ресурса внутри него: Docker-образ всегда используется в качестве базового слоя бокса, а все перечисленные в боксе слои и ресурсы накладываются уже поверх него.
Для Sandbox, напротив, необходимо сопоставить конкретный артефакт из всех доступных в релизе (для этого используется тип ресурса) с конкретным объектом, который пропатчить (слой, статический или динамический ресурс).

### Автоматически обновляем сервис {#auto-update}

Предположим, что у нас есть Sandbox-задача `BUILD_MY_SERVICE`, которая собирает porto-слой с сервисом `MY_SERVICE_PORTO_LAYER` и ресурс с базой `MY_SERVICE_DATABASE`.

Сервис выложен в Я.Deploy как `my-service-stage` с тремя deploy unit'ами: `sas-testing`, `sas-production` и `man-production`.

> Как можно подключить релизную интеграцию, чтобы сборки автоматически попадали на тестирование и в продакшен?

Первым делом научим сборочную задачу информировать Я.Deploy о релизах. Можно расширить уже имеющуюся задачу, но для простоты мы создадим новую на основе старой:

```python
from sandbox.projects.common.ya_deploy import release_integration

class BuildMyServiceWithDeploy(release_integration.ReleaseToYaDeployTask2, BuildMyService):
    def get_yp_oauth_token(self):
        # OAuth YP-токен робота, от чьего имени будут делаться релизы
        # 'sec-1234...' — идентификатор секрета в Секретнице yav.yandex-team.ru
        # 'yp-token' — ключ токена в секрете
        return sdk2.yav.Secret('sec-1234...').data()['yp-token']

    @property
    def release_template(self):
        subject = 'MyService released!'
        message = textwrap.dedent('''\
            Changelog:
                ** Bugs:
                   * MYSERVICE-XXX: bug1
                ** Features:
                   * MYSERVICE-YYY: feature1
        ''')
        default_emails = ['myservice@yandex-team.ru']
        release_types = ['stable', 'testing']
        
        return sdk2.task.ReleaseTemplate(default_emails, subject, message, release_types)
        
    def on_release(self):
        release_integration.ReleaseToYaDeployTask2.on_release(self, additional_parameters)
        # Если ваш сервис реализует какую-то дополнительную логику при релизе, надо позвать и её:
        # BuildMyService.on_release(self, additional_parameters)
```

Теперь у нас есть таски, которые можно релизить в `testing` или `stable`, при этом они будут создавать соответствующий объект релиза в YP.

Теперь необходимо создать релизные правила, которые в зависимости от типа релиза будут обновлять соответственно testing или stable инсталляцию.

**release-rule-testing.yaml:**

```yaml
meta:
  id: my-service-testing
  stage_id: my-service-stage
  acl:
  - action: allow
    permissions:
    - read
    - write
    - create
    subjects:
    - abc:service:1234
  inherit_acl: true
spec:
  auto_commit_policy:
    type: maintain_active_trunk
  patches:
    # имя патча: может быть произвольным, должно быть уникальным в рамках одного релизного правила, задаётся пользователем
    update-service-layer:
      # тип патча: sandbox или docker
      sandbox:
        # тип используется для выбора артефакта (ресурса) из Sandbox-релиза
        sandbox_resource_type: MY_SERVICE_PORTO_LAYER
        # путь в спеке стейджа, по которому нужно записать артефакт.
        # динамические ресурсы пока не поддерживаются, поэтому здесь всегда указываем static
        static:
          # заменяем слой с id = service-layer в деплой-юните sas-testing
          deploy_unit_id: sas-testing
          layer_ref: service-layer
    update-database:
      sandbox:
        sandbox_resource_type: MY_SERVICE_DATABASE
        static: 
          # заменяем статический ресурс с id = database-resource в деплой-юните sas-testing
          deploy_unit_id: sas-testing
          static_resource_ref: database-resource
  # тип релизов, на которые мы подписаны: sandbox или docker
  sandbox:
    # далее описывается способ выбора Sandbox-релиза, в котором мы заинтересованы
    resource_types:
    - MY_SERVICE_PORTO_LAYER
    - MY_SERVICE_DATABASE
    task_type: BUILD_MY_SERVICE_WITH_DEPLOY
    release_types:
    - testing
    - stable
```

Это правило будет обновлять один deploy unit с тестовой инсталляцией, срабатывая на оба типа релизов. При этом из релиза будут использоваться ресурсы:

1. `MY_SERVICE_PORTO_LAYER` — он будет обновлять слой под названием `service-layer`.
1. `MY_SERVICE_DATABASE` — он будет обновлять статический ресурс под названием `database-resource`.

В соответствии с политикой автокоммита среди ожидающих в очереди релизов будет выбираться самый свежий, а все остальные пропускаться.

{% note warning %}

Если таск вдруг при сборке создаст не все требуемые релизным правилом ресурсы, то правило не сработает! Правило может быть применено только в комплексе и запрещает обновлять сервис «наполовину». Если логика вашего сервиса позволяет независимо обновлять порто-слой и базу, придётся создать два правила, каждое из которых будет обновлять что-то своё.

{% endnote %}

Для продакшена конфигурация будет очень похожая, но патчить надо будет два deploy unit: `sas-production` и `man-production`. Кроме того, настроим политику автокоммита, так чтобы в продакшен выезжали только stable-релизы и при этом выкатывался сразу последний.

**release-rule-production.yaml:**

```yaml
meta:
  id: my-service-production
  stage_id: my-service-stage
  acl:
  - action: allow
    permissions:
    - read
    - write
    - create
    subjects:
    - abc:service:1234
  inherit_acl: true
spec:
  auto_commit_policy:
    type: maintain_active_trunk
  patches:
    update-sas-service-layer:
      sandbox:
        sandbox_resource_type: MY_SERVICE_PORTO_LAYER
        static:
          deploy_unit_id: sas-production
          layer_ref: service-layer
    update-sas-database:
      sandbox:
        sandbox_resource_type: MY_SERVICE_DATABASE
        static:
          deploy_unit_id: sas-production
          static_resource_ref: database-resource
    update-man-service-layer:
      sandbox:
        sandbox_resource_type: MY_SERVICE_PORTO_LAYER
        static:
          deploy_unit_id: man-production
          layer_ref: service-layer
    update-man-database:
      sandbox:
        sandbox_resource_type: MY_SERVICE_DATABASE
        static:
          deploy_unit_id: man-production
          static_resource_ref: database-resource
  sandbox:
    resource_types:
    - MY_SERVICE_PORTO_LAYER
    - MY_SERVICE_DATABASE
    task_type: BUILD_MY_SERVICE_WITH_DEPLOY
    release_types:
    - stable
```

Права на эти релизные правила мы дали одинаковые, только abc-группе с id=1234.
Теперь осталось сохранить эти правила, и все новые релизы будут применяться автоматически:

```bash
0 ➜ ya tool dctl put release_rule release-rule-production.yaml
Put release rule: my-service-production
0 ➜ ya tool dctl put release_rule release-rule-testing.yaml
Put release rule: my-service-testing
```

### Обновляемся при выходе новой версии стороннего компонента {#update-by-component}

Предположим теперь, что команда сервиса X разрабатывает общий компонент и регулярно релизит его новые версии в виде ресурса `X_RESOURCE` в Sandbox. Как сделать так, чтобы мы могли легко и контролируемо обновлять у себя этот компонент в нашем сервисе `my-service`? Создадим правило, которое будет генерировать тикеты на выкатку новых релизов:

**release-rule-my-service-x-component-testing.yaml:**

```yaml
meta:
  id: my-service-x-component-testing
  stage_id: my-service-stage
  acl:
  - action: allow
    permissions:
    - read
    - write
    - create
    subjects:
    - abc:service:1234
  inherit_acl: true
spec:
  auto_commit_policy:
    type: none
  patches:
    update-x-component:
      sandbox:
        sandbox_resource_type: X_RESOURCE
        static:
          deploy_unit_id: sas-testing
          static_resource_ref: x-component
  sandbox:
    resource_types:
    - X_COMPONENT
    release_types:
    - stable
```

{% note warning %}

Данное правило обновляет ресурс с идентификатором `x-component` стабильной версией компонента, но что самое важное, оно не делает это автоматически. Правило создаст только по тикету для каждого релиза, а администратор сможет сам выбрать и применить его, когда захочет:

{% endnote %}


```bash
0 ➜ ya tool dctl list deploy_ticket --release-rule my-service-x-component-testing
+---------------------------------------+------------------+---------+--------------------------------+---------+
|                   ID                  |      Stage       | Release |           ReleaseRule          |  Status |
+---------------------------------------+------------------+---------+--------------------------------+---------+
| x-v1-0-my-service-x-component-testing | my-service-stage | x-v1-0  | my-service-x-component-testing | Pending |
| x-v2-0-my-service-x-component-testing | my-service-stage | x-v2-0  | my-service-x-component-testing | Pending |
| x-v2-1-my-service-x-component-testing | my-service-stage | x-v2-1  | my-service-x-component-testing | Pending |
| x-v3-0-my-service-x-component-testing | my-service-stage | x-v3-0  | my-service-x-component-testing | Pending |
+---------------------------------------+------------------+---------+--------------------------------+---------+
0 ➜ ya tool dctl commit deploy_ticket x-v2-1-my-service-x-component-testing
Committed ticket: x-v2-1-my-service-x-component-testing
```
