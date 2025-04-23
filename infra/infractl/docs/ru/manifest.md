# Манифест сборки (i.yaml)

```
service level               i.yaml
	                .../  |  \...
	                      |
	                      |
	                      |
project level               i.yaml
                           /  |   \
                          /   |    \
                         /    |     \
stage level         i.yaml i.yaml i.yaml


```

Манифест представляет из себя описание сборки спецификации списка объектов. Обычно он используется для дедупликации или разделения на смысловые части. Сборка происходит с помощью команды [infractl make](cli.md#make).

Сборка представляет из себя прохождение пути в графе зависимостей, в каждом из узлов которого выполняются два действия: сборка ресурсов и применение патчей. Разберем каждый из них подробнее:

## Сборка ресурсов

Сборка всегда запускается из листового узла, а выполняется с корня. Список ресурсов указывается в поле `resources` манифеста. Ресурсы бывают двух видов:

Для указания зависимости от какого-либо базового манифеста, используется ресурс типа `base`, в котором должен быть указан абсолютный путь от корня в аркадии. Например:

```yaml
resources:
- base: infra/dproxy/infractl/base
```

Для указания относительного пути до файла, содержащего спеки kubernetes-объектов, используется ресурс `file`:

```yaml
resources:
- file: deploystage.yaml
- file: backend.yaml
```

Таким образом при прохождении пути от корня графа сборки, мы получаем список неповторяющихся ресурсов.

Рассмотрим пример:
```
arcadia
└── infra
    ├── balancer.yaml
    ├── i.yaml
    └── dproxy
        ├── i.yaml
        ├── runtime.yaml
        └── dev
            ├── deploystage.yaml
            └── i.yaml
```
infra/i.yaml:
```yaml
resources:
- file: balancer.yaml
```
infra/dproxy/i.yaml:
```yaml
resources:
- base: infra
- file: runtime.yaml
```
infra/dproxy/dev/i.yaml:
```yaml
resources:
- base: infra/dproxy
- file: deploystage.yaml
```

Результатом сборки будут объекты из файлов в следующем порядке:
- infra/balancer.yaml
- infra/dproxy/runtime.yaml
- infra/dproxy/dev/deploystage.yaml

## Применение патчей

В каждом из узлов можно применить произвольное количество патчей, изменяющих собранные на данный момент ресурсы. При дальнейшем прохождении пути в графе будут использоваться уже измененные объекты.

На текущий момент список патчей такой:

### kustomize

Применяет указанную спеку [kustomize](https://kustomize.io) для существующих ресурсов. Если бы использовалась утилита `kustomize`, то это было бы содержимым файла `kustomization.yaml`

Пример, добавляющий префикс `test-` к именам всех объектов:

```yaml
patches:
- kustomize:
    namePrefix: test-
```

### files

Добавляет файлы из относительного пути или секрета, может использоваться вместе с селектором. Селектор необходим для указания пути до места в DeployStage или Runtime, в котором нужно применить изменения, и имеет следующие поля:

```yaml
selector:
  name: "" # Имя или DeployStage или Runtime
  deploy_unit_id: "" # не используется для Runtime
  box_id: "" # не используется для Runtime
  workload_id: ""
```
Некоторые поля (или весь селектор) могут быть опущены, если однозначно определяются нижестоящие сущности.

Пример:

```yaml
patches:
- files:
    # ключ: путь внутри пода
    # значение: относительный путь до локального файла
    /configs/config.yaml: config.yaml
    /configs/secret.yaml: ${secretID:secretVersion:secretKey}
  selector:
    name: some-runtime-name
```

### dirs

Позволяет указывать директории вместо отдельных файлов:

```yaml
patches:
- dirs:
    # ключ: директория внутри пода
    # значение: относительный путь до локальной директории
    /configs/: configs/
```

### env

Указание переменных окружения для box (в DeployStage) или workload (в DeployStage или Runtime)

```yaml
patches:
- env:
    SOME_KEY: value 
    SOME_TOKEN: ${secretID:secretVersion:secretKey}
  selector:
    name: some-name
    workload_id: app
```

### env\_source

Аналогично env, но читает переменные из локального `.properties` файла

i.yaml:
```yaml
patches:
- env_source: env.properties
```
env.properties:
```
SOME_KEY=value 
SOME_TOKEN=${secretID:secretVersion:secretKey}
```

Внутри одного элемента списка могут находиться несколько патчей (кроме `kustomize`, который всегда должен быть отдельно), для которых будет применен общий селектор, например:

```yaml
patches:
- env_source: env.properties
  dirs:
    /configs/: configs/
  selector:
    name: SomeStage
```

## Пример

Для сохранения результата сборки в файл используется поле `output`, которое необходимо указать в листовом узле графа сборки.

Пример манифеста:
```yaml
output: infra.dev.yaml
resources:
- base: infra/dproxy/infractl/base
patches:
- kustomize:
    namePrefix: dev-
    patchesStrategicMerge:
    - stage.yaml

- files:
    /configs/cfg.yml: cfg.yml
  env_source: env.properties
```

