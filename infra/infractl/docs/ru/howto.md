# HowTo — импорт сервиса из Deploy

## TL;DR {#tldr}

В этом документе мы положим в Аркадию поднятый в [Deploy](https://docs.yandex-team.ru/deploy) сервис и передадим управление им в infractl. Для этого:
* Делегируем в infractl права на управление стейджами от имени робота
* Положим в репозиторий описание тестового стейджа из Deploy
* Укажем в нём ссылку на [манифест сборки докер-образа](https://docs.yandex-team.ru/ya-make/usage/ya_package/docker)
* Импортируем из Deploy престейбл и продовый стейджи и объединим их в неймспейс
* Избавимся от дублирования общих настроек наших контуров, вынеся их в отдельный файл
* Выложим стейджи напрямую и через [CI](https://docs.yandex-team.ru/ci/)

Все операции будем проводить над сервисом [dproxy](https://deploy.yandex-team.ru/projects/dproxy).

В результате мы получим хранимую в Аркадии структуру файлов, которую можно посмотреть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/infra/dproxy/infractl). Она включает:
* директории с общими настройками сервиса и специфичными для отдельных контуров: `base`, `dev`, `pre`, `prod`
* конечные описания каждого контура: `infra.{dev,pre,prod}.yaml`
* флоу выкладки сервиса через CI: `a.yaml`

Начнём с получения доступа к infractl.

## Доступ к infractl {#access}

Доступ к infractl есть у всех пользователей, имеющих в **любом** ABC-сервисе роль со скоупом `development`, `administration`, `testing` или `devops`. В их число входят роли вида `Администратор MDB`, `Разработчик интерфейсов` и подобные. У ролей без этих скоупов, например, `Менеджер продукта`, доступа не будет, потребуется получить роль с названным скоупом. Если вам не хватает указанных доступов, просим [сообщить нам](https://t.me/+VdEooUIOJbo4ZDVi) об этом.

## Подготовка infractl {#install}

infractl доступен всем пользователям Аркадии с помощью утилиты `ya`: `ya tool infractl`. Если утилита `ya` не может найти его, попробуйте обновить локальную копию Аркадии, выполнив `arc pull`. [Быстрый старт для работы с Аркадией](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

Поскольку infractl использует для работы стандартный файл конфига Kubernetes, необходимо добавить в него настройки нашего кластера и переключить контекст на добавленный конфиг:

```bash
ya tool infractl kubeconfig setup
ya tool infractl kubeconfig use k.yandex-team.ru
```

## Права на управление стейджами {#permissions}

Чтобы infractl мог управлять нашими стейджами, нужно выдать доступ на их редактирование какому-нибудь роботу и делегировать в infractl его токен. Создать робота можно через [форму](https://staff.yandex-team.ru/preprofile/create/robot/). Для примера возьмём робота `robot-dproxy` и выдадим роль `MAINTAINER` на наш проект в Deploy.

{% cut "Скриншоты" %}

Открываем проект в Deploy:

![](https://jing.yandex-team.ru/files/alonger/edit-project.png)

Переходим на страницу выдачи роли `MAINTAINER`:

![](https://jing.yandex-team.ru/files/alonger/manage-roles.png)

Запрашиваем роль нашему роботу:

![](https://jing.yandex-team.ru/files/alonger/request-role.png)

Заполняем форму:

![](https://jing.yandex-team.ru/files/alonger/robot-dproxy.png)

{% endcut %}

После этого залогинимся под роботом в приватном режиме браузера и откроем из-под него [ссылку для получения YP-токена](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=3e5a6e634dd243088d230775c401147d).

## Импорт сервиса из Deploy {#import}

Импортируем стейдж `dev-dproxy`. Для этого сначала необходимо создать в k8s неймспейс — это аналог проекта — в котором будут храниться наши стейджи. Имя неймспейса **обязательно** должно совпадать с именем проекта в Deploy:

```bash
ya tool infractl create namespace dproxy --abc dproxy -o infra.namespace.yaml --push
ya tool infractl modify delegate yp --yp-token <ROBOT-TOKEN> -f infra.namespace.yaml
```

Мы создали неймспейс `dproxy`, привязанный к abc-сервису dproxy, положили его в файл со спекой, и сразу же запушили его в k8s. Затем мы положили токен нашего робота в Секретницу и делегировали доступ до него в infractl.

Все члены указанного нами ABC-сервиса автоматически получают права на редактирование всех объектов неймспейса. Пока что другого штатного способа управления правами в infractl нет, [больше деталей](https://docs.yandex-team.ru/infractl/limitations#roles).

После этого импортируем стейдж из Deploy:

```bash
mkdir dev
ya tool infractl import stage dev-dproxy -o dev/infra.dev.yaml
```

Мы записали описание стейджа в файл `dev/infra.dev.yaml`. Его уже можно выкатить, что мы и сделаем, чтобы убедиться, что всё настроено правильно:

```bash
ya tool infractl put dev/infra.dev.yaml -m 'deploy from infractl'
```

Если теперь открыть в UI историю нашего стейджа, в ней должна быть видна свежесозданная от имени робота ревизия, отличающаяся от предыдущей только номером.

## Просмотр статуса стейджа {#status}

Чтобы убедиться, что всё прошло успешно, или найти причину, если выкладка в Deploy не произошла, посмотрим статус стейджа по версии infractl. Просмотр объектов на данный момент реализуется через утилиту `kubectl`, которая доступна в `ya`. Выводимый статус отформатируем через `ya tool jq`:

```bash
ya tool kubectl get -f dev/infra.dev.yaml -o jsonpath='{.status.sync_status}' | ya tool jq
```

В зависимости от результата, в выхлопе этой команды будет информация или об успешной заливке стейджа в Deploy, или сообщение об ошибке.

Посмотреть полный статус объекта можно командой:

```bash
ya tool kubectl get -f dev/infra.dev.yaml -o jsonpath='{.status}' | ya tool jq
```

## Подстановка таргета сборки {#generalize}

Хотя мы уже и импортировали наш стейдж в виде текстового файла и даже можем выкладывать его в Deploy, коммитить его в Аркадию ещё рано. В нем сейчас зашиты конкретные версии артефактов сервиса: исполняемых файлов, докер-образа или слоёв файловой системы. При сборке новой версии приложения нам бы пришлось каждый раз редактировать его описание, храняющееся в репозитории, заменяя версию докер-образа или бинарника на более свежую. В случае автовыкладок это бы требовало добавить промежуточный шаг в виде коммита в Аркадию. Вместо этого infractl позволяет указывать в спеке сервиса вместо конкретных версий артефактов ссылки на лежащие в Аркадии таргеты их сборки.

В нашем случае пакет dproxy собирается в виде porto-слоя с id=`dproxy`.

{% cut "Для сервисов на porto-слоях и докер-образах это можно проверить, увидев в файле строки вида:" %}

Для porto-слоёв:
```yaml
...
layers:
- checksum: 'EMPTY:'
  id: dproxy
  ...
  url: sbr:2906960529
...
```

Для докер-образов:

```yaml
...
images_for_boxes:
  my-box:
    name: path/to/docker/image
    tag: "12.06"
...
```

{% endcut %}

Заменим указание конкретного слоя в созданном файле на ссылку на пакет, создающий этот артефакт:

```bash
ya tool infractl modify set layer -f dev/infra.dev.yaml --layer dproxy infra/dproxy/pkg.json
```

Для докер-образов команда будет выглядеть так:
```bash
ya tool infractl modify set docker -f dev/infra.dev.yaml junk/alonger/docker-package/package.json
```

Подобная возможность пока что не поддержана для статических ресурсов, однако появится [в скором времени](https://st.yandex-team.ru/INFRACTL-92).

Эти команды полагаются на то, что в стейдже есть лишь один деплой-юнит с одним боксом. В противном случае нужно указать ID деплой-юнита, а для докер-образа ещё и бокса через аргументы `--du` и `--box`.

Убедиться, что всё прошло успешно, можно найдя в файле строки вида:

```yaml
metadata:
  annotations:
    deploystage.infractl.k.yandex-team.ru/buildManifest: |

        # Для докер-образов:
        docker_packages:
        - path: junk/alonger/docker-package/package.json

        # Для porto-слоёв:
        layers:
        - layer_id: dproxy
          path: infra/dproxy/pkg.json
```

В таком виде наш файл уже можно закоммитить в Аркадию:
```bash
arc add infra.namespace.yaml dev/infra.dev.yaml
arc commit -m 'Add infractl specs'
arc pr c --push
```

Команда `ya tool infractl modify` удаляет из сервиса конкретную версию докер-образа или porto-слоя, перекладывая их значения в файл `.build.yaml`. Поэтому несмотря на то, что наш сервис уже больше не содержит конкретных версий артефактов, мы всё ещё можем записать его в infractl с помощью команды:

```bash
ya tool infractl put dev/infra.dev.yaml -m 'generalize spec'
```

Эта команда объединит настройки сервиса из файла `infra.dev.yaml` и конкретные версии его артефактов из файла `.build.yaml` и запустит выкладку получившегося результата.


## Локальная сборка {#build}

При разработке бывает удобным выкладывать собранные локально версии своего приложения в разработческие контура. infractl позволяет сделать это сразу же из консоли. Больше не нужно сначала пушить собранный локально докер-образ в docker-registry или исполняемый файл в sandbox, после чего отдельно обновлять его в Yandex.Deploy. Теперь для этого достаточно выполнить две команды:

```bash
ya tool infractl build dev/infra.dev.yaml
ya tool infractl put dev/infra.dev.yaml -m 'bump stage'
```

Первая из указанных команд соберёт все указанные в сервисе артфеакты из локальной версии кода Аркадии, а вторая запустит выкладку сервиса. infractl будет собирать все артефакты под linux, используя кросскомпиляцию при запуске команды `build` на другой платформе, [цитата из кода](https://a.yandex-team.ru/arc_vcs/infra/infractl/cli/commands/build/build.go?rev=r9264859#L209).

{% note tip %}

Если в сервисе используется докер-образ, для его сборки на локальном компьютере должен стоять docker. А перед запуском `ya tool infractl build` нужно не забыть залогиниться в docker-registry, [выполнив команду docker login](https://wiki.yandex-team.ru/qloud/docker-registry/#authorization).

{% endnote %}


## Импорт всех стейджей сервиса {#multiple-stages}

До сих пор мы работали только с тестовым стейджом сервиса, пришло время импортировать престейбл и продакшн. Для этого выполним знакомые команды:

```bash
mkdir pre
ya tool infractl import stage pre-dproxy -o pre/infra.pre.yaml
ya tool infractl modify set layer -f pre/infra.pre.yaml --layer dproxy infra/dproxy/pkg.json

mkdir prod
ya tool infractl import stage prod-dproxy -o prod/infra.prod.yaml
ya tool infractl modify set layer -f prod/infra.prod.yaml --layer dproxy infra/dproxy/pkg.json
```

И закоммитим результат в Аркадию:

```bash
arc add pre/infra.pre.yaml prod/infra.prod.yaml
arc commit -m 'Add more infractl specs'
arc pr c --push
```

Теперь наш сервис представлен в репозитории тремя файлами:
```
dev/infra.dev.yaml
pre/infra.pre.yaml
prod/infra.prod.yaml
```

В текущем виде сервис уже можно хранить в Аркадии и выкладывать через CI. В следующем разделе мы попытаемся выделить общие настройки стейджей в отдельный файл, чтобы избавиться от дублирования. Это нетривиальная задача, требующая аккуратной ручной работы, которую можно облегчить с помощью дополнительных инструментов, но вряд ли удастся полностью автоматизировать в общем случае. Если на данном этапе вы не готовы заниматься выделением общих настроек, рекомендуем пропустить этот шаг и перейти сразу к [разделу о выкладке через CI](#ci).

## Выделение общих настроек {#make}

### Подготовка {#make-prepare}

Можно заметить, что большая часть настроек в получившихся файлах идентичны. Чтобы избежать дублирования, мы разделим их на общую и специфичные для каждого контура части. Общую часть мы вынесем в директорию `base`, а специфичные — в директории `dev`, `pre` и `prod`. Внутри каждой из директорий создадим файл `stage.yaml`, где будут храниться сами настройки:

```bash
mkdir -p base
touch base/stage.yaml dev/stage.yaml pre/stage.yaml prod/stage.yaml
```

Теперь структура файлов выглядит так:
```
├── base
│   └── stage.yaml
├── dev
│   ├── stage.yaml
│   └── infra.dev.yaml
├── pre
│   ├── stage.yaml
│   └── infra.pre.yaml
└── prod
    ├── stage.yaml
    └── infra.prod.yaml
```

### infractl make (#make-intro)

Для спецификации способов объединения ресурсов будем использовать утилиту `infractl make`. Для ее работы необходимо объявить один или несколько манифестов `i.yaml`.

Начнем с простого примера, в котором определим список ресурсов, с которыми будет работать `infractl make`:
```bash
cat <<EOF >base/i.yaml
output: idle.yaml
resources:
- file: stage.yaml
EOF
```
Мы указали, что хотим в качестве ресурса использовать `stage.yaml`, а результат положить в `idle.yaml`  
```bash
ya tool infractl make base/
```
Можно проверить, что в `idle.yaml` лежит копия `stage.yaml`


### kustomize {#kustomize-intro}

Для выделения общих настроек предлагается использовать формат, поддерживаемый утилитой [kustomize](https://kustomize.io). Её возможности весьма ограничены и покрывают лишь несложные сценарии доопределения базовых настроек кастомными. Генерацию описаний сервисов императивным кодом пока что можно построить только снаружи infractl, однако в будущем мы поддержим её в команде `infractl make`.

`kustomize` принимает на вход файлы с общей и специфичной частями настроек, в каждом из которых они должны быть представлены в виде документа с одной и той же схемой данных, в нашем случае это объект `DeployStage`.

{% cut "Общий принцип слияния настроек" %}

При слиянии этих файлов ассоциативные массивы объединяют свои элементы рекурсивно по ключам, при слиянии скаляров приоритет отдаётся специфичным настройкам. Списки, представленные в схеме данных стейджа, проаннотированны надлежащим образом, позволяющим сливать их так же, как словари, используя в качестве ключа поле, идентифицирующее элемент списка. Проще всего разобраться на примере.

{% endcut %}

### Пример слияния настроек {#merge-example}

Если задать в общих настройках стейджа одни свойства ворклоада:

```yaml
workloads:
- id: dproxy
  transmit_logs: true
```

А в специфичных другие:

```yaml
workloads:
- id: dproxy
  start:
    command_line: ./dproxy -c /cfg_testing.yml
```

То `kustomize` сможет объединить их, опираясь на идентифицирующий ворклоад ключ `id`:

```yaml
workloads:
- id: dproxy
  transmit_logs: true
  start:
    command_line: ./dproxy -c /cfg_testing.yml
```

{% cut "Подобным образом умеют сливаться все необходимые поля стейджа." %}

- [TVolume](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L34)
- [TWorkload](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L37)
- [TBox](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L40)
- [TFile](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L361)
- [TEnvVar](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L775)
- [TLayer](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L1087)
- [TResource](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r9040707#L1089)
и другие

{% endcut %}

### Ручное разделение настроек {#kustomize-action}

К сожалению, выделение общих настроек из нескольких стейджей это нетривиальная задача, и мы не умеем её автоматизировать и пока что не умеем облегчать. Её приходится проделать вручную, опираясь на [пример](https://a.yandex-team.ru/arc/trunk/arcadia/infra/dproxy/infractl/).

В нём в [общую часть](https://a.yandex-team.ru/arc/trunk/arcadia/infra/dproxy/infractl/base/stage.yaml) вынесены почти все настройки, включая заказ ресурсов (за исключением CPU и памяти), параметры запуска приложения, а также общие переменные окружения и файлы.

А в [специфичные для контуров](https://a.yandex-team.ru/arc/trunk/arcadia/infra/dproxy/infractl/dev/stage.yaml) части вынесены кастомные переменные окружения (тестовые для теста, продовые для прода), заказ CPU и памяти, а также команда запуска.

### Манифест сборки {#i-yaml}

Помимо самих настроек, необходимо указать ещё манифест `i.yaml`, описывающий способ их слияния. Из директорий со специфичными настройками он [должен](https://a.yandex-team.ru/arc/trunk/arcadia/infra/dproxy/infractl/pre/i.yaml) ссылаться на файл с общими настройками. А в директории с общими настройками он должен содержать имя файла с ними.

```bash
cat <<EOF >base/i.yaml
resources:
- file: stage.yaml
EOF

cat <<EOF >dev/i.yaml
output: infra.dev.yaml
resources:
- base: infra/dproxy/infractl/base
patches:
- kustomize:
    namePrefix: dev-
    patchesStrategicMerge:
    - stage.yaml
EOF

cat <<EOF >pre/i.yaml
output: infra.pre.yaml
resources:
- base: infra/dproxy/infractl/base
patches:
- kustomize:
    namePrefix: pre-
    patchesStrategicMerge:
    - stage.yaml
EOF

cat <<EOF >prod/i.yaml
output: infra.prod.yaml
resources:
- base: infra/dproxy/infractl/base
patches:
- kustomize:
    namePrefix: prod-
    patchesStrategicMerge:
    - stage.yaml
EOF
```

Пройдем по всем полям:

- `output`: путь к файлу, в котором будет храниться результат выполнения данного манифеста
- `resources`: может быть двух видов
  - `base`: путь в аркадии до другого манифеста, из результата сборки которого возьмутся ресурсы для текущего манифеста. В нашем примере мы ссылаемся на `base/i.yaml`, который (как мы убедились [выше](#make-intro)) просто вернет базовую спеку
  - `file`: относительный путь к `yaml` файлу, необходим для добавления ресурса. Это может пригодиться не в базовом слое, если нам нужно добавить специфичный для данного окружения объект (например еще один стейдж или балансер).
- `patches`: список патчей, которые применятся ко всем собранным ресурсам, сейчас поддерживается только `kustomize`.
  - `kustomize`: описание того, как будут изменяться ресурсы в данном окружении. Для тех, у кого есть опыт работы с `kustomize` - это содержимое файла `kustomization.yaml`.  

## Применение настроек {#make-build}

После того, как мы справились с разделением настроек, проверим, что всё сделали правильно и сформируем содержимое наших стейджей из исходных файлов:

```bash
ya tool infractl make dev/
ya tool infractl make pre/
ya tool infractl make prod/
```

Чтобы проверить себя на наличие ошибок в результирующих файлах, позовём команду `arc diff dev/infra.dev.yaml` и убедимся, что дифф отсутствует или корректен.

{% note tip %}

Мы рекомендуем хранить в репозитории как исходные файлы, так и конечное содержимое стейджей, поскольку последнее намного проще валидировать чем исходники. В том числе это даёт возможность делать ревью изменений конечных спек сервисов коллегами из команды при их коммите в Аркадию.

{% endnote %}

После того, как мы привели исходники в подходящее состояние и убедились, что в конечных спеках отсутствует неожидаемый дифф, коммитим все добавленные нами файлы в Аркадию:

```bash
arc add base dev pre prod
arc commit -m 'Add kustomize layers'
arc pr c --push
```


## Настройка CI {#ci}

{% note tip %}

Примеры можно [найти в Аркадии](https://a.yandex-team.ru/arc_vcs/infra/infractl/ci_tasklets/examples).

{% endnote %}

Для сборки сервиса и заливки спек в Kubernetes через CI можно использовать кубик [apply_specs](https://a.yandex-team.ru/arc_vcs/infra/infractl/ci_tasklets/apply_specs/impl/__init__.py).

На данный кубик поддерживает сборку сервиса только с использованием задачи `YA_PACKAGE_2`: можно собирать либо докер-образ, либо слой.

Рассмотрим пример flow с использованием `apply_specs`:

```yaml
 flows:
    autodeploy:
      title: Autodeploy InfraCtl simple layer pipeline commit
      jobs:
        build:
          task: common/arcadia/ya_package_2
          title: Build layer
          stage: build
          input:
            packages: infra/deploy_ci/examples/layer_pipeline_without_approves/build.json
            package_type: tarball
            resource_type: YA_PACKAGE
        apply-infractl:
          task: common/infractl/apply_specs
          title: Apply InfraCtl specs
          version: testing
          needs:
           - pull-specs
           - build
          stage: apply
          input:
            config:
              source:
                arc:
                  path: infra/infractl/ci_tasklets/examples/layer_pipeline/infra.stage.yaml

```

### Пререквизиты для использования кубика apply_specs {#ci-prerequisites}

1. Для робота, от которого будет выполняться CI-flow, необходимо запросить доступы в [IDM](https://nda.ya.ru/t/rH6i-rMx4skp8n), как это описано в разделе [Доступы](#access).
2. В YAV-секрет, указанный в `a.yaml`, необходимо положить токен до нашего кластера Kubernetes. Ключ до токена в YAV должен быть таким: `infractl_ci.kubetoken`. Токен можно получить, пройдя по [ссылке](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=141d6d975f6049789ba7c78bf82ada5d).
3. При использовании докера в кубик необходимо передать пользователя и токен, с которыми нужно ходить в Docker registry. Пользователь передаётся в параметре `config.build.docker`. Токен нужно положить в YAV-секрет, указанный в `a.yaml`. Ключ в YAV должен быть таким: `infractl.docker_token`.

Путь до спеки стейджа передаётся в кубик через входной параметр `config.source.arc.path`. Это должен быть путь относительно корня аркадии. Пока в кубике поддерживается только получение спек из аркадии.

Сборка бинарника сервиса осуществляется с помощью таски `YA_PACKAGE_2` (пока кубик работает только с ней). Собранный артефакт будет передан на вход команде `infractl build`, которая подставит полученный `id` sandbox-ресурса в спеку стейджа.

После этого кубик `apply_spec` запушит спеку командой `infractl put`.

Пример flow для сборки докера можно посмотреть в [примере](https://a.yandex-team.ru/arc_vcs/infra/infractl/ci_tasklets/examples/docker_pipeline/a.yaml).
