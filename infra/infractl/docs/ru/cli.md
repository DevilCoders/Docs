# Установка и настройка

Утилита `infractl` доступна из `ya`:

```bash
ya tool infractl
```

# Команды

## Рабочее окружение

* Утилита infractl использует файл конфига k8s (kubeconfig) как источник настроек для подключения к серверу
* Для настройки этого файла используйте команды `infractl kubeconfig setup` и `infractl kubeconfig use-context`

## kubeconfig

Настройка конфига k8s для подключения к серверу infractl.

### setup

Создаёт или обновляет имеющийся kubeconfig, добавляя настройки для кластеров infractl:

```bash
ya tool infractl kubeconfig setup
```

Создаёт контекст с именем `k.yandex-team.ru:infractl-context`.

### use-context

Переключает контекст конфига kubeconfig на указанный:

```bash
ya tool infractl kubeconfig use-context k.yandex-team.ru
```

## bootstrap

Команда `infractl bootstrap` предназначена для создания скелета сервиса под `infractl`. Команда работает в интерактивном режиме, получая от пользователя необходимую информацию для создания неймспейса, проекта и рантаймов. Перед запуском нужно подготовить [токен робота](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=3e5a6e634dd243088d230775c401147d), от имени которого будет работать `infractl`, а так же сетевой макрос, в котором будет развёрнут сервис.

Кроме записи объектов в Kubernetes команда генерирует всю необходимую структуру файлов и каталогов c i.yaml-манифестами и спеками объектов. В качестве объектов генерируются сервисы-пустышки с простейшим веб-сервером. Предполагается, что пользователь сам поправит необходимые спеки объектов под свои нужды.

`infractl bootstrap` генерирует сервис целиком: неймспейс, проект, test- и prod-рантаймы. Для более гранулярного использования есть следующие команды:

### bootstrap namespace
Генерирует только неймспейс и проект.

### bootstrap runtime
Генерирует только объекты test- и prod-рантаймов.

Пример сгенерированной структуры каталогов для неймспейса `my-team` и рантайма `my-service`:
```
manifests/
├── base.my-team.runtime.my-service.yaml
├── env.properties
├── i.yaml
├── prod
    ├── cfg.yaml
    ├── env.properties
    ├── infra.my-team.runtime.prod.my-service.yaml
    ├── i.yaml
    └── patch.my-team.runtime.my-service.yaml
└── test
    ├── cfg.yaml
    ├── env.properties
    ├── infra.my-team.runtime.test.my-service.yaml
    ├── i.yaml
    └── patch.my-team.runtime.my-service.yaml
```
Предполагается, что пользователь будет редактировать базовую yaml-спеку и yaml-спеки патчей. Конечные спеки `infra.my-team.runtime.prod.my-service.yaml` и
`infra.my-team.runtime.test.my-service.yaml` генерируются запуском команды `infractl make` и напрямую пользователем редактироваться не должны.

## create

Генерация файлов спецификаций на основе пользовательского ввода.

На текущий момент поддерживается только создание спецификаций неймспейсов:
```bash
ya tool infractl create --abc abc_slug -o infra.namespace.yaml --push namespace_name
```

Опции:
```bash
-a, --abc ABC_SLUG      Имя abc-сервиса, к которому будет привязан нейсмпейс
-o, --output FILENAME   Имя файла, в который будет записана созданная спека неймспейса
--push                  Если этот флаг включен, созданная спека будет сразу залита в k8s
namespace_name          Имя создаваемого неймспейса
```

## import

Импорт объектов из других систем для последующего управления ими с помощью infractl.

На текущий момент поддерживаются стейджи из Yandex.Deploy и апстримы awacs:

### stage
```bash
ya tool infractl import stage -o infra.stage.yaml stage_name
```

Опции:
```bash
-o, --output FILENAME        Имя файла, в который будет записана созданная спека
stage_name                   Имя стейджа, который необходимо импортировать
```

### awacs upstream

```bash
ya tool infractl import awacsupstream -o infra.upstream.yaml -n namespace awacs_namespace upstream_name
```

Опции:
```bash
-o, --output FILENAME        Имя файла, в который будет записана созданная спека
-n, --namespace NAMESPACE    Имя неймспейса k8s, в котором будет находиться импортированный апстрим
awacs_namespace              Имя неймспейса awacs, в котором находится апстрим
upstream_name                Имя апстрима awacs, который необходимо импортировать
```

### project
```bash
ya tool infractl import project -o infra.project.yaml project_name
```

Опции:
```bash
-o, --output FILENAME        Имя файла, в который будет записан импортируемый проект
project_name                 Имя проекта, который необходимо импортировать
```

## modify

Модифицирующие операции над объектами.

### delegate

Делегирование необходимых для работы токенов.
Поддерживаются токены YP и awacs.

#### YP

```bash
ya tool infractl modify delegate yp -f infra.namespace.yaml
```

Опции:
```bash
-f, --file FILENAME          Имя файла неймспейса, для которого делегируется токен
--yp-token TOKEN             Токен робота для работы с YP. Вместо этой опции рекомендуется использовать
                             переменную YP_TOKEN.
```

#### awacs

```bash
ya tool infractl modify delegate awacs -f infra.namespace.yaml
```

Опции:
```bash
-f, --file FILENAME          Имя файла неймспейса, для которого делегируется токен
--awacs-token TOKEN          Токен робота для работы с awacs. Вместо этой опции рекомендуется
                             использовать переменную YP_TOKEN.
```

### set-template

Команда для удобной генерализации спек стейджей с заменой указаний конкретных ресурсов на вычисляемый
в момент загрузки результат сборки артефакта ya package. На текущий момент поддерживаются docker и
порто-слои.

#### Docker:

```bash
ya tool infractl modify set docker -f infra.stage.yaml --du deploy_unit --box box_name path/to/package.json
```

Опции:
```bash
-f, --file FILENAME          Имя файла с редактируемой спекой стейджа
--du DEPLOY_UNIT             Имя модифицируемого deploy unit. Если он в стейдже только один, указывать необязательно
--box BOX_NAME               Имя генерализуемого box. Если он в deploy unit только один, указывать необязательно
path/to/package.json         Путь к файлу спецификации ya package от корня аркадии
```

#### Слои:

```bash
ya tool infractl modify set layer -f infra.stage.yaml --du deploy_unit --layer layer_name path/to/package.json
```

Опции:
```bash
-f, --file FILENAME          Имя файла с редактируемой спекой стейджа
--du DEPLOY_UNIT             Имя модифицируемого deploy unit. Если он в стейдже только один, указывать необязательно
--layer LAYER_NAME           Имя генерализуемого слоя. Если он в deploy unit только один, указывать необязательно
path/to/package.json         Путь к файлу спецификации ya package от корня аркадии
```

## build

Команда для сборки необходимых для выкладки артефактов и подготовки билд-файла с подстановками.
Поддерживаются сендбокс-ресурсы и докер-образы.

Также позволяет вручную задать предсобранные пользователем артефакты.

```bash
ya tool infractl build --incremental \
      -d path/docker1/package.json=docker1/image:tag@sha \
      -d path/docker2/package.json=docker2/image:tag@sha \
      -s path/layer1/package.json=12345678 \
      -s path/layer2/package.json=87654321 \
      infra.stage.yaml...
```

Опции:
```bash
-d, --docker PACKAGE=IMAGE          Использовать в качестве докер-артефакта PACKAGE уже собранный образ IMAGE
-s, --sandbox PACKAGE=RESOURCE_ID   Использовать в качестве сендбокс-артефакта PACKAGE уже собранный ресурс RESOURCE_ID
-i, --incremental                   Собирать только те артефакты, которых ещё нет в билд-файле
filename.yaml...                    Перечисление файлов, в которых надо искать указания на артефакты
```

## put

Применить спецификации к k8s, подставив необходимые артефакты из билд-файла.

Поддерживают файлы namespace, deploy stage, runtime и awacsupstream.

```bash
ya tool infractl put -m "some description" infra.*.yaml…
```

Опции:
```bash
-m, --message MESSAGE        Описание правки, которое попадёт в историю стейджа
-w, --wait                   Дожидаться вкладки стейджа в Y.Deploy. Работает только для объектов deploy stage
-t, --timeout SECONDS        Таймаут, в течение которого дожидаться выкладки стейджа
```

## pull

Вытянуть из k8s спецификации и сгенерировать билд-файл на их основе.

```bash
ya tool infractl pull NAMESPACE Kind/ObjectName…
```

Опции:
```bash
-o, --output FILENAME      Имя файла, в который записать все полученные объекты. Если не указан, то каждый объект
                           будет записан в отдельный файл с именем вида infra.<NAMESPACE>.<Kind>.<ObjectName>.yaml
-s, --strict               Строгий режим формирования buld-файла. Если несколько извлекаемых объектов используют
                           разные артефакты для подстановки одного и того же пакета, в строгом режиме выдастся
                           ошибка, в противном случае будет использован последний извлечённый
NAMESPACE                  Имя неймспейса, из которого извлекаются объекты
Kind                       Тип объекта, например, awacsupstream, awacsbackend, deploystage, deployproject
ObjectName                 Имя объекта
```

## make

Сборка ресурсов для указанного [манифеста i.yaml](manifest.md).

```bash
ya tool infractl make TARGET_DIR
```

`TARGET_DIR` - относительный путь до директории, содержащей `i.yaml`. Может быть опущен, если запуск команды происходит уже в нужной директории.

