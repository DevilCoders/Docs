# Настройка CI/CD

В этом руководстве мы настроим базовый flow сборки и деплоя сервиса, используя [Arcadia CI](https://docs.yandex-team.ru/ci/) и [кубики Deploy](https://a.yandex-team.ru/arc_vcs/ci/registry/common/deploy), которые позволяют патчить/обновлять ресурсы в вашем Stage и управлять полокационным релизом.

## Предварительные шаги. 

### Настройка Arcadia CI {#quickstart-ci}

Перед началом необходимо убедиться, что вы подключили свой проект к Arcadia CI, выполнив все шаги из [этой инструкции](https://docs.yandex-team.ru/ci/quick-start-guide)

В результате у вас есть:
* Пользователь-робот
* Секрет в Секретнице и токен с именем `ci.token`
* Файл `a.yaml` с примером Hello world
* Группа в Sandbox

### Настройка Deploy

* Получите токен [Deploy token for CI](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=c185b75fce81443c86750dd411b8943a)
* Положите полученный токен с ключом `deploy_ci.token` в [секрет CI](https://docs.yandex-team.ru/ci/secret), созданный в [шаге выше](#quickstart-ci), в [Секретницу](https://yav.yandex-team.ru/)
* Проверьте, что у вашего робота есть права `Maintainer` в Ya.Deploy на ваш проект. Если прав нет, их необходимо выдать в [IDM](https://idm.yandex-team.ru/#rf-role=vJXej8CO#deploy-prod(fields:()),rf-expanded=vJXej8CO,rf=1)

## Настройка релизного flow

После предварительных шагов и перед непосредственно написанием flow желательно ознакомиться с [основами описания a.yaml](https://docs.yandex-team.ru/ci/basics) и остальными подразделами в данной документации.

Все примеры flow ниже будут содержать два/три шага: 
1. Сборка ресурса
2. Релиз в Deploy
3. Одобрение локационной выкладки

После настройки этих шагов вы сможете настраивать и более сложные flow, например: 
1. Сборка ресурса
2. Релиз в тестовое окружение
3. Запуск тестов
4. Релиз в стабильное окружение
5. Проверка мониторингов
6. ...

## Настройка кубика common/deploy/create_release

Данный кубик опирается на релизную интеграцию (*пользователю ее настраивать не нужно*) и модифицирует **только указанные пользователем ресурсы** в рамках одного Stage применяя патчи, не затрагивая другие параметры спецификации.

Auto Rollback и другие flow отката с использованием данного кубика выполняют откат накатом, то есть применяют патчи и модифицируют указанные ресурсы не затрагивая изменения, которые были сделаны пользователем вне релизного flow.

Стоит отметить, что кубик не будет дожидаться релиза, если у вас настроен локационный апрув, для этого используйте кубики `common/deploy/approve_location`.

Каждый приведённый патч указывается в качестве элемента массива `patches` во входных параметрах кубика `common/deploy/create_release`. Массив обязан содержать хотя бы один патч.  
Для всех возможных полей патчей рекомендуется смотреть структуру proto-сообщения [TDeployPatchSpec](https://a.yandex-team.ru/arc_vcs/yp/yp_proto/yp/client/api/proto/deploy_patch.proto?rev=ed71cce3ce6220e39689ebefee8c9a7e6a731b41#L120).

### Обновление статического ресурса

```yaml
release-to-deploy:
  task: common/deploy/create_release
  input:
    config:
      stage_id: stage_id
      patches:
        - sandbox:
            # Тип sandbox-ресурса, который необходимо найти в собранных ранее во flow артефактах.
            sandbox_resource_type: TEST_RESOURCE
            # Опциональный словарь требуемых атрибутов ресурса, который также используется для поисков правильного ресурса
            # в собранных артефактах. Как правило имеет смысл, если вы собираете в рамках flow несколько артефактов
            # с одинаковым типом.
            attributes:
              key1: value1
              key2: value2
            static:
              # Имя deploy unit, в котором производятся изменения.
              deploy_unit_id: du1
              # Имя статического ресурса в этом deploy unit.
              static_resource_ref: resource1
```

### Обновление слоя

```yaml
release-to-deploy:
  task: common/deploy/create_release
  input:
    config:
      stage_id: stage_id
      patches:
        - sandbox:
            # Тип sandbox-ресурса, который необходимо найти в собранных ранее во flow артефактах.
            sandbox_resource_type: TEST_RESOURCE
            # Опциональный словарь требуемых атрибутов ресурса, который также используется для поисков правильного ресурса
            # в собранных артефактах. Как правило имеет смысл, если вы собираете в рамках flow несколько артефактов
            # с одинаковым типом.
            attributes:
              key1: value1
              key2: value2
            static:
              # ID deploy unit, в котором производятся изменения.
              deploy_unit_id: du1
              # ID слоя в этом deploy unit.
              layer_ref: layer1
```

### Обновление динамического ресурса

```yaml
release-to-deploy:
  task: common/deploy/create_release
  input:
    config:
      stage_id: stage_id
      patches:
        - sandbox:
            # Тип sandbox-ресурса, который необходимо найти в собранных ранее во flow артефактах.
            sandbox_resource_type: TEST_RESOURCE
            # Опциональный словарь требуемых атрибутов ресурса, который также используется для поисков правильного ресурса
            # в собранных артефактах. Как правило имеет смысл, если вы собираете в рамках flow несколько артефактов
            # с одинаковым типом.
            attributes:
              key1: value1
              key2: value2
            dynamic:
              # ID обновляемого динамического ресурса в стейдже
              dynamic_resource_id: dr1
              # Идентификатор группы подов в динамическом ресурсе. В подавляющем большинстве случаев
              # динамические ресурсы содержат всего одну группу с идентификатором "all"
              deploy_group_mark: all
```

### Обновление докер-образа

```yaml
release-to-deploy:
  task: common/deploy/create_release
  input:
    config:
      stage_id: stage_id
      patches:
        - docker:
            docker_image_ref:
              # Имя deploy unit, в котором производятся изменения.
              deploy_unit_id: du1
              # Имя бокса в этом deploy unit.
              box_id: box1
            # Имя образа, который необходимо выложить. Обратите внимание, что в отличие от sandbox-ресурсов,
            # для docker-образов пока не существует установленного способа описать докер образ в качестве выходного
            # артефакта какого-то из кубиков на стадии сборки, поэтому в отличие от релизной интеграции Ya.Deploy
            # здесь указывается имя образа вместе с конкретным тегом.
            # В данном примере мы предполагаем, что данный патч используется в релизном flow, где в качестве имени
            # тега будет использоваться подстановочная переменная ${context.version_info.full}. Сам образ должен
            # быть собран на стадии сборки и запушен в registry.yandex.net под этим же тегом.
            image_name: "myproject/myimage:${context.version_info.full}"
```

## Настройка кубика common/deploy/approve_location

### Сборка и выкладка статического ресурса с простыми полокационными аппрувами

Для работы локационных аппрувов необходимо настроить свой стейдж в соответствии с [инструкцией](https://deploy.yandex-team.ru/docs/concepts/perlocation).

```yaml
release-to-deploy:
  task: common/deploy/create_release
  ...
# Кубик одобрения локационной выкладки. В этом примере мы используем простую автогенерацию,
# когда нет необходимости вручную прописывать во flow все локации — количество экземпляров кубика
# создаётся автоматически на основании информации о стейдже. Недостатком этого подхода является то,
# что кубики аппрува равнозначны и пользователь может одобрять выкатку локаций в произвольном порядке.
approve-location:
  task: common/deploy/approve_location
  needs: release-to-deploy
  stage: deploy
  multiply:
    # Здесь мы указываем ID предыдущего кубика release-to-deploy, который в output-артефактах
    # создаёт список approval_locations, содержащий информацию о том, какие локации требуют аппрува.
    by: ${tasks.release-to-deploy.approval_locations}
    title: "Approving location ${by.cluster} for deploy unit ${by.deploy_unit}"
    as-field: infra.deploy_ci.approve_location.Input.LocationMatcher
  # Требуем, чтобы пользователь явно одобрил выкатку в интерфейсе CI.
  manual:
    enabled: true
    prompt: "Approve location ${by.cluster} for deploy unit ${by.deploy_unit}?"
```

### Сборка и выкладка статического ресурса со строгим порядком аппрува локаций

Для работы локационных аппрувов необходимо настроить свой стейдж в соответствии с [инструкцией](https://deploy.yandex-team.ru/docs/concepts/perlocation).

```yaml
release-to-deploy:
  task: common/deploy/create_release
  ...
# Кубик одобрения выкатки в ДЦ man
approve-location-man:
  task: common/deploy/approve_location
  needs: release-to-deploy
  stage: deploy
  input:
    # явно указываем во входных параметрах кластер
    location_match:
      cluster: man
  title: Approve location man
  manual:
    enabled: true
    prompt: "Approve location man?"
# Ваш опциональный кубик, в котором можно запустить какие-то тесты для проверки, что релиз успешно выехал в man
run-tests-man:
  task: dummy
  title: Run tests in man location
  needs: approve-location-man
# Кубик одобрения выкатки в ДЦ sas
approve-location-sas:
  task: common/deploy/approve_location
  needs: run-tests-man
  stage: deploy
  input:
    # явно указываем во входных параметрах кластер
    location_match:
      cluster: sas
  title: Approve location sas
  manual:
    enabled: true
    prompt: "Approve location sas?"
# Ваш опциональный кубик, в котором можно запустить какие-то тесты для проверки, что релиз успешно выехал в sas
run-tests-sas:
  task: dummy
  title: Run tests in sas location
  needs: approve-location-sas
```

## Примеры flow

Все примеры доступны в [репозитории](https://a.yandex-team.ru/arc_vcs/infra/deploy_ci/examples/). Список будет пополняться со временем.

### Сборка и выкладка docker-образа с помощью ya package

Для сборки docker-образа при помощи задачи YA_PACKAGE необходимо предварительно подготовить Dockerfile и json-спецификацию сборки [по инструкции](https://docs.yandex-team.ru/ya-make/usage/ya_package/docker).
Пример Dockerfile и файла build.json можно посмотреть [в примерах](https://a.yandex-team.ru/arc_vcs/infra/deploy_ci/examples/docker_pipeline/).

Кроме того, в соответствии с [требованиями Ya.Deploy](../concepts/stage/ispolzovanie-docker-obraza) необходимо выдать роботу **robot-qloud-client@** роль **viewer** на ваш docker-репозиторий в registry.

Для docker необходимо указывать при сборке и выкладке имя тега (как правило, для него используется версия), поэтому здесь приводится пример со сборкой Docker-образа в релизном flow, где доступно поле `${context.version_info}`:

```yaml
flows:
  autobuild:
    title: Autodeploy deploy_ci docker pipeline commit
    jobs:
      build:
        task: common/arcadia/ya_package_2
        title: Build docker
        stage: build
        input:
          # Путь относительно корня аркадии к спеке собираемого с помощью ya package пакета
          packages: infra/deploy_ci/examples/docker_pipeline/build.json
          package_type: docker
          # Имя docker-репозитория. Это не имя docker-образа: если вы заливаете свой
          # пакет в докер, например, как deploy-ci/http_server_example:1.0
          # то "deploy-ci" — это репозиторий, "http_server_example" — имя образа,
          # а "1.0" — имя тега.
          docker_image_repository: deploy-ci
          # Имя робота, который авторизуется в Registry
          docker_user: robot-drug-deploy
          # Имя хранилища Sandbox Vault, содержащего OAuth-токен для доступа docker_user к registry.
          # В качестве токена в Vault можно сохранить тот же токен, который вы сохранили
          # под именем deploy_ci.token в yav. 
          docker_token_vault_name: docker.registry.token
          docker_push_image: true
          # Явно задаём имя тега, который мы собираем. Оно потребуется ниже.
          custom_version: "${context.version_info.full}"
      release-to-deploy:
        task: common/deploy/create_release
        title: Create release
        needs: build
        stage: deploy
        input:
          config:
            stage_id: deploy-ci-test
            patches:
              - docker:
                  docker_image_ref:
                      # Имя deploy unit, в котором производятся изменения.
                      deploy_unit_id: du3
                      # Имя обновляемого box в этом deploy unit.
                      box_id: box
                  # Полное имя применяемого docker-образа, включая
                  # имя тега (совпадает с тем тегом, который мы собрали выше).
                  image_name: "deploy-ci/example_http_server:${context.version_info.full}"
```

### Сборка и выкладка слоя с помощью ya package

```yaml
flows:
  autobuild:
    title: Autodeploy deploy_ci layer pipeline commit
    jobs:
      build:
        task: common/arcadia/ya_package_2
        title: Build layer
        stage: build
        input:
          packages: infra/deploy_ci/examples/layer_pipeline_without_approves/build.json
          package_type: tarball
          resource_type: TEST_RESOURCE
      release-to-deploy:
        task: common/deploy/create_release
        version: testing
        title: Create release
        needs: build
        stage: deploy
        input:
          config:
            stage_id: deploy-ci-test
            yp_cluster: man-pre
            patches:
              - sandbox:
                  sandbox_resource_type: TEST_RESOURCE
                  static:
                    layer_ref: layer1
                    deploy_unit_id: du2
```

### Сборка и выкладка нового статического ресурса

```yaml
flows:
  autobuild:
    jobs:
      # Кубик (или кубики), описывающий сборку.
      # На выходе получается произвольное множество объектов SandboxResource,
      # которые могут использоваться на стадии выкладки.
      build:
        task: common/arcadia/ya_make
        title: Build
        stage: build
        input:
          targets: infra/deploy_ci/examples/pipeline_without_approves
          arts: infra/deploy_ci/examples/pipeline_without_approves/http_server
          result_rt: TEST_RESOURCE
          result_single_file: true
          build_type: release
      # Кубик для выкладки собранных артефактов в деплой. 
      release-to-deploy:
        task: common/deploy/create_release
        title: Deploy
        needs: build
        stage: deploy
        input:
          config:
            # Имя стейджа, который мы обновляем
            stage_id: deploy-ci-test
            # Список применяемых патчей. В данном случае мы собираем и обновляем только один ресурс.
            patches:
              - sandbox:
                  # Ищем собранный артефакт типа TEST_RESOURCE
                  sandbox_resource_type: TEST_RESOURCE
                  # и обновляем им статический ресурс resource1 в деплой юните du2
                  static:
                    deploy_unit_id: du2
                    static_resource_ref: resource1
```
