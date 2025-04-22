# Infrastructure models. Part 3.
На примере Terraform'а мы посмотрели на инфраструктуру как систему и отметили трудности реализации системы _в целом_. В этой части рассмотрим на несколько другой подход и реализацию в виде Kubernetes и то, как он решает задачи пользователей и провайдеров.

# Infrastructure as data
Описать этот подход можно так:
>Declarative configuration is about treating infrastructure as data, which is more portable than code, and enables workflows that manipulate desired state based on policy, while serializing the results between each step of the pipeline.
>Data can easily be imported and manipulated by other tools, written in any language, and then version controlled and rolled out programmatically.

[twitter.com/kelseyhightower](https://twitter.com/kelseyhightower/status/1164194470436302848?lang=en)

Если сравнивать с infrastructure as code: у нас есть данные, с которыми может работать (редактировать и генерировать) _разный код_. Это могут быть:
  * системы контроля версий
  * текстовые редакторы и IDE
  * UI с формами
  * автоматизированные системы (например, анализа уязвимостей)
  * самое интересное: управляющие циклы (control loops) на стороне провайдера

Такой подход позволяет обновлять и заменять (даже полностью переписывать!) код независимо, не меняя описание инфраструктуры. Это в теории, давайте посмотрим на реализацию подхода в kubernetes.

Important: когда слышишь _kubernetes_, то приходят аналогии с Nanny, Deploy, YP. И это совершенно верные ассоциации. Проект начинался и во многом развивается как система управления кластерами, т.е. включает в себя планирование ресурсов, оркестрирование и запуск пользовательских контейнеров в pod'ах на различных ОС. **Но** k8s это уже давно гораздо больше: это **второй** после ядра Linux проект по количеству участников [[link]](https://twitter.com/celeste_horgan/status/1390590058835496960) и даёт ОГРОМНУЮ экосистему проектов, подходов и применений. Относительно новым является использование kubernetes в качестве universal control plane - реализацию подхода infrastructure as data. Основные облачные провайдеры уже представляют такие сервисы:
  * Google даёт официальный контроллер (но закрытый код) для управления GCE: [config-connector](https://github.com/GoogleCloudPlatform/k8s-config-connector)
  * Microsoft даёт официальный контроллер для Azure: [azure-service-operator](https://github.com/Azure/azure-service-operator)
  * Для AWS очень активно пишетcя набор отдельных операторов (сотрудниками Amazon): [aws-controllers-k8s](https://github.com/aws-controllers-k8s)

Это молодая, но активная область поиска удобных инженерных решений. Давайте познакомимся с ней.

# Kubernetes Resource Model
Начнём с модели ресурсов. Большое и подробное описание есть в [design-proposals/architecture/resource-management.md](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/architecture/resource-management.md). Если совсем бегло, то у нас объекты, изменения в которых можно [эффективно отслеживать](https://kubernetes.io/docs/reference/using-api/api-concepts/#efficient-detection-of-changes) и реагировать. Объекты называются _ресурсами_ и доступны по протоколу HTTP в REST. В итоге получается средство обмена данными и состоянием объектов, observe-decide-react-loop у клиентов и провайдера. Пример ресурса для наглядности:
```yaml
apiVersion: v1  # версионирование API нашего ресурса
kind: Pod  # тип ресурса
metadata:  # задаваемые пользователям мета-данные
  labels:  # набор _идентификаторов_ для фильтрации и управления
    app: provider-azure
  annotations:  # частные (конфигурационные) данные различных пользователей
    irq-load-balancing.crio.io: "false"  # disable pod-cpus from irq-balancing
  name: provider-azure  # передаваемое пользователем имя объекта
spec:  # спецификация объекта - целевое состояние
  containers:
  - image: cr.yandex/crp05dvtcqpakmaeq8hq/crossplane/provider-azure-controller:yandex-v0.1
    name: provider-azure-controller
```

Модель описывает, а, самое главное, api-server реализует многие особенности, которые при самостоятельной реализации можно упустить, либо на них может не хватить сил. Отметим:
  * [ownership, finalizers и GC](https://kubernetes.io/blog/2021/05/14/using-finalizers-to-control-deletion/) - комплиментарно к асинхронному развёртыванию механизмы корректного и контроллируемого удаления
  * [field managers и server side apply](https://kubernetes.io/docs/reference/using-api/server-side-apply/) - делегирование части полей объектов другим акторам и применение патчей средствами сервера
  * [versioning](https://kubernetes.io/docs/concepts/overview/kubernetes-api/#api-groups-and-versioning) - прописаны и реализованы политики проверки того, что v1alpha1 версия объекта совместима с v1beta3
  * [revisions and ids](https://kubernetes.io/docs/reference/using-api/api-concepts/#generated-values) - все объекты имеют версии и uuid для корректной работы в распределённой среде
  * style, naming - часто упускаемый, но важный компонент для удобного использования пользователями
  * ...and many more

# Custom Resource Definitions
>Я, как провайдер инфраструктуры, хочу уметь создавать новые типы объектов, описывать и документировать их структуру.

Т.е. провайдер предоставляет свою инфраструктуру, соответственно ему нужны _собственные объекты_. В модели k8s для этого есть механизм - [CRD](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/). Workflow провайдера выглядит так:
  * Описываю схему своего объекта:
```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  # name must match the spec fields below, and be in the form: <plural>.<group>
  name: crontabs.stable.example.com
spec:
  # group name to use for REST API: /apis/<group>/<version>
  group: stable.example.com
  # list of versions supported by this CustomResourceDefinition
  versions:
    - name: v1
      # Each version can be enabled/disabled by Served flag.
      served: true
      # One and only one version must be marked as the storage version.
      storage: true
      schema:
        openAPIV3Schema:
          description: "Cron style periodic container execution"
          type: object
          properties:
            spec:
              type: object
              properties:
                cronSpec:
                  type: string
                  description: "Crontab style string, e.g. `* * * * */5`"
                image:
                  type: string
                  description: "Image tag or ref, e.g. payments/user-logs-cron:v4"
                replicas:
                  type: integer
                  description: "Number of replicas, defaults to 1"
  # either Namespaced or Cluster
  scope: Namespaced
  names:
    # plural name to be used in the URL: /apis/<group>/<version>/<plural>
    plural: crontabs
    # singular name to be used as an alias on the CLI and for display
    singular: crontab
    # kind is normally the CamelCased singular type. Your resource manifests use this.
    kind: CronTab
    # shortNames allow shorter string to match your resource on the CLI
    shortNames:
    - ct
    categories:
    - apps
    - periodic
```
  * Создаю новый тип объекта в кластере: `kubectl apply -f crds/cron.yaml`

На этом почти всё (нам ещё нужна реализация, об этом чуть ниже). Новый тип объекта готов, он не потребовал изменения конфигурационных файлов сервера, сборки новой версии и выполнялся штатным `kubectl` через штатный API. Но уже сейчас пользователь может найти этот тип ресурса, познакомиться с ним и создать:
```shell
ya-darkstar in ~/workspace/arcadia/infra/hostctl 
❯ kubectl explain ct
KIND:     CronTab
VERSION:  stable.example.com/v1

DESCRIPTION:
     Cron style periodic container execution
...
❯ kubectl explain ct.spec.cronSpec
KIND:     CronTab
VERSION:  stable.example.com/v1

FIELD:    cronSpec <string>

DESCRIPTION:
     Crontab style string, e.g. `* * * * */5`
```
Весь heavy lifting реализации берёт на себя `kube-apiserver`, давайте посмотрим на него.

# API server
Во второй части мы говорили про необходимость наличия _сетевого endpoint_'а и API сервера для взаимодействия с клиентом. Имея модель (CRD) нам нужна реализация сервера, которая обспечит нашим _данным_:
  * сетевую доступность
  * отказоустойчивость
  * надёжное хранение
  * средства документации
  * клиентские библиотеки

"Ванильный" `kube-apiserver` предоставляет все эти компоненты (а есть разные реализации, например, [k3s-io/kine](https://github.com/k3s-io/kine) поверх PostgreSQL). Они могут не всегда оптимальны для каких-то отдельных случаев, но показали свою достаточную эффективность на практике.

# One tool and many more
Человеку (как пользователю, так и администратору провайдера) для работы нужны инструменты, с которыми он непосредственно работает. Штатным является - `kubectl`, который позволяет работать (создавать, просматривать, редактировать, удалять, получать списком, показывать документацию) с любыми объектами - см. [cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/). Недостающие, либо специфичные функции можно добавлять с помощью [плагинов](https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/).

# Controllers by the book
У нас оставалась одна нерешённая задача - реализация контроллера CronTab'а. `kube-apiserver` освободил нас от реализации API сервера, но непосредственно код нужно писать самостоятельно (пока?). В коде нам нужно выбрать лидера, следить за изменениями объектов, валидировать их, непосредственно разворачивать нужную инфраструктуру. Звучит не сложно, но дьявол в деталях. Разобраться в них, не наступить на известные ошибки помогает [book.kubebuilder.io](https://book.kubebuilder.io/) - пошаговый гайд по созданию контроллеров на базе фреймворка _kubebuilder_. Несмотря на некоторую неуклюжесть и большое количество кодогенерации - даёт понятный набор примитивов.

# Deep admin state
Если мы считаем пользовательские запросы - данными, которые доступны как ресурсы API, то можно сделать следующий логичный шаг. Использовать ту же модель и инструменты для администрирования и настроек. Для этого нам нужно:
  * сетевой endpoint для API сервера - тот же `kube-apiserver`, что и у пользователя
  * модель API - kubernetes resource model
  * реализация API сервера - `kube-apiserver` с механизмом делегирования валидации
  * инструмент для ревью изменений в административные настройки - arcanum/gerrit/github
  * инструмент применения настроек, фильтрация, получение статусов (CRUD) - `kubectl`

Давайте посмотрим на примере. В работе администратора провайдера есть такой _user story_:
>Я, как провайдер service'а, хочу ограничить использование функции `cpuset` только для объектов в namespace'е saas.

Или немного проще:

>Я, как администратор, хочу требовать наличие лейбла `app` у всех подов, чтобы единообразно управлять трафиком приложений.

Как мы можем её реализовать? Возьмём **готовое** решение, с которым администратор (в шапочке пользователя) уже умеет работать. В нашей экосистеме, построенной на workflow данных, подобные политики можно реализовать через:
  * [Admission webhook](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks) - механизм `kube-apiserver`'а делегации валидации сторонним сервисам.
  * [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/) - реализация webhook'а и контроллера политик Open Policy Agent'а в нативных объектах kubernetes.

Схема работает так:
```
                                 ┌──────────────────┐
                                 │                  │ k apply -f policy.yaml┌───────┐
┌────────┐  k apply -f pod.yaml  │  kube-apiserver  ◄───────────────────────┤ Admin │
│  User  ├───────────────────────►                  │                       └───────┘
└────────┘                       └──┬────────────┬──┘
                                    │            │
                         admission  │            │ event: update
                          review    │            │ object: policy
                                    │            │
                                    │            │
                                  ┌─▼────────────▼─┐
                                  │                │
                                  │   Gatekeeper   │
                                  │                │
                                  └────────────────┘
```
План есть, приступим к реализации.
  * Выкладываем Gatekeeper: `kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/release-3.5/deploy/gatekeeper.yaml`
  * Описываем шаблон наших ограничений на языке [Rego](https://www.openpolicyagent.org/docs/latest/policy-language/) (будем требовать обязательный label `app` у подов):
  ```
apiVersion: templates.gatekeeper.sh/v1beta1
kind: ConstraintTemplate
metadata:
  name: k8srequiredlabels
spec:
  crd:
    spec:
      names:
        kind: K8sRequiredLabels
      validation:
        # Schema for the `parameters` field
        openAPIV3Schema:
          properties:
            labels:
              type: array
              items: string
  targets:
    - target: admission.k8s.gatekeeper.sh
      rego: |
        package k8srequiredlabels

        violation[{"msg": msg, "details": {"missing_labels": missing}}] {
          provided := {label | input.review.object.metadata.labels[label]}
          required := {label | label := input.parameters.labels[_]}
          missing := required - provided
          count(missing) > 0
          msg := sprintf("you must provide labels: %v", [missing])
        }
  
  ```
  * Коммитим, ревьюим, применяем: `kubectl apply -f required-labels-template.yaml`.
  * Описываем конкретный constraint:
  ```
apiVersion: constraints.gatekeeper.sh/v1beta1
kind: K8sRequiredLabels
metadata:
  name: pod-must-have-app
spec:
  match:
    kinds:
      - apiGroups: [""]
        kinds: ["Pod"]
  parameters:
    labels: ["app"]
  ```
  * Создаём: `kubectl apply -f pod-must-have-app.yaml`.
  * Проверяем: 
  ```
❯ kubectl run ephemeral-demo --image=busybox:latest --restart=Never
Error from server ([pod-must-have-app] you must provide labels: {"app"}): admission webhook "validation.gatekeeper.sh" denied the request: [pod-must-have-tier] you must provide labels: {"app"}
```

## Known issues
Как любая реализация чего-то универсального - kubernetes не оптимален, но на практике он эффективно решает задачи. К недостаткам можно отнести (из популярного):
  * относительная ограниченная масштабируемость (если в nodes - 10k):
    * [etcd](https://etcd.io/), который хранит данные не шардирован и эффективно поддерживает не более 100Gb размера базы
    * перезапуск контроллеров - это по-сути репликация состояния, что ограничивает модель - на старте контроллеров возможен долгий sync.
  * отличная поддержка клиентов и контроллеров только для Go. Клиенты и фреймворки для других языков (даже для [Си](https://github.com/kubernetes-client/c)) есть, но сильно ниже по качеству.
  * Go IDL в качестве штатного средства для описания объектов и генерации CRD - Go и комментарии вокруг кода не самый удобный IDL
  * нет истории изменения объектов

# When it is not enough
Подведём небольшой итог:
  * Инфраструктура - это _система_ пользователя и провайдера (и администраторов).
  * _Декларативный_ подход к её описанию (с обоих сторон) удобен.
  * Terraform - это пользовательский инструмент развёртывания, он не позволяет целостно управлять инфраструктурой.
  * Kubernetes даёт модель, реализацию и экосистему инструментов для пользователей и провайдеров.

В следующей (и надеюсь завершающей части) попробуем посмотреть, когда этого подхода недостаточно, когда нужен подход _императивный_.
