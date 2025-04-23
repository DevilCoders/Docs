# Service.toml

_На текущий момент представлена версия 0.0.1 для ознакомления со структурой, возможными блоками._

## Общее описание формата

```toml
version = 1

#
# Общие блоки описывающий микросервис
#

# Описание вертикальной структуры
namespace = "media-services"
project = "dating"
name = "friends-api"

# Описание языка
language = "golang"
# Шаблон микросервиса
template = "base-rtc"
# Возможные варианты [yc, aws]
cloud = "rtc" 
# Возможные варианты [nanny, k8s]
engine = "deploy"

# Описание сервиса, документация, тикет
docs = "https://wiki.yandex-team.ru/service-name"
design_doc = "https://wiki.yandex-team.ru/service-name/design"
design_ticket = "https://st.yandex-team.ru/service-1"

# Ответственные за сервис
abc_parent = "<abc-service url>" # link if not linked
abc = "<abc-service url>" # create if not exist

idm_id = "ms-dating-friends-api" # create if not exist
idm_owners = "group, user, staff"

#
# Блоки описывающие окружение
#

# Список доступных окружений, "stable" есть всегда
envs = ["test", "pre-stable"]

# По умолчанию, все ключи в service.toml объявленные вне группы, имеют префикс env.stable, описывают продакшн окружение
# Например сетевой макрос указанный ниже, задает проект для stable окружения, полный путь будет env.stable.network
network = "_MY_PROJECT_"

#
# Блоки описывающие ресурсы
#

[replicas]
sas = 5
man = 3
vla = 1

[resources]
cpu = 100
mem = 4
disk = "10 Gib"
net = "15 MiBps"

# Переопределение для sas
[resources.dc.sas]
cpu = 98

# Переопределение для test окружения
[env.test.replicas]
sas = 1
man = 0
vla = 0

[env.test.resources]
cpu = 10
mem = 1
disk = "4 Gib"
net = "4 MiBps"

#
# Блоки описывающие содержимое
#

# to run CMD from Docker registry
[[box]]
name = "my_simple_docker_box"
docker = "registry.yandex.net/maps_core/classifier:stable@hash=...." # hash обязателен на уровне модели

# to run CMD from package.json which builds docker image
[[box]]
name = "docker_ci"
docker = "arc:maps/core/classifier/package.json"

# user binaries for experienced users
[[box]]
layers = [
    "default:bionic_20211101",
    "sbr:123456",
    "arc:project/my-binary-dir/build.json",
]
resources = [
 "/tmp/bin1=sbr:234567", 
 "/tmp/bin2=arc:project/my-binary-dir",
]

[[box.workload]]
name = "api"
run = "..."

[[box.workload]]
name = "front"
run = "..." # опционально, если это докер-файл c директивой CMD
unistat_path = "/stat"
unistat_port = "8080"
cwd = "/opt" # опционально

# Переменные окружения уровня workload
[[box.workload.env_vars]]
workload = "api"
YT_TOKEN = "yav://sec-***id/version/yt-token"
LOG_LEVEL = "literal:INFO"

# Переменные окружения уровня workload для test окружения
[[env.test.box.workload.env_vars]]
workload = "front"
LOG_LEVEL = "literal:PROTO"

# Глобальные переменные окружения для всех окружений
[env_vars]
YT_TOKEN = "yav://sec-***id/version/yt-token"
LOG_LEVEL = "literal:INFO"

# Глобальные переменные окружения для test
[env.test.env_vars]
YT_TOKEN = "yav://sec-***id/version/yt-token"
LOG_LEVEL = "literal:DEBUG"

#
# Блоки описывающие системные сайдкары
#

[sidecar.tvmtool]
tvm_destinations = [320, 456]

[sidecar.logs]
aggregate = true
topic = "lb:123"
logrotate = 

[sidecar.juggler]

#
# Блоки описывающие балансировку
#

# Upstreams
[[entrypoints]]
name = admin
protocol = "http"
port = 8080

[[entrypoints]]
name = main
protocol = "grpc"
port = 8081

# Routing
[[routes]]
route = "dating.yandex.net/maps"
preset = "rtc.nano"
expose = "ext"
entrypoint = "main"

[[routes]]
route = "dating.yandex-team.ru/admin"
preset = "rtc.nano"
expose = "internal"
entrypoint = admin

#
# Блоки описывающие базы данных
#

[[db]]
name = "dating-friends"
type = "postgres"
version = 13
master_policy = "master"
pools = "..."

[[db.replicas]]
sas = 3

[[db.resources]]
cpu = 12
mem = 30
size = 200

#
# Блоки описывающие алертинг
#

duty_calendar = "..."
jns_channel = "dating"

[alerts]
...

```

## Пример сервиса

```toml
namespace = "media-services"
project = "dating"
name = "friends-api"
language = "golang"
template = "fast-http"
docs = "https://wiki.yandex-team.ru/service-name"
design_ticket = "https://st.yandex-team.ru/service-1"
abc_parent = "<abc-service url>" 
abc = "<abc-service url>"
idm_id = "ms-dating-friends-api"
idm_owners = "group, user, staff"

envs = ["test", "pre-stable"]
cloud = "rtc"
engine = "deploy"

########################
######## Stable ########
########################

network = "_MY_PROJECT_"

[replicas]
sas = 5
man = 3
vla = 1

[resources]
cpu = 100
mem = 4
disk = "10 Gib"
net = "15 MiBps"

[[box]]
name = "docker_ci"
docker = "arc:maps/core/classifier/package.json"

[[box.workload]]
name = "api"

[[box.workload.env_vars]]
workload = "api"
YT_TOKEN = "yav://sec-***id/version/yt-token"
LOG_LEVEL = "literal:INFO"

[env_vars]
YT_TOKEN = "yav://sec-***id/version/yt-token"
LOG_LEVEL = "literal:INFO"

[sidecar.tvmtool]
tvm_destinations = [320, 456]

[sidecar.logs]
aggregate = true
topic = "lb:123"

[[entrypoints]]
name = main
protocol = "grpc"
port = 8081

# Routing
[[routes]]
route = "dating.yandex.net/friends/api"
preset = "rtc.nano"
expose = "ext"
entrypoint = "main"

[[db]]
name = "dating-friends"
type = "postgres"
version = 13
master_policy = "master"
pools = "..."

[[db.replicas]]
sas = 3

[[db.resources]]
cpu = 12
mem = 30
size = 200

#########################
######## Testing ########
#########################

env.test.network = "_MY_PROJECT_TEST_"

[env.test.replicas]
sas = 1
man = 0
vla = 0

[env.test.resources]
cpu = 10
mem = 1
disk = "4 Gib"
net = "4 MiBps"

[env.test.env_vars]
YT_TOKEN = "yav://sec-***id/version/yt-token"
LOG_LEVEL = "literal:DEBUG"

[[env.test.db]]
name = "dating-friends"
type = "postgres"
version = 13
master_policy = "master"
pools = "..."

[[env.test.db.replicas]]
sas = 1

[[env.test.db.resources]]
cpu = 2
mem = 4
size = 10

...
```

## Почему `toml` формат?

Основное преимущество `toml` над форматом `yaml`, **удобная работа с ним человеком**. Из-за отсутствия отступов и наличия логического выделения блоков, формат легко читается и воспринимается, его легко редактировать как в редакторе, так и в консоли или UI интерфейсе. При редактирование практически невозможно совершить ошибки. Удобно копировать и вставлять части спецификации, делиться блоками, формат отлично смотрится на любом носителе или экране.

С точки зрения функциональности формат не уступает другим, при этом превосходит в удобстве определения массивов, таблиц, inline таблиц и массивов таблиц, содержит богатый набор нативных типов и прост для изучения.

С другой стороны, у пользователей остается возможность использовать `yaml` формат, тк внутреннее представление в infractl будет храниться в нем, для удобства генерации так же будет предоставлены `.proto` структуры.