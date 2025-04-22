# Sandbox Integration

## Задачи {#goals}

Интеграция тикетов и сервисов Nanny с релизами Sandbox необходима для:

* обеспечения единого механизма учёта и управления выкладками релизов — как выкатывающихся с помощью сервисов Nanny, так и тех, что выкатываются «вручную» (с помощью кубиков и прочих инструментов);
* обеспечения механизма pull request-ов, который заключается в том, что операторы сервисов получают уведомления о новых релизах, но при этом имеют контроль над процедурой «коммита» релиза в описание сервиса и его выкладкой.

## Уведомление Няни о релизе {#release-notification}

Чтобы уведомлять Няню о релизах таска, необходимо подмешать в его класс (пронаследовать) _mixin_ `ReleaseToNannyTask` [код)](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/common/nanny/nanny.py). Сам класс также должен быть отнаследован от `sandboxsdk.SandboxTask`.

{% note warning %}

Для sdk2 необходимо использовать `ReleaseToNannyTask2`.
Метод `on_release` этого миксина отправляет данные в Няню, такие как: тип и идентификатор таска, его описание, статус релиза (stable/prestable/...), поля To и СС.

{% endnote %}


### Схема уведомления о релизе {#release-notification-schema}

Для уведомления о релизе какой-либо компоненты (task'а) Sandbox вызывает удалённый метод `CreateRelease`, передавая в качестве параметров атрибуты:

* `meta` — мета-информация о релизе, в данный момент только набор пар строк `labels`.
* `spec` — описание содержимого релиза.

Например:

```json
{
  "meta": {
      "labels": {
          "prj": "basesearch"
      },
  },
  "spec": {
      "sandboxRelease": {/* release specification */}
  }
}
```
Схема релиза типа sandbox описывается следующим protobuf документом:

```
message SandboxRelease {
    google.protobuf.Timestamp creation_time = 1 [(field_schema.title) = "Creation time"];
    string task_type = 2 [(field_schema.title) = "Task type", (field_schema.maxLength) = 1024];
    string task_id = 3 [(field_schema.title) = "Task identifier", (field_schema.maxLength) = 1024];
    string release_author = 4 [(field_schema.title) = "Release author (login)", (field_schema.maxLength) = 1024];
    string task_author = 5 [(field_schema.title) = "Task author (login)", (field_schema.maxLength) = 1024];
    string desc = 6 [(field_schema.title) = "Release description", (field_schema.maxLength) = 655360];
    string title = 7 [(field_schema.title) = "Release title", (field_schema.maxLength) = 1024];
    string release_type = 8 [(field_schema.title) = "Release type (stable, testing, etc)", (field_schema.maxLength) = 1024];
    repeated string resource_types = 9 [(field_schema.title) = "Resource types", (field_schema.maxLength) = 1024];
    EmailNotifySettings email_notify_settings = 10 [(field_schema.title) = "Email notification settings"];
}
```
который является одним из атрибутов общего объекта релиза:

```
message ReleaseSpec {
    enum Type {
        SANDBOX_RELEASE = 0;
        USER_REQUEST = 1;
        GENCFG_RELEASE = 2;
    }
    string title = 1;
    string desc = 2;
    Type type = 3;
    SandboxRelease sandbox_release = 4;
    UserRequest user_request = 5;
    GencfgRelease gencfg_release = 6;
    repeated string startrek_ticket_ids = 7;
}
```
**Исходный код**: полное описание документа можно найти [в исходном коде](https://bb.yandex-team.ru/projects/NANNY/repos/nanny/browse/nanny/src/protobuf/nanny_tickets/releases.proto).

{% note warning %}

В поле `desc` попадает одно из полей `release_comments`, `task_description` исходного запроса (то, которое первое определено).

{% endnote %}

### Как использовать ReleaseToNannyTask {#using-release-to-nanny-task}

Предположим, что мы наследуем наш таск от стандартного `SandboxTask`. Есть несколько вариантов, как можно использовать `ReleaseToNannyTask`.

* Если `on_release` родительского класса запускать не нужно, можно просто подмешать миксин следующим образом (**порядок перечисления базовых классов важен, `ReleaseToNannyTask` должен идти первым**):

    ```python
    from sandboxsdk.task import SandboxTask
    from projects.common.nanny import nanny
      
    class MyTask(nanny.ReleaseToNannyTask, SandboxTask):
        pass
    ```

* Если `on_release` родительского класса запускать нужно (`SandboxTask.on_release`, например, рассылает email-уведомления), то необходимо явно переопределить этот метод, в котором позвать `on_release` как миксина, так и родительского класса. Порядок перечисления базовых классов в таком случае не важен:

    ```python
    from sandboxsdk.task import SandboxTask
    from projects.common.nanny import nanny
      
    class MyTask(SandboxTask, nanny.ReleaseToNannyTask):
        def on_release(self, additional_parameters):
            # ещё какая-нибудь логика 
            nanny.ReleaseToNannyTask.on_release(self, additional_parameters)
            SandboxTask.on_release(self, additional_parameters)
    ```

Для SDK2

```python
import sdk2
from projects.common.nanny import nanny

class MyTask(nanny.ReleaseToNannyTask2, sdk2.Task):
   def on_release(self, additional_parameters):
        # ещё какая-нибудь логика    
        nanny.ReleaseToNannyTask2.on_release(self, additional_parameters)
        sdk2.Task.on_release(self, additional_parameters)
```

### Интеграция с тикетами Startrek {#startrek-tickets-integration}

Во время вызова `.on_release` извлекает из контекста задачи Sandbox (`self.ctx`) значение ключа `startrek_ticket_ids`, ожидая получить список строк, в котором должны быть перечислены идентификаторы тикетов из Startrek. Например, `['SWAT-2409', 'SWAT-2340']`

#### Логика работы {#startrek-tickets-integration-logic}

На стороне Nanny работает следующая логика:

* Указанный список становится атрибутом **каждого** тикета, созданного для данного релиза.
* При изменении состояния тикетов система асинхронно будет оставлять в указанных тикетах комментарии вида:
    * `Nanny tickets NANNY-169642, NANNY-169643 have been created`
    * `Nanny tickets NANNY-169642, NANNY-169643 have been deployed successfully`


#### Параметр таска в Sandbox {#startrek-tickets-integration-sandbox-parameter}

Для удобства пользователей создан параметр таска в Sandbox `common.nanny.nanny.StartrekTicketIdsParameter`. Его можно использовать для отображения в UI и ручного заполнения пользователем. Параметр принимает на вход строку, которая должна содержать список тикетов Startrek, разделённых запятыми. Например, `SWAT-2409,SWAT-2340`.

#### Настройки авторизации для работы интеграции {#startrek-tickets-integration-authorization}

Для того, чтобы Nanny могла оставлять комментарии, необходимо попросить предоставить такие права для пользователя `nanny-robot`, от имени которого система будет аутентифицирована в Startrek.

### Веб-хуки при закрытии релиза {#release-webhooks}

Во время вызова `.on_release` извлекает из контекста задачи Sandbox (`self.ctx`) значение ключа `webhook_urls`, ожидая получить список строк, в котором должны быть перечислены url веб-хуков, которые будут вызваны при закрытии релиза в Nanny.
Например, `['http://yandex.ru/post_release/', 'http://ya.ru/send_release_info/']`
Проверить результат работы webhooks можно через API или в браузере. Обратившись по адресу:

```
https://nanny.yandex-team.ru/api/tickets/GetRelease/?releaseId=<ID релиза>
```

Например:

```
https://nanny.yandex-team.ru/api/tickets/GetRelease/?releaseId=SANDBOX_RELEASE-221535146-TESTING
```

Для работы веб-хуков нужен доступ от сети `_SWAT_NETS_` до желаемого fqdn/макроса. [Пример заказанного доступа через Puncher](https://puncher.yandex-team.ru/?id=60530b5c601b4f84ea495270)

#### Логика работы {#release-webhooks-logic}

На стороне Nanny работает следующая логика:

* Указанный список становится атрибутом релиза.
* При закрытии релиза (статус `CLOSED`), на каждый URL из списка будет отправлен POST-запрос.
* Хук повторно выполняется при 400-х и 500-х кодах ошибки. После 3-х неудачных попыток хук помечается невыполненным и пропускается, текст ошибки будет сохранен.
* Вебхуки также сработают, если в закрытом релизе один из тикетов перейдет в статус `DEPLOY_SUCCESS` или из статуса `DEPLOY_SUCCESS` в любой другой.

Содержимое тела запроса зависит от выбранного типа (формата) хука:

* `RELEASE_ONLY` — json-представление релиза

```json
{  
   "status":{  
      "status":"CLOSED",
      "comment":"All tickets are closed (number of tickets: 30).",
      "author":"nanny-robot",
      "webhook":[  

      ],
      "postProcessing":{  
         "isFinished":true,
         "timestamp":"2017-04-10T15:41:02.590Z",
         "hostname":"fol1-0509.search.yandex.net"
      },
      "endTime":"2017-04-10T18:59:27Z"
   },
   "meta":{  
      "creationTime":"2017-04-10T15:40:50Z",
      "author":"nanny-robot"
   },
   "id":"SANDBOX_RELEASE-101906171-STABLE",
   "spec":{  
      "sandboxRelease":{  
         "title":"report-templates\/r1226\/serp\/web4@v1.103.0",
         "releaseType":"stable",
         "releaseAuthor":"robot-serp-bot",
         "creationTime":"2017-04-10T15:40:50Z",
         "emailNotifySettings":{  
            "cc":[  

            ],
            "to":[  
               "sanity",
               "binarycat",
               "mobile-search-releases"
            ]
         },
         "resourceTypes":[  
            "REPORT_TEMPLATES_PACKAGE"
         ],
         "taskId":"101906171",
         "taskType":"REPORT_TEMPLATES_DOWNLOAD",
         "taskAuthor":"",
         "resources":[  
            {  
               "description":"Report templates for project all, version: r1226",
               "skynetId":"rbtorrent:1747541bab58ac53c3526f4b57e27f2a60b41584",
               "arch":"any",
               "httpUrl":"http:\/\/sandbox-storage21.search.yandex.net:13578\/resource\/242111367\/report-templates--join-tc-5957626.tar",
               "fileMd5":"276bd301c7e511467675bb74a5124e80",
               "releasers":[  
                  "alex-k",
                  "shoihet",
                  "sanity",
                  "rudeshko",
                  "robot-serp-bot"
               ],
               "type":"REPORT_TEMPLATES_PACKAGE",
               "id":"242111367"
            }
         ],
         "desc":"release description"
      },
      "title":"report-templates\/r1226\/serp\/web4@v1.103.0",
      "webhook":[  

      ],
      "startrekTicketIds":[  

      ],
      "type":"SANDBOX_RELEASE",
      "desc":"release description"
   }
}
```


* `RELEASE_WITH_TICKETS` — JSON документ следующего вида 

```json
{
"release": {},
"tickets": [{ticket...}]
}
```

где `ticket` — это json представление тикета, например

```json
{
  "id": "NEWS-2088664",
  "meta": {
    "annotations": {},
    "author": "nanny-robot",
    "ctime": "2017-06-27T05:59:57Z",
    "mtime": "2017-06-27T05:59:57Z"
  },
  "spec": {
    "cc": [],
    "desc": "",
    "intervals": [],
    "isUrgent": false,
    "queueId": "NEWS",
    "releaseId": "SANDBOX_RELEASE-122359409-STABLE",
    "responsible": "feliksas",
    "serviceDeployment": {
      "serviceId": "amp_related_news_uploader",
      "setSnapshotStateId": "",
      "snapshotId": "baa36af4e4cf84ce39bd04a1078aa69499deed16"
    },
    "startrekTicketIds": [],
    "taskgroupId": "",
    "title": "amp_related_news_uploader: Automatic release (stable)"
  },
  "status": {
    "lastTransitionTime": "2017-06-27T05:59:57.192Z",
    "status": "COMMITTED"
  },
  "uniqueId": "de936b867892506d0674ab4c4fdaf33f18c50f76"
}
```

#### Параметры таска в Sandbox {#release-webhooks-sandbox-parameters}

Для ручного заполнения пользователем созданы параметры таска в Sandbox

* `common.nanny.nanny.WebHookUrlParameter`, `common.nanny.nanny.WebHookUrlParameter2` для sdk2
    Принимает на вход список строк — URL'ов.
* `common.nanny.nanny.WebHookTypeParameter`, `common.nanny.nanny.WebHookTypeParameter2` для sdk2
    Позволяет выбрать формат payload'а.

![img](https://jing.yandex-team.ru/files/sshipkov/webhook-type-ui.8dc6605.png)

* `common.nanny.nanny.LabelsParameter`, `common.nanny.nanny.LabelsParameter2` для sdk2
    Позволяет указать `labels`, которые будут указаны у всех релизов таска.
    Так же можно самостоятельно выставлять label'ы в `ctx` таска, используя ключ `common.nanny.nanny.LABELS`.

Пример использования labels в sdk2:

```python
  from sandbox.projects.common.nanny import nanny
  from sandbox import sdk2


  class TaskParameters(sdk2.Parameters):
      ### задать лейблы через UI sandbox
      release_labels = nanny.LabelsParameter2('nanny release labels')
      ### или, например, так
      release_labels = {'param1': 'val1', 'param2': 'val2'}


  class BuildTask(nanny.ReleaseToNannyTask2, sdk2.Task):
      """
      Build task.
      """
      Parameters = TaskParameters
```

В фильтре настроек тикетной интеграции labels можно проверять так:
![img](https://jing.yandex-team.ru/files/sshipkov/Screenshot%202019-10-21%20at%2021.00.07.f3eaaaf.png)

### Что происходит, когда Няня узнает о релизе от Sandbox {#release-processing}

Информация о релизе, посланная в Няню, порождает релиз типа `SANDBOX_RELEASE` [список всех релизов](https://nanny.yandex-team.ru/ui/#/release_requests/).
Затем происходит несколько процессов.

##### Матчинг по сервисам {#release-rules-matching-service}

Для каждого из [сервисов](https://nanny.yandex-team.ru/ui/#/services/), для которых:

* включена интеграция с тикетами (чекбокс **Enable release requests integration** в секции **Information** → **Tickets Integration**).
* указана очередь (поле **Deploy queue to put deploy tickets into** в секции **Information** → **General**).

Няня смотрит на каждое из **release rules** секции **Information** → **Tickets Integratio** сервиса, **(НЕ на sandbox files сервиса)** и создаёт тикет, если для одного из release rules выполняются условия:
* тип таска равен типу таска релиза или не указан.
* тип ресурса содержится в релизе или не указан.
* релиз подходит под фильтр, указанный в правиле.

При выполнении указанных выше условий **будет создан тикет на выкладку**.

После этого появляется возможность [вкоммитить в сервис изменения](#service-tickets), связанные с этим тикетом.

{% note alert %}

В момент коммита тикета, в сервисе будут записаны новые версии **всех** типов ресурсов, присутствующих одновременно в релизе и в сервисе, независимо от того, из какого release rule был создан данный тикет.

{% endnote %}

###### Пример 1

1. В сервисе есть release rule, с указанным ресурсом `A`;
1. В сервисе есть sandbox files с типами ресурса `A` и `B`;
1. Появляется релиз, в котором указаны типы ресурса `A`, `B`, `C`;
1. При этом будет создан тикет на выкладку для данного сервиса;
1. При коммите из данного тикета будет обновлены версии **обоих ресурсов: `A` и `B`**.

###### Пример 2

1. В сервисе есть release rule, с указанным ресурсом типа `A` и типом таска `T`;
1. В сервисе есть sandbox files с ресурсом типа `A` таска типа `T` и ресурсом типа `A` таска типа `Z`;
1. Появляется релиз таска `T`, в котором указан тип ресурса `A`;
1. При этом будет создан тикет на выкладку для данного сервиса;
1. При коммите из данного тикета будет обновлены версии **обоих ресурсов: относящихся к таску типа `T` и типа `Z`**.

Настройка очереди:
![img](https://jing.yandex-team.ru/files/sshipkov/Screen%20Shot%202015-11-20%20at%2013.04.19.b6e6f80.png)

Настройка сервисных релизных правил:
![img](https://jing.yandex-team.ru/files/sshipkov/ti_settings.606b34f.png)

При срабатывании правила система создаёт тикет и опционально может:

* Указать срочность тикета (_ticket priority_).
* Внести изменения в сервис "Enable auto commit".

Выставив при этом приоритет полученной ревизии (приоритеты используются для автоматической выкладки)

![img](https://jing.yandex-team.ru/files/sshipkov/snapshot_priority.17fa9c0.png)

Правило тикетной интеграции можно поставить на паузу. Для этого нужно выставить `Pause rule to cancel all created tickets`.

![img](https://jing.yandex-team.ru/files/sshipkov/ti_pause.4b73dab.png)

После этого все тикеты, созданные по правилу, которое поставлено на паузу, будут сразу переходить в состояние `CANCELLED`. Даже если для такого правила включён `Enable auto commit`, коммит для тикетов выполнен не будет.

Полный [список существующих очередей](https://nanny.yandex-team.ru/ui/#/queues/).

Страница [создания очереди](https://nanny.yandex-team.ru/ui/#/queues/create-queue/).

##### Матчинг по очередям {#queues-matching}

Для каждой очереди из [списка](https://nanny.yandex-team.ru/ui/#/queues/) происходит следующее. Каждое из её правил (**release rules** в UI) применяется к только что созданному релиз-реквесту и, если хотя бы одно правило вернуло истинное значение, в очереди создаётся тикет, привязанный к релиз-реквесту.
На данном шаге используются только правила с нормальным приоритетом (те, у которых не стоит чекбокс **Is low priority**).

##### Матчинг по низкоприоритетным правилам {#low-priority-queue}

В случае, если релиз-реквест не породил ни одного тикета в предыдущих шагах, повторяется шаг «матчинг по очередям», но с использованием низкоприоритетных правил (тех, у которых стоит чекбокс **Is low priority**). Этот механизм используется для создания тикетов в мусорной очереди [DENVULL](https://nanny.yandex-team.ru/ui/#/queues/DENVULL/) (meant to be DEVNULL), где они автоматически закрываются сразу после создания.

### Тикеты, привязанные к сервисам {#service-tickets}

В тикете, [привязанном к сервису](#release-rules-matching-service), можно в нажатие одной кнопки выкатить или закоммитить изменения в описание сервиса (то есть, обновить идентификатор Sandbox-таска у сматченных файлов).
Активация приведёт к фиксации изменений в случае, если тикет ещё не был закоммичен, и выставлению полученной ревизии в качестве активной.
Во время выкладки тикет будет автоматически обновляться, отражая процесс выкладки, после чего будет закрыт.

![img](https://jing.yandex-team.ru/files/sshipkov/2018-04-20_18-52-30%202.84926e5.png)

### Поиск и закрытие дублей {#release-duplicates-find-and-close}

Для работы с дублями релизов используются следующие параметры

* необязательный `component` (значение по умолчанию `''`):
* в sandbox SDK1: `self.ctx.get('component')`;
* в sandbox SDK2: `common.nanny.nanny.ComponentParameter`.
* необязательный `duplicate_policy_type` (значение по умолчанию `'IGNORE'`):
* в sandbox SDK1: `self.ctx.get('duplicate_policy_type')`;
* в sandbox SDK2:`common.nanny.nanny.DuplicatePolicyTypeParameter`.
Валидные значения: `'CLOSE_AS_DUPLICATE'`, `'IGNORE'`
Оба эти параметра копируются в поле `spec` релиза в Няне.

#### Логика работы {#release-duplicates-logic}

Релиз `A`  дублирует релиз `B` если:

* `A.spec.duplicate_policy_type == 'CLOSE_AS_DUPLICATE'`;
* `A.spec.type == SANDBOX_RELEASE` и `B.spec.type == SANDBOX_RELEASE` (пока поиск дублей работает только для Sandbox релизов);
* `A.spec.component == B.spec.component` (на основе поля `component` происходит поиск дублей);
* `A.status == OPEN` (автоматически закрываем только открытые релизы);
* все тикеты релиза `A` находятся в терминальных статусах, либо в статусе `IN_QUEUE`. При этом хотя бы один тикет должен быть в статусе `IN_QUEUE` (это условие необходимо для дополнительной проверки, что релиз действительно открыт).
Если все вышеперечисленные условия выполняются, то на этапе постпроцессинга релиз `A` будет закрыт в пользу релиза `B`.

### Как настроить автодеплой {#auto-deploy-setup}

В случае, если тикет создан в результате срабатывания сервисного правила (cм. секцию [матчинг по сервисам](#release-rules-matching-service)), у которого нажата галочка **Enable auto commit**, тикет будет автоматически закоммичен сразу после создания.

Используя [Maintain active trunk](../reference/service-scheduling.md#maintain-active-trunk) в качестве политики выкладки (секция **Information** → **Scheduling Policy**), можно добиться того, что снапшоты рантайм-атрибутов, создаваемые в результате автоматических коммитов, будут также и автоматически активироваться.

{% note warning %}

Как внесение изменений в описание сервиса, так и активация полученных снапшотов производятся от имени nanny-robot@, поэтому он должен быть присутствовать в списках conf- и ops-менеджеров сервиса (см. секцию Administration).

{% endnote %}

## Автодеплой the old way {#auto-deploy}

Логику автодеплоя можно воспроизвести на стороне Sandbox-таска, например, используя `projects.common.nanny.NannyClient`.

`NannyClient` имеет два метода с одинаковой сигнатурой:

* `update_service_sandbox_file` — для обновления Sandbox-файла сервиса;
* `update_service_sandbox_bsc_shard` — для обновления шарда.

Пример использования:

```python
from projects.common.nanny import nanny

class BuildSomething(nanny.ReleaseToNannyTask, SandboxTask):
    def on_release(self, additional_parameters):
        nanny.ReleaseToNannyTask.on_release(self, additional_parameters)
        nanny_client = nanny.NannyClient(api_url='http://nanny.yandex-team.ru/',
                                         oauth_token='...')
        nanny_client.update_service_sandbox_bsc_shard(
            service_id='production_something',
            task_type=self.type,
            task_id=str(self.id),
            deploy=False  # или True, если хочется не только обновить описание,
                          # но и тут же выложить сервис
        )
```

## Аутентификация {#authentification}

Для выполнения любого запроса в API Няни необходимо использовать **OAuth-токен**, который можно получить [в UI Няни](https://nanny.yandex-team.ru/ui/#/oauth). Рекомендуем рассмотреть подход к хранению токена в [Sandbox Vault](https://sandbox.yandex-team.ru/admin/vault).

## Авторизация {#authorization}

Все изменения в сервисах, выполняемые из тасков Sandbox, так же как все остальные проходят процедуру авторизации. Пользователь, чей токен используется, должен быть перечислен в разделе Administrators сервиса и иметь следующие роли:

* **Configuration managers** — для внесения изменений без выкладки.
* **Operation managers** — для запуска выкладки новой ревизии (snapshot'а) сервиса.

