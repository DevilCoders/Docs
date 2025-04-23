# Сборка и доставка
Для доставки обновлений необходимо собрать docker образ и залить его в 
[registry](https://registry.yandex.net/maps_adv/billing_proxy). 
Дальше необходимо обновить кофигурацию в qloud.

## Docker
Для сборки образа необходимо из корня аркадии выполнить следующую 
команду:
`ya package --docker --docker-repository maps_adv maps_adv/billing_proxy/app/package.json`

### Флаги
* `--docker-push` - Залить собранный образ в registry
* `--docker` - Собрать docker образ
* `--docker-repository` - Какой репозиторий использовать
* `--docker-registry` - Какой registry использовать, по умолчанию 
`registry.yandex.net`

Подробнее описано [здесь](https://wiki.yandex-team.ru/yatool/package/#vnimanie)

## Qloud
Для этого процесса используется [qtools](https://github.yandex-team.ru/maps/qtools). 
Он позволяет обновлять конфигурации в qloud основываясь на специальном 
конфигурационном файле `.qtools.json`.

### Установка qtools
Установки необходимо выполнить команду: 
`npm install --registry=https://npm.yandex-team.ru @yandex-int/qtools`.
Она скачает зависимости qtools и подтянит необходимые зависимости. 
Обратите в каком каталоге выполняете эту команду, так как в нем будет 
создана директория `node_modules`, которая использыется в команде 
деплоя конфигурации на qloud 

### Обновление конфигурации в qloud
Для обновления конфигурации необходимо вызвать команду: 
`node node_modules/.bin/qtools deploy testing --force --wait -v2`

> Команду необходимо выполнять из каталога в котором непосредственно 
находиться файл конфигурации `.qtools.json`

### Флаги
* `--force` - Принудительное обновление конфигурации
* `--wait` - Дождаться пока конфигурация не перейдет в необходимое 
состояние
* `--target-state` - Целевое состояние для конфигурации. Флаг не 
обязательный по умолчанию имеет значение `DEPLOED`, а так же может 
принимать значения `COMMITTED` и `PREPARED`


## CI/CD
Сборка проекта происходит автоматически при коммите в `trunk`. На это 
событие подвешена реакция в `testenv`, который в свою очередь запускает 
цепочку задач в `sandbox`.

### Сборка docker образа
Первой задачей дергается [задача](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps_adv/BuildStatController.yaml)
запускающая процесс сборки `Docker` образа в процессе, которого еще и 
происходит сборка бинарного файла.

> Бинарный файл собирается как релизный билд

### Автоматическое создание коммитов в qloud
Для работы автоматического создания коммитов в Qloud необходимо:
1. [Получить](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4dd38b9acbb44ad8a7ece163ddf1c53a)
OAuth ключ для qtools
1. Добавить ключ `qtools-oauth` в [sandbox vault](https://sandbox.yandex-team.ru/admin/vault)
    - **Name:** `qtools-oauth`
    - **Owner:** _указать себя_
    - **Shared:** `robot-testenv`
    - **Data:** _полученный ранее oauth ключ_

### Обновление конфигурации в qloud
При успешно выполнении задачи сборки запускается другая [задача](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/maps_adv/DeployQloudStatController.yaml)
выкатки обновленной конфигурации в qloud.

> Конфигурации выкладываются в COMMITTED состоянии и требует ручного 
перевода в DEPLOYED состояния 

Для запуска инструмента qtools была разработа отдельная независимая 
[задача](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps_adv/QtoolsDeployApplication/__init__.py)
в sandbox. 

### Ссылки
* Админка для [testenv](https://beta-testenv.yandex-team.ru/project/maps_adv-builder/),
при этом в ней не все поддерживается и есть [старый](https://testenv.yandex-team.ru/?screen=manage&database=maps_adv-builder)
варинант оной
* Управление окражениями для приложения в [qloud](https://qloud-ext.yandex-team.ru/projects/maps/front-maps-adv-statistics) 
