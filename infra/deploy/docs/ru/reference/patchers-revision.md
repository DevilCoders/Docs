# Runtime version (ревизия схемы патчеров)

## Мотивация {#motivation}

Одной из самых приоритетных задач команды Deploy является задача обеспечения надежности и предсказуемости выкладок.
Доминирующим всегда оставался вызов — как выкатывать релиз stagectl, при этом иметь возможность управлять распространением фичей, которые есть в релизе.

{% cut "История" %}

**Первый подход (Начало)**
В конфиге stagectl был bool флаг включения фичи и блэклист стейджей, куда фичу точно выкатывать нельзя.

Все стейджи, которые выкатились после включения флага, начинали обрабатываться новой версией, в случае проблем необходим откат флага через релиз конфига.
После отката все стейджи, которые получили фичу, после следующей выкладки её потеряют.

**Второй подход (Лейблы)**
Решили, что можно более точечно управлять, повесить лейбл на определенный стейдж, и тогда там, где лейбл есть, фича применится. Или наоборот, где нет лейбла, применится.
А где-то лейбл будет перетерт...

{% endcut %}


## Runtime version (ревизия схемы патчеров) {#runtime-version}

В stage появилось [поле](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/stage.proto?rev=r7899759#L228), куда можно указать [Runtime version (ревизию схемы патчеров)](https://wiki.yandex-team.ru/deploy/dev/designdocs/stage/patchers-versioning/), stagectl будет обрабатывать стейдж в соответствии с указанной ревизией.

Накатывать и откатывать фичи можно с гранулярностью до DeployUnit.

Для отката runtime version (ревизии схемы патчеров) в любом стейдже нужно просто указать желаемую ревизию.
Все изменения, которые вызывают переаллокацию, рестарт, сильно меняют поведение — будут релизиться через runtime version (ревизии схемы патчеров).

{% note info %}

Stagectl хранит более десяти предыдущих ревизий.

{% endnote %}

Runtime version можно обновлять автоматически, вместе с [сайдкарами](../concepts/pod/sidecars/sidecars.md#updates).

## Runtime version №14 {#runtime-version-14}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

##### Новая функциональность {#new-runtime-version-14}

* Изменили `liveness_limit_ratio` по умолчанию:
    
    было: 
    `liveness_limit_ratio=0.35` — endpoint создавался по определенным [правилам](../concepts/service-discovery.md#endpoint-lifecycle).

    стало: 
    `liveness_limit_ratio=1.0` — endpoint будет создан для каждого pod'а, независимо от его статуса. 
    В таком случае решать, куда слать/не слать трафик, можно на клиентском уровне.

* Включили отгрузку [системных логов](https://deploy.yandex-team.ru/docs/logs/system-logs?searchQuery=Системны) по умолчанию:
    
    Системные логи содержат события хуков (start, stop, destroy, liveness, readiness, init) для пользовательских ворклоудов и боксов.

* Добавили возможность обновлять coredump через механизм [обновления сайдкаров](../concepts/pod/sidecars/sidecars.md#updates): доступно через [yaml редактор](https://a.yandex-team.ru/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r9631093#L257).
* [SecretEnv](../launch/sox-service.md#secret-env-get) и [childOnly](../launch/sox-service.md#child-only) теперь выставляются по умолчанию:
    
    {% note info %}
    
    Можно отключить через обращение в rtcsupport.

    {% endnote %}

## Runtime version №13 {#runtime-version-13}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

##### Новая функциональность {#new-runtime-version-13}

* Добавлены переменные для конфигурации отправки сообщений в ErrorBooster:
     
    `ERROR_BOOSTER_HTTP_PORT`
    `ERROR_BOOSTER_HTTP_HOST`

## Runtime version №12 {#runtime-version-12}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

##### Новая функциональность {#new-runtime-version-12}

* Добавлены переменные для конфигурации отправки сообщений в ErrorBooster:
   
    `ERROR_BOOSTER_SYSLOG_HOST`
    `ERROR_BOOSTER_SYSLOG_PORT`
    `ERROR_BOOSTER_SENTRY_DSN`

#### Исправления {#fix-runtime-version-12}

* Исправили резерв тредов на инфраструктуру.

    В поде доступно примерно 9000 тредов. Треды делятся между боксами если лимит на боксы явно не задан.

* Исправили имена box сайдкаров.
   
    В именах box заменили `_` на `-`. Это нужно для правильной работы ssh ссылки из web интерфейса.

* Исправили обработку sox стейджей.
   
   При использовании runtime version > 7, readonly монтирование могло работать некорректно.


## Runtime version №11 {#runtime-version-11}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

##### Новая функциональность {#new-runtime-version-11}

* Изменено создание туннеля для L3-балансера:

    Изменение действует только для туннеля, заданного через:

    - UI (`Deploy unit settings (Form) / Network settings / Virtual service id`)
    - dctl: `deploy_unit.network_defaults.virtual_service_id`([прото-схема](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8647731#L151))

    Было:
    Туннель прокидывался независимо от интерфейса (`fastbone` / `backbone`).
    
    Стало:
    Туннель прокидывается только для `backbone` интерфейсов.

#### Исправления {#fix-runtime-version-11}

* Исправили отображение доступных Box'y ресурсов.

    Лимиты для Box'ов **без заданных лимитов** отображались некорректно при просмотре через **переменные окружения** и **cgroupfs**.

    Было:
    Показывались лимиты Dom0 системы.
    
    Стало:
    Для пользовательского приложения будут видны лимиты Pod.

## Runtime version №10 {#runtime-version-10}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

##### Новая функциональность {#new-runtime-version-10}

* Скрипт инициализации Juggler теперь падает при неуспешной распаковке ресурсов и других ошибках.

* Конфигурация TVM прокидывается в ворклоады в переменную окружения `DEPLOY_TVM_CONFIG`.

    Конфигурация прокидывается без секретов для обеспечения требования безопасности.


## Runtime version №9 {#runtime-version-9}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

##### Новая функциональность {#new-runtime-version-9}

* Изменено наследование специальных переменных окружения из бокса в ворклоад.

    Специальными переменными окружения являются `PATH`, `HOME`, `USER`.

    {% note info %}

    Описанные изменения актуальны только при отсутствии пользовательских значений для специальных переменных в ворклоаде.

    {% endnote %}

    Было: специальные переменные заполнялись значениями из Porto вместо значений из бокса.

    Стало: специальные переменные прокидываются из бокса в ворклоад; Porto заполняет их только при отсутствии значения в боксе.

* В unistat-метрики добавлен тег `workload` — идентификатор ворклоада.

  Было: ранее были только теги для Stage и Deploy unit, для сбора метрик с заданного ворклоада необходимы были кастомные теги.

  Стало: при отсутствии пользовательского тега с именем `workload` данный тег заполняется идентификатором ворклоада.

## Runtime version №8 {#runtime-version-8}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

#### Новая функциональность {#new-runtime-version-8}

* Включение `ip_limit`.

    Запрещает использовать сети в контейнере отличные от того, что установлено в секции ip (то что запросил пользователь). Является частью требований по безопасности.

* Включение флагом `extra_routes` без nat64.

    Включает пониженный MTU для хождения в дикий интернет для тех, у кого нет nat64.
    Для использования необходимо включить:
    ```yaml
    spec:
        deploy_units:
            deployUnit:
            -----
            multi_cluster_replica_set:
                -----
                pod_template_spec:
                    spec:
                    network_settings:
                        extra_routes: true <==

            ----
            patchers_revision: 8  <==
        ----
    ```


## Runtime version №7 {#runtime-version-7}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

#### Новая функциональность {#new-runtime-version-7}

* Изменение логики приноса системных папок и вольюмов для writable папок в случае использования read only fs бокса.

    Было: в случае readonly rootfs бокса было невозможно примонтировать вольюм к несуществующей папке, соответственно такие папки должны были приноситься слоями в пользовательский бокс.

    Стало: в случае readonly rootfs бокса спека пользователя автоматом обогащается слоями с системными папками и необходимыми вольюмами для writable папок для deploy sidecars (pod_agent, logbroker, coredump, logrotate, dru, juggler).

* Поменялись лимиты по логам:

    Лимиты задаются **для деплой юнитов** по двум параметрам:

    1. Передаваемый объем в секунду.
    2. Количество сообщений в секунду.

    Было: объем: 1 терабайт, сообщений: 100500.
    Стало: объем: 15 мегабайт, сообщений: 20000.

    **Прежние** лимиты сохранились для Deploy Unit с **хотя бы одним** из следующих условий:

    1. Используется кастомный топик.
    2. Не указана версия Unified Agent (поле `logbroker_tools_sandbox_info`).
    3. Версия Unified Agent ниже 2249562029.

    Для Deploy Unit, которые за период 05.07.21 — 05.08.21 превысили 90% от новых лимитов хотя бы по одному параметру, введены **специальные** лимиты — максимум из нового лимита и х2 от максимального зафиксированного за период значения.

    {% note warning %}

    Данные лимиты применяются **на всех runtime version**, но **не применяются** при выполнении хотя бы одного из условий для **прежних** лимитов.

    {% endnote %}

    Полный список Deploy Unit со специальными лимитами представлен по [ссылке](https://paste.yandex-team.ru/5383186). Unit'ы заданы в формате `stage_id.du_id` и отсортированы в алфавитном порядке.

* Поменялось значение по умолчанию для `DeployUnit.anonymous_memory_limit`.

    Было: `DeployUnit.MemoryLimit — 128Mb`
    Стало: `DeployUnit.MemoryLimit — Min(128Mb, DeployUnit.MemoryLimit * 10%)`

    То есть для маленьких подов (RAM < 1.2Gb) уменьшили зазор для файловых кешей. Для больших подов осталось без изменений.

    Это изменение затрагивает только те DeployUnit, в которых пользователем не выставлен `DeployUnit.AnonymousMemoryLimit`.


## Runtime version №6 {#runtime-version-6}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

#### Новая функциональность {#new-runtime-version-6}

* Выставление лимитов анонимной памяти для сайдкаров [DEPLOY-4422](https://st.yandex-team.ru/DEPLOY-4422).

* Возможность сбора портометрик с системных сайдкаров [DEPLOY-4649](https://st.yandex-team.ru/DEPLOY-4649).
  
  Если выставить [флаг](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/stage.proto?rev=r8516331#L242) для DeployUnit'a, то с инфраструктурных сайдкаров в нём начнут собираться портовоклоадные метрики со следующими itype:
  ```
  deploy_sidecar_tvm
  deploy_sidecar_logs
  deploy_sidecar_dru
  deploy_sidecar_juggler
  ```

#### Исправления {#fix-runtime-version-6}

* Не перетирается `NODE_FILTER` для sox-сервисов [DEPLOY-4761](https://st.yandex-team.ru/DEPLOY-4761).

## Runtime version №5 {#runtime-version-5}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

#### Новая функциональность {#new-runtime-version-5}

* `extra_routes` выставляется для пода по умолчанию.
  
  Включаются автоматически дополнительные настройки роутинга, касается только окружений у которых есть настройки **ResolvConf**.
  
  При использовании NAT64 для похода во внешние сети будет использоваться MTU 1450, вместо 8910.

* `ip_limit` выставляется для пода по умолчанию.
  
  Включается автоматически для всех. Является частью мер по безопасности.


## Runtime version №4 {#runtime-version-4}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

#### Новая функциональность {#new-runtime-version-4}

* Добавлены переменные окружения с тэгами из YASM Monitoring (itype,ctype,prj, ...).
  
  Подробнее про настройку мониторинга: [Monitoring in YASM](../how-to/monitorings/settings). Все переменные окружения имеют префикс `YASM_` за которым идет имя тэга в верхнем регистре.
  ```
  YASM_DEPLOY_UNIT=deployUnit
  YASM_ITYPE=stagectl_test_itype
  YASM_PRJ=test-stage1.deployUnit.workload
  YASM_CUSTOM_TAG=my_tag
  ```


* Добавлены переменные окружения со списком лимитов из спецификации DeployUnit/Box/Workload.
  
  Если лимит не выставлен используется значение 0. Для лимитов по памяти значение в байтах. Для VCPU в виртуальных микроядрах (также как в спеке). При деплое количество доступных ядер может быть пересчитано, в зависимости от того на какой хост заселяется Pod. Честное значение для CPU будет добавлено после [PORTO-870](https://st.yandex-team.ru/PORTO-870), [DEPLOY-4407](https://st.yandex-team.ru/DEPLOY-4407).

  Список переменных:
  ```
  DEPLOY_VCPU_GUARANTEE
  DEPLOY_VCPU_LIMIT
  DEPLOY_MEMORY_GUARANTEE
  DEPLOY_MEMORY_LIMIT
  DEPLOY_ANONYMOUS_MEMORY_LIMIT
  DEPLOY_THREAD_LIMIT
  ```

#### Исправления {#fix-runtime-version-4}

* Изменение порядка переопределения переменных окружения при сборке пода из Docker образа.
  
  Переменные окружения можно задавать на различных уровнях (например добавить в Box, тогда переменная появится во всех Workload'ах данного Box'a). На каждом следующем уровне иерархии объектов есть возможность переопределить значение переменной окружения, созданной на родительском уровне. В случае, когда пременная окружения пристутствует в Docker образе, то порядок переопределения будет начиная с 4-й ревизии патчеров таким: **Stage 🠖 DOCKER_IMAGE 🠖 Box 🠖 Workload** Т.е. если переменная с одинаковым именем присутствует и в Docker образе и в Box, то приоритет отдается значению из Box.

## Runtime version №3 {#runtime-version-3}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

#### Новая функциональность {#new-runtime-version-3}

* `anon_memory_limit` выставляется для пода по умолчанию.

  Если не задан `anon_memory_limit`, то заполняем его для pod-а автоматически: `non_memory_limit = memory_limit - 128`.

  Под файловый кеш резервируется 128 MiB. Это означает, что OOM будет наступать раньше, но поды будут работать более предсказуемо.

* [tvm_config](../concepts/pod/sidecars/sidecars#quotas):
    * `cpu_limit` берется из спеки;
    * пользовательские значения `cpu` и `memory` используются, даже если они меньше дефолтных.

* [Dynamic resource](../concepts/pod/sidecars/sidecars#quotas): использует дополнительную квоту **0.1 CPU**, **128 MB**.


#### Исправления {#fix-runtime-version-3}

* По умолчанию для пода выставляется `persistent fqdn` вместо `transient`.
    Например, если в поде выполнить команду `hostname`:
    
    Было: `sas3-8740-1.4iojwzkhozvwlvjn.sas.yp-c.yandex.net`
    
    Стало: `4iojwzkhozvwlvjn.sas.yp-c.yandex.net`

## Runtime version №2 {#runtime-version-2}

{% include notitle [patcher-revision-alert](../_includes/patcher-revision-alert.md) %}

#### Новая функциональность {#new-runtime-version-2}

* Добавляет 2 переменных окружения `DEPLOY_DOCKER_HASH` и `DEPLOY_DOCKER_IMAGE`.

  Добавляет 2 переменных окружения, вида:

  ```
  DEPLOY_DOCKER_HASH=sha256:0468f73632331064dde1b763a09c7760179cc5692255d62394b60bc42f385e0b
  DEPLOY_DOCKER_IMAGE=registry.yandex.net/rtc-base/bionic:stable
  ```
  
  Добавляет в Box, использующий Docker образ, и все Workload'ы этого Box'а. В Box'ах, не использующих Docker, данные переменные отсутствуют.

* Содержимое докеров обновляется при каждой выкладке, вместо похода в кеш.

  При любом изменении версии спеки DeployUnit'a будет проверка, не поменялся ли docker image в реестре по данному тэгу. Например, если пользователь перезалил образ по тэгу `stable`, то при деплое будет раскатана **самая свежая версия из docker registry** по данному тэгу. Сама по себе перезаливка нового образа в реестр по тому же тэгу к автоматической перевыкладке не ведет (перевыкладка только **после** обновления ревизии DU по любым причинам).

* Поддержали нескольких juggler bundle.


#### Исправления {#fix-runtime-version-2}

* Исправили проблему неправильного деплоя docker образов, когда внутри одного DeployUnit в 2х разных Box'ах используются одинаковые Docker образы с разными тэгами.
    
  Изменилась схема генерирования идентификаторов каждого слоя.

* При включенном juggler у пода выставляется persistent fqdn вместо transient.

* Исправлено выставление дисковой квоты на juggler workload.

  Теперь выставляется [512MB HDD на каждый box](../concepts/pod/sidecars/sidecars#quotas).

  Суть проблемы: дополнительная квота по hdd space приплюсовывалась к рутовой дисковой аллокации (в случае использования изоляции дисковая аллокация с под агентом является рутовой) вместо дисковой аллокации пользователя.

## Runtime version №1 {#runtime-version-1}

Она же `Default` — самая старая версия, надо обновлять.

