# Cборка мобильных приложений в Sandbox


[Чат поддержки](https://t.me/joinchat/BGoHwlAt-eqLDRpAHhB8lQ)


## Что такое сборка в sandbox и какие у неё плюсы и минусы { #what_is_it_teamcity_sandbox_runner }
Sandbox - универсальная система запуска задач, подробнее [тут](https://docs.yandex-team.ru/sandbox/). Основные отличия teamcity sandbox runner (TSR) от запуска напрямую на агентах:
* В sandbox значительно больше ресурсов и их проще динамически аллоцировать.
* В TSR больше возможностей для контроля выполнения задач, например можно запускать build step-ы параллельно и ускорять сборку в разы.
* Задачи в sandbox (sb) запускаются асинхронно и почти не занимают лицензии. Минусы – не так удобно смотреть логи и realtime-логи.
* При использовании TSR конфиг сборки хранится в репе в коде, а не в UI teamcity - проще редактировать через PR-ы и запускать старые билды.
* Сборка в sb работает в чистом окружении, а само окружение можно легко подготовить самостоятельно, если нужны какие-то особые пакеты/бинарники/итд.

## Как начать пользоваться сборкой в Sandbox { #how_start }

### Шаг 1: создать BUILD_NUMBER { #step_1_create_build_number }
Данный счетчик можно будет использовать при сборке приложения. Он будет доступен в gradle через `System.env.BUILD_NUMBER`

Нужно придумать название своему счетчику и создать его с помощью [teamcity конфигурации](https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Infra_Sandbox_CounterCreate). Просто запустите ее, и teamcity попросит указать название счетчика и его начальное значение (больше нуля). Как правило это текущий макс. номер билда в тимсити. Название счетчика необходимо будет указать в конфиг файле чуть позже.
Существующие имена счетчиков и их значения можно посмотреть в [YT](https://yt.yandex-team.ru/locke/navigation?path=//home/mobdevtools/build_counters).


{% note warning %}

 Ограничения:
 Запускаемая ваша сборка в teamcity должна запускаться под пользователем robot-sbmonorepo, принадлежащему MOBDEVTOOLS. Задача выполняемая под вашим проектным роботом не сможет получить доступ к счетчику принадлежащему MOBDEVTOOLS. На практике это означает что robot-sbmonorepo должен получить доступы к используемым в сборке секретам.

{% endnote %}

{% cut "Для того чтобы обойти это ограничение, нужно создать и использовать счетчик в своей проектной квоте." %}

1. Запросить квоту в locke.

   1. Перейти в свой сервис ABC, затем в Квоты, затем "Передать квоту".
   2. В строке "Откуда взять" в первое поле указываем "YT", во второе "reserve".
   3. В строке "Куда перевести" в первое поле указываем свой сервис, во второе "default".
   4. Провайдер выбираем "YT".
   5. Ресурс выбираем "Locke количество нод" и указываем количество нод. Две ноды нужны для директорий + по ноде для каждого счетчика.
   6. Нажать создать заявку.

2. Создать аккаунт в locke по [инструкции](https://yt.yandex-team.ru/docs/description/common/quota_request#zapros-na-sozdanie-vychislitelьnogo-pula) где "Ключ аккаунта" и будет `<quota_name>`.
3. Запросить "Read and Write Access" доступ к locke через IDM.

   1. Перейти в [IDM](https://idm.yandex-team.ru).
   2. Нажать "запросить роль".
   3. Указать "YT кластер locke" затем "Read and Write Access".
   4. Указать путь `//home/quota_name` где quota_name имя квоты.

4. Cоздать папку build_counters в своей квоте locke, и положить в нее нужное значение в виде uint64_node с произвольным названием `<build_counter_name>`, тогда названием build_counter-а будет `<quota_name>:<build_counter_name>`.

    Альтернативный вариант выполнения пункта 4 (предварительно установив [yt](https://yt.yandex-team.ru/docs/api/cli/install)):
    ```shell
    export YT_PROXY=locke
    export YT_TOKEN=<token https://oauth.yt.yandex.net/>
    export QUOTA_NAME=<quota_name>
    export BUILD_COUNTER_NAME=<build_counter_name>
    yt create map_node //home/$QUOTA_NAME/build_counters
    yt create uint64_node //home/$QUOTA_NAME/build_counters/$BUILD_COUNTER_NAME
    yt set //home/$QUOTA_NAME/build_counters/$BUILD_COUNTER_NAME <build counter number>
    ```



5. Положить yt-token в sandbox vault, с названием `yt_token` и выдать права owner-у запускаемой задачи.

{% endcut %}

{% cut "Пример использования проектной квоты в приложении IoT." %}

Чеклист с конфигами, которые нужно заполнить, ключами, которые нужно создать, и прочими деталями, необходимыми для корректной работы сборок. Если у вас возникли проблемы, пройдитесь по списку и проверьте, что в вашем проекте всё настроено правильно.
- [Группа](https://abc.yandex-team.ru/services/alice_iot_mobile_application/folders/) в ABC со [своей квотой в locke](https://yt.yandex-team.ru/locke/navigation?path=//home/iot_mobile/build_counters).
- Соответствующая [группа](https://sandbox.yandex-team.ru/admin/groups/ALICE_IOT_MOBILE/general) в Sandbox.
- build_counter'ы в [своей квоте в locke](https://yt.yandex-team.ru/locke/navigation?path=//home/iot_mobile/build_counters), по одному на каждый вид сборки.
- [Робот](https://staff.yandex-team.ru/robot-nafanya), от лица которого будут запускаться сборки. У вас должен быть доступ к его аккаунту.
- SSH ключ для робота. Публичный ключ должен быть указан у робота на [Staff](https://staff.yandex-team.ru/robot-nafanya), а приватный - добавлен в [Vault](https://sandbox.yandex-team.ru/admin/vault) (Create -> Vault -> Name: id_<логин робота> -> Shared with: <[группа в Sandbox](https://sandbox.yandex-team.ru/admin/groups/ALICE_IOT_MOBILE/general)> и <логин робота>)
- ARC_TOKEN. (Create -> Vault -> Name: ARC_TOKEN -> Owner: <[группа в Sandbox](https://sandbox.yandex-team.ru/admin/groups/ALICE_IOT_MOBILE/general)> -> Data: <токен [отсюда](https://oauth.yt.yandex.net/)>)
- yt_token. (Create -> Vault -> Name: yt_token -> Owner: <[группа в Sandbox](https://sandbox.yandex-team.ru/admin/groups/ALICE_IOT_MOBILE/general)> -> Data: <токен [отсюда](https://nda.ya.ru/t/qPiF_BwS3WKLuC)>)

Все три vault'а из примера можно посмотреть [здесь](https://sandbox.yandex-team.ru/admin/vault?limit=20&offset=0&shared=robot-nafanya). Если при выполнении таска возникает ошибка `TaskError: Enter passphrase: load failed`, SSH для робота нужно генерировать на Ubuntu Precise (12.04), пишите за этим [сюда](https://staff.yandex-team.ru/quasistellar).
- [Проект](https://teamcity.yandex-team.ru/project/MobileNew_Monorepo_IoT?mode=builds) на TeamCity.
- [Билд](https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_IoT_Android_IotRelease?mode=builds) внутри проекта.
- Параметры билда (Edit configuration... -> Parameters):
- - `branch_spec`: ```
+:arcadia/(trunk)
+:arcadia/(users/robot-stark/iot/android/*/merge_pin)```
Нужно чтобы TeamCity мог получать изменения из наших PR.
- - `sandbox.config_path`: `mobile/iot/android/iot-app/sandbox/release`
Указание на директорию в нашем проекте, в которой будет лежать конфиг сборки.
- - `sandbox.ssh_key`: `quasistellar:id_robot-nafanya` Указание на приватный SSH ключ робота, который мы положили в Vault. Имеет форму `<owner ключа>:<название ключа>`.
- Конфиг сборки, путь к которому был указан в `sandbox.config_path`:
```
config:
  name:
    release
  build_counter:
    iot_mobile:IoT_Android_Release_Build_Counter // Название build_counter'а из нашей группы в locke
  runner_version:
    2021.02.08-7832518
stages:
  assemble:
    android-sdk:
      platforms(31,32)+tools(32.0.0) // compileSdk вашего проекта должна быть среди указанных platforms, а tools должны соответствовать buildToolsVersion; различные варианты android-sdk можно посмотреть здесь: https://sandbox.yandex-team.ru/resources?type=ANDROID_SDK и выбрать подходящий
    work_dir:
      mobile/iot/android/iot-app/ // директория вашего проекта
    cmd:
      - ./gradlew app:assembleRelease app:testReleaseUnitTest // команды, выполняемые в рамках сборки; в данном случае собирается приложение и прогоняются тесты
    lxc:
      2161339669
    artifacts: // содержимое этих папок станет доступно во вкладке Artifacts на TeamCity, когда билд завершится
      +app/build/outputs/apk/release/*.apk: apk
      +app/build/outputs/bundle/release/*.aab: bundle
      +app/build/reports/: reports
      +app/build/outputs/mapping/release/*: proguard
    kill_timeout:
      3600
    multislot:
      MEDIUM
    env:
      IS_SANDBOX_BUILD: true
```
- Конфиг `a.yaml` (должен лежать в корне проекта), нужен для запуска сборок после PR:
```
service: iot_mobile_app
title: iot_mobile_app
arcanum:
  auto_merge:
    requirements:
      - system: arcanum
        type: comment_issues_closed
      - system: teamcity-common
        type: MobileNew_Monorepo_IoT_Android_IotRelease // Build configuration ID нашей сборки, можно посмотреть на странице сборки (Edit configuration... -> General Settings)
        alias: IoT::Android::PR
        restartable: true
        data:
          branch_prefix: iot/android
          strategy: merge-pin
          included_paths:
            - /mobile/iot/android/iot-app/ // директория вашего проекта

```

{% endcut %}


### Шаг 2: написать <config_name\>.config.yaml и положить его в репозиторий { #step_2_create_config }

Проверка запускается по правилам, описанным в конфиг-файле формата yaml, который лежит в вашей директории проекта monorepo(можно класть в любое место, путь до него будет указываться в Build Features, см. ниже).

{% cut "Конфиг файл на примере hypercube" %}

```yaml
config:
    name:
        Hypercube_runner_config
    build_counter:
        Mdm_Android_Build_Counter
    runner_version:
        2021.02.08-7832518
stages:
    assemble:
        work_dir:
            hypercube/android/mdm-app/
        cmd:
            - ./gradlew assemble
        caches:
            - gradle-modules-2
            - ~/.konan
        lxc:
            2161339669
        kill_timeout:
            3600
        artifacts:
             +app/build/*: assemble
        multislot:
            MEDIUM
    test:
        work_dir:
            hypercube/android/mdm-app/
        cmd:
            - ./gradlew test
        lxc:
            2161339669
        junit:
            - app/build/test-results
        multislot:
            LARGE
```

{% endcut %}

[Подробнее о заполнении конфига](#all_about_config)

### Шаг 3: создать конфигурацию teamcity с запуском в sandbox { #step_3_setup_teamcity_build }
Создайте (если еще нет) свой проект в teamcity  внутри [мобильной монорепы](https://teamcity.yandex-team.ru/project/MobileNew_Monorepo?projectTab=overview&mode=builds).
Далее создайте новую билд конфигурацию внутри проекта. Выберите тип конфигурации Manually. Заполните название конфигурации, а в качестве шаблона для конфига выберите

{% cut "Arcadia Sandbox Tier 1 template" %}

![Image](https://jing.yandex-team.ru/files/makstheimba/2021-02-15T09:40:01Z.195044f.png)

{% endcut %}

В качестве параметра `sandbox.config_path` укажите путь до вашего конфиг файла в аркадии. (можно использовать `path/to/config_dir`, в таком случае конфигурация должна располагаться по пути `path/to/config_dir/config.yaml`, либо `path/to/config_dir/config_name.` и конфигурация располагается по пути `path/to/config_dir/config_name.config.yaml`)

{% cut "Или измените текущую(не рекомендуется)." %}

![Image](https://jing.yandex-team.ru/files/aslevushkin/Снимок%20экрана%202019-09-12%20в%2017.50.59.png)

Откройте свою teamcity configuration, которая уже запускает ваши проверки, перейдите в Edit Configuration Settings и затем в Build Features. Feature, которая нас интересует — Sandbox Task Launcher.
В ней есть несколько полей:
* **sandbox_task_type** — название Sandbox задачи, нам нужна [TEAMCITY_SANDBOX_RUNNER_LAUNCHER](https://sandbox.yandex-team.ru/tasks?type=TEAMCITY_SANDBOX_RUNNER_LAUNCHER&limit=20&created=3_days);
* **authorisation_token** — [Sandbox token](https://sandbox.yandex-team.ru/oauth/token) пользователя, под которым будут запускаться задачи;
* **provide_sandbox_context** — `True`, позволяет пробрасывать параметры в Sandbox задачу;
* **parameters_prefix** — sandbox префикс, по которому параметр пробрасывается в Sandbox, например, sandbox.some_parameter пробрасывает `some_parameter` из teamcity в [Sandbox](https://sandbox.yandex-team.ru/tasks);
* **description** — описание задачи;
* **owner** — группа, которая будет являться владельцем запусков (необходимо предварительно [создать](https://sandbox.yandex-team.ru/admin/groups) ее в [Sandbox](https://sandbox.yandex-team.ru/tasks)).
Примечание: группу необходимо создавать в Sandbox, не ABC!

Рядом с Build Features есть вкладка с Build steps. Необходимо добавить Sandbox resources loader для того, чтобы указанные в конфиге артефакты отображались в teamcity.

{% endcut %}

### Шаг 4: (опциональный) Поменять параметры сборки { #step_4_change_build_parameters }
На странице **Parameters** перенастройте параметры, если не устраивают дефолтные значения либо добавьте новые:
* **<sandbox_parameters_prefix\>.ssh_key** - название ssh-ключа с доступом к репозиторию. Отдельный важный момент, что ключ нужно создавать под Linux размером 2048 (например временно создать VM из tmp квоты в QYP).
* **<sandbox_parameters_prefix\>.repo_url** - url репозитория (необходимо изменить если используется репозиторий отличный от monorepo)

env и секреты лучше указать в конфиге, но можно и задать их в тимсити:
* **<sandbox_parameters_prefix\>.env** - переменные окружения в формате json словаря.
  Как добавить переменные в Teamcity:
  - В Build Features -> Sandbox Task Launcher возьмите значение parameters_prefix.

    {% cut "пример с parameters_prefix = 'sandbox'" %}

    ![Image](https://jing.yandex-team.ru/files/r2d2/Screenshot%202021-09-23%20at%2017.44.08.png)
    ![Image](https://jing.yandex-team.ru/files/r2d2/Screenshot%202021-09-23%20at%2017.43.53.png)

    {% endcut %}

  - В Parameters -> Configuration Parameter добавьте переменную ``<sandbox_parameters_prefix\>.env``, в ``sandbox_parameters_prefix`` подставляем
  значение полученное на предыдущем шаге. В переменной перечислите в формате json переменные.

    {% cut "пример" %}

    ![Image](https://jing.yandex-team.ru/files/r2d2/Screenshot%202021-09-23%20at%2017.44.24.png)

    {% endcut %}

    {% note warning %}

    В названии переменных запрещено использовать точки

    {% endnote %}

    Пример валидных переменных
    ```yaml
    'TEAMCITY_VERSION': '1',
    'PROJECT_PATH': '.',
    'BRANCH': '%teamcity.build.branch%',
    'IS_TABLET': 'false'
    ```

* **<sandbox_parameters_prefix\>.secrets** - секреты в формате json словаря (доступны начиная с версии `20_04_30-6755638`).

Удалите параметры MANAGED_ANDROID_HOME, иначе у вас будет пустой список compatible agent-ов

{% cut "В примере под катом нужно удалить переменные ANDROID_HOME и ANDROID_SDK_HOME" %}

![Image](https://wiki.yandex-team.ru/mobvteam/sandbox-runner/.files/screenshot2020-09-16at17.19.31-1.png)

{% endcut %}

### Шаг 5: (опциональный) добавить Build Report Tab с логами { #step_5_add_report_tab_with_logs }
Зайдите в режим редактирования настроек своего проекта, и добавьте новый Build Report Tab в разделе Report Tabs, с параметрами `Tab Title: Sandbox execution log` и `Start page: index.html`

## Подробнее про конфигурацию { #all_about_config }

Пример абстрактной конфигурации
```yaml
config:
  name:
    features
  runner_version:
    2021.02.08-7832518
  build_counter:
    Passport_Android_Build_Counter               # номер билда будет доступен в окружении как BUILD_NUMBER (аналогично teamcity); про заведение новых счётчиков см. шаг 1
                                                 # так же будет доступен branch как BUILD_BRANCH
stages:                                          # все stage-и выполняются параллельно, если не заданы явные или неявные зависимости(если сортировать по длине выполнения,
                                                 # от большего к меньшему, то общее время выполнения сократится)
  app3:
    work_dir:                                    # рабочая директория, все команды stage-а запускаются относительно неё. default - текущая директория
      passport/android/passport-sdk/
    cmd:                                         # команды для запуска, выполняются последовательно, через %env.v_name% матчатся переменные окружения
      - ./gradlew clean :passport:testDebugUnitTestCoverage javadoc publishPassportReleasePublicationToMavenLocal
      # Обратите внимание на пример с разбитием длинной cmd на строки:
      - ./gradlew :app-test:assembleApp3ProdRelease
        -Pmaven_local_dependencies=true
        -Penv_value_1=%env.VALUE1%
        -Puser_login=%env.user_login%
      # Вариант с разбиением длинной команды используя block scalar & strip chomping indicator (см. https://yaml.org/spec/1.2.2/#block-scalar-styles)
      - >-
          ./gradlew :app-test:assembleApp3ProdRelease
          -Pmaven_local_dependencies=true
          -Penv_value_1=%env.VALUE1%
          -Puser_login=%env.user_login%
    fail_fast:                                   # останавливает с ошибкой все шаги сразу после падения текущего шага, default = false
      true
    lxc:
      2161339669                                 # lxc-образ для запуска команд, подробнее см. ниже
    env:
      VALUE1: some_value                         # будет доступен в env как VALUE1; в gradle можно передавать через -P, либо забирать через System.getenv("VALUE1")
      <variable>: <value>
      COMPOSITE_VALUE1: composite_%env.VALUE1%   # сложные переменные окружения доступны начиная с версии 20_05_26-6874170.
      # Сложная переменная означает, что значение %env.VALUE% будет подставлено в значение COMPOSITE_VALUE1.
      # Однако, прямой маппинг COMPOSITE_VALUE1: %env.VALUE1% не будет работать из-за недопустимости такого значения в yaml.
      # Также стоит уточнить, что подстановка значения будет осуществлена только в случае, если COMPOSITE_VALUE1 используется как часть команды в блоке cmd.
      ADDITIONAL_JAVA_OPTIONS: -Xmx4g            # дополнительные java опции доступны начиная с версии 20_06_05-6909128
    secrets:                                     # https://docs.yandex-team.ru/sandbox/dev/secret документация по секретам;
                                                 # для использования в из-под общего аккаунта выдавайте доступ к MOBDEVTOOLS
      aslevushkin:token1: TOKEN1                 # будет доступен в окружении как TOKEN1, нельзя передавать через -P из-за безопасности
      aslevushkin:token2: TOKEN_XXX              # как TOKEN_XXX
      some-value:sec-abc1[key]: TOKEN_YYY        # для использования секретов из общей секретницы. sec-abc1[key] - номер (ID) и ключ секрета,
                                                 # some-value будет проигнорировано.
                                                 # Чтобы начать пользоваться, следуйте инструкции https://wiki.yandex-team.ru/sandbox/yav/#permissions

    secret_files:                                # файлы из секретницы, сохраняемые в work_dir
      sec-abc1:file.txt: test.txt:MYVAR123       # секрет в yav, test.txt - имя файла под которым сохраняем секрет, MYVAR123 - переменная в которой сохраняем путь к файлу.
      sec-abc1:file_key: newfile.txt
                                                 # Результат:
                                                 #   в work_dir созданы файлы test.txt, newfile.txt.
                                                 #   в env создана переменная MYVAR123=/place/sandbox-data/tasks/..../arcadia/mobile/hypercube/android/mdm-app/newfile.txt
    kill_timeout:                                # optional, default 1800
      3600
    artifacts:                                   # публикуются на teamcity; одинаковые пути запрещены; правая часть маппинга обязательна, тк это map; подробнее в разделе ниже
      +passport/build/output: passport/output    # переместит директорию
      +passport/app/output/*.xml: app/output     # переместит файлы по маске по маске
      +passport/build/docs/**/*.txt: docs        # The “**” pattern means “this directory and all subdirectories, recursively”
      +passport/build/samples: samples.zip  # создаст архив, полезно использовать при большом количестве файлов
    internal_artifacts:                          # Позволяет передавать артефакты между stage'ами. Не публикуется на teamcity; одинаковые пути запрещены; подробнее в разделе ниже
      path/to/aars.zip: sandbox_aar_path
    caches:                                      # кэширует указанные папки, подробности ниже
      - android-sdk-linux
      - ~/.example                               # начиная с v20_03_12-6480218
    junit:                                       # добавляет результаты тестов по указанным путям во вкладку tests на teamcity. Символ '/' в конце строки приведет к тому, что будет добавлена только одна директория результатов тестов.
      - passport/build/test-results
      - passport-core/build/test-results
    multislot:                                   # подробнее про мультислоты см. ниже
      LARGE
    disk_space:
       30                                        # задает requirement к исполняемой машине: не меньше 30gb дискового пространства.
    ramdisk:
       2                                         # задает требования к размеру tmpfs, в Gb. Дефолтное значение 2. Неприменимо(игнорируется) на Macos.
  app4:   # app4 соберем в окружении где добавился ndk 21.3.6528147
    depends_on:
      - app3                                     # синтетический пример. app4 запустится после выполнения стейджа app3
    android-sdk:
      platforms(28,29,30)+tools(30.0.2)+ndk(21.3.6528147) # окружение с android_sdk версий 28..30, platform tools 30.0.2 и ndk;21.3.6528147
    certs:                                       # сертификаты в yav для подписи ios приложений
      - sec-<sec_id>:<cert_name>
      - sec-<sec_id>:<cert_name>
  app5:
    ios:
      true
    rosetta:
      true
    client_tags: USER_MONOREPO & ( OSX_BIG_SUR | OSX_CATALINA )                 # задает требования к выбору машин. В этом примере это означает запусти на Intel based Macos с Catalina или Big Sur.
    arc_exported_paths:                          # список папок экспортируемых из Аркадии (arc export)
            - hypercube/scripts
            - mobile/hypercube/android/legacy-app
```

Для Android сборок в stage-е укажите окружение android-sdk. Это sandbox ресурс с android-sdk, platform tools, выставленной переменной ANDROID_HOME и (если указано) ndk
```yaml
stages:
  app3: #app3 соберем в окружении с android-sdk 28..30 и platform tools 29.0.2
    android-sdk:
      platforms(28,29,30)+tools(29.0.2)
  ..
  app4:   # app4 соберем в окружении где добавился ndk 21.3.6528147
    android-sdk:
      platforms(28,29,30)+tools(30.0.2)+ndk(21.3.6528147) # окружение с android_sdk версий 28..30, platform tools 29.0.2 и ndk 21.3.6528147
```
Список готовых окружений можно посмотреть [тут](https://sandbox.yandex-team.ru/resources?type=ANDROID_SDK&limit=20&attrs=%7B%22ttl%22%3A%22inf%22%7D).

У каждого конфига свое имя которое указывается в `config: name: <config_name>`, оно ни на что не влияет и нужно лишь для обозначения задачи конфига.
Так как teamcity умеет отдавать BUILD_NUMBER для нумерации сборки приложений мы сделали свой аналог autoincrement as a service, подробности можно прочитать ниже. Его название необходимо указывать в `config: build_counter: <build_counter_name>`, тогда его значение автоматически попадет в переменную окружения BUILD_NUMBER.
И stages. Каждый stage имеет уникальное имя и является независимой параллельно выполняющейся единицей.
Каждый stage содержит в себе ряд параметров:
* **work_dir** — директория, из которой будут выполняться команды, и относительно которой будут забираться артефакты;
* **cmd** — shell команды, которые будут выполняться из work_dir (поддерживается несколько команд - список по правилам yaml формата), в командах можно использовать переменные окружения через %env.\<name\>% и переиспользовать файлы из других стейджей с помощью %internal.<stage_name>:<internal_file_key>%, для второго необходимо обозначить этот файл как переиспользуемый с помощью internal_artifacts;
* **internal_artifacts** - словарь, в котором указываются файлы, которые необходимо сохранить для переиспользования в других stage'ах. Эти файлы не добавляются в артефакты teamcity. Например, `path/to/aars.zip: sandbox_aar_path` скопирует файл по указанному пути во внутреннюю директорию и сохранит к нему путь в переменной `sandbox_aar_path`. В следующем stage можно будет использовать этот путь, например, через параметры грэдла: `-Pmy_path_to_aars=%internal.app3:sandbox_aar_path%` (см раздел про **cmd**).
* **depends_on** - список шагов, после завершения которых должен запуститься текущий;
  пример указания шагов:
  ```yaml
    depends_on:
            - assemble
            - test
  ```
* **fail_fast** - в случае падения текущего шага вся проверка остановится с отрицательным статусом.
* **lxc** — номер ресурса Sandbox, который является Linux Container. Рекомендуемые к использованию lxc контейнеры:
  - [1879057891](https://sandbox.yandex-team.ru/resource/1879057891/view) - java8 + пакеты для запуска android emulator
  - [2466247729](https://sandbox.yandex-team.ru/resource/2466247729/view) - java11 + пакеты для запуска android emulator
  - [2161339669](https://sandbox.yandex-team.ru/resource/2161339669/view) - только java11

   Свой контейнер можно собрать по [инструкции](https://docs.yandex-team.ru/sandbox/dev/cookbook#task_container));

* **env** — переменные окружения, заданные в виде словаря (также можно передавать дополнительные (например изменяемые в teamcity) переменные в sandbox задачу через параметр sandbox.env в teamcity. Эти параметры слиты с параметрами из config.yaml. Подробнее см. в FAQ);
* **secrets** — словарь секретов из [sandbox vault](https://sandbox.yandex-team.ru/admin/vault) или общей секретницы, где ключ — это название секрета в формате `<owner>:<secret_name>`, и значение это alias секрета. Про общую секретницу смотри пример выше. Для секретов в sandbox vault дайте доступ MOBDEVTOOLS, в yav секретам доступ нужно дать роботу robot-sbmonorepo и [проделегировать в sandbox](https://docs.yandex-team.ru/sandbox/dev/secret)
* **kill_timeout** — время в секундах, спустя которое stage будет остановлен;
* **artifacts** — пути интересующих вас файлов для группировки (поддерживается "+" как добавление файлов в артефакты и "-" как исключение файлов из артефактов). В пути разрешены "*" - см. пример конфига выше
* **junit** - пути до папок test-result с xml результатами junit тестов, нужно для отображения во вкладке tests на teamcity (в формате списка).
* **multislot** — [требования к хосту](https://wiki.yandex-team.ru/sandbox/clients/#client-tags-multislot), на котором будет выполняться данный stage. SMALL — 1CPU 4RAM, MEDIUM — 4CPU 16RAM, LARGE — 8CPU 32RAM, XLARGE - 16CPU, 64RAM.
* **disk_space** - задает требование к свободному дисковому пространству к хосту на котором выполняется задача. Размер задается в гигабайтах

## Как работает экспорт папок из Аркадии { #arcadia_export}
Teamcity Sandbox Runner примонтирует аркадию в ```TASK_DIR/arcadia```, прочитает конфиг задачи. Получит из него список экспортируемых папок.
Затем в ```TASK_DIR/export``` для каждой папки выполнит ```arc export```.
Для того чтобы не менять сборочные скрипты, ```work_dir``` выставит относительно ```TASK_DIR/export```, а не ```TASK_DIR/arcadia```.

Для того чтобы можно было пользоваться arc-ом, в окружение добавлена переменная ```ARC_WORK_TREE```, указывающая на ```TASK_DIR/arcadia```.
Из этого следует что ```arc status``` будет отображать текущее состояние примонтированной аркадии, а не папок в ```TASK_DIR/export```

Пример указания папок:
```yaml
arc_exported_paths:
    - hypercube/scripts
    - mobile/hypercube/android/legacy-app
```

## Где читать логи { #where_to_read_logs }
Для каждого запуска мы генерируем короткую html, с логами запуска команд для каждого stage(она отображается во вкладке Sandbox execution log), большую html, которая лежит в artifacts/full_index.html и текстовую версию логов которая лежит в artifacts/full_log.txt.

## Зависимые конфигурации { #dependable_configs }
Начиная с версии 20_05_26-6874170 поддержано наследование конфигураций стандартными средствами наследования yaml.

{% cut "Пример наследования yaml." %}

Создадим темплейт в аркадии по пути ```mobile/geo/maps/maps/ios/support/sandbox_arc/templates/maps_linux_env.yaml:``` с содержимым
```yaml
_template: &maps_linux_env
    work_dir:
        mobile/geo/maps/maps/ios
    secrets:
        yav:sec-01e8mp73ydq4541wbrkba0rhvn[automation-oauth-token]: FASTLANE_OAUTH_TOKEN
        yav:sec-01e8mp73ydq4541wbrkba0rhvn[arcanum-oauth-token]: FASTLANE_ARCANUM_TOKEN
        yav:sec-01e8mp73ydq4541wbrkba0rhvn[staff-password]: FASTLANE_ROBOT_PASSWORD
    kill_timeout:
        1200
    lxc:
        3200093560
    multislot:
        SMALL
```

Наследуем его в конфиге задачи:
```yaml
templates:
    - mobile/geo/maps/maps/ios/support/sandbox_arc/templates/maps_linux_env.yaml
    ...
config:
   ...
stages:

    build:
        <<: *maps_linux_env # вносим в stage build значения из темплейта maps_linux_env
        env:
            # Path parameters
            SRC_ROOT: "$PWD" # можем перекрыть значения из темплейта, заново указав их в стейдже
            ...
        cmd:
            ...
```

{% endcut %}

Для того что бы наследовать шаги tsr необходимо:
- вынести наследуемый шаблон в отдельный файл
- добавить в начало конфигурации раздел templates
```yaml
template:
  - path/to/template
```

{% note warning %}

Поддерживается наследование [только блока stages](https://st.yandex-team.ru/DEVTOOLS-7183).

{% endnote %}

## Про кэш { #cache }
По умолчанию **кэш полностью выключен** и каждая сборка герметична.
Для каждого stage каждого из конфигов можно включить сборку любой папки относительно HOME_DIR. Для этого в секции stage в параметре caches перечисляем все пути которые нужно кешировать

Пример:
```yaml
    caches:
    - ~/.gradle/caches/modules-2   #стейдж специфичный кеш.
      # К сендбоксовому ресурсу кеша в атрибуты дописывается имя стейджа. При запуске задачи, подходящие ресурсы фильтруются по имени стейджа.
    - ~/.gradle/wrapper:shared:<shared_common_name>    #расшаренный между стейджами по shared_common_name кеш. В атрибуты запишется не имя стейджа, а <shared_common_name>
      # shared кеши шарятся в рамках одной платформы (нельзя создать кеш на macos_x86 и переиспользовать его на macos_arm)
    - ~/.cocoapods:use_config_hash # обновляем кеш если изменился хеш конфига сразу же, не дожидаясь "устаревания кеша по времени"
    - ~/.test:<id ресурса с кешем> #запинненный ресурс с кешем
```

Принудительно пересобрать кеши можно указав в конфиге

   ```yaml
   force_clean_build: true
   ```

Теперь о том как устроено кеширование:

  - При запуске задачи, подходящие ресурсы фильтруются по имени стейджа (по умолчанию) либо по ```<shared_common_name>```
  - Если кеш не попадает под требование обновления кеша, привозится и распаковывается ресурс из sandbox-а.
  - Выполняется пользовательская задача.
  - На этапе завершения задачи повторно проходим по списку кешей. Если считаем что кеш нужно обновить - запаковываем папку и публикуем ее ресурсом сендбокса.


  При распаковке кеша:
  - удаляем содержимое папки куда будем распаковывать кеш.
  - распаковываем ресурс сендбокса в эту папку.

  Критерии по которым кеш нужно обновить:
  - ресурс кеша создан более 3 суток назад
  - в Teamcity (или конфиге задачи) задана опция ```force_cache_rebuild = True```
  - в конфиге кеш задан как ```- /.cocoapods:use_config_hash``` и хеш конфига отличается от хеша зашитого в атрибуты ресурса с кешем.
  - кеш не найден в Sandbox
  - статус ресурса Sandbox-а отличается от ```READY```

  Shared кеши шарятся в рамках одной платформы (нельзя создать кеш на macos_x86 и переиспользовать его на macos_arm)

Если вдруг кэш оказался сломанным, или вы хотите принудительно сбросить кэш, можно одним из способов:
- удалить ресурс с кэшом по ссылке https://sandbox.yandex-team.ru/resource/<resource_id>/view.
```id``` ресурса можно найти в ```debug.log``` по словам ```New resource for <cache> was generated```, либо по строке ```Unpack CACHE_RESOURCE: <id>```.
- перезапустить задачу, указав в Teamcity параметр ```force_clean_build: True```. В этом случае будут перегенерены все кеши во всех stage-ах

    {% cut "пример запуска Teamcity с force_clean_build: True" %}

    ![Image](https://jing.yandex-team.ru/files/r2d2/Screenshot%202022-05-12%20at%2016.11.53.png)

    {% endcut %}


## Сценарии сбора артефактов { #artifacts }
- ```source/path: dst``` сохранить директорию или файл как dst
- ```source/path/<mask>: dst``` сохранить файлы и директории из директории source/path по маске в dst
- ```source/path/**/<mask>: dst``` сохранить файлы и директории из поддиректорий source/path по маске в dst
- ```source/path: dst.zip``` сохранить артефакты как архив (так же можно использовать маску)
пример [конфигурации](https://a.yandex-team.ru/arc_vcs/mobile/infra/sandbox_runner/simple_config/config.yaml). Получившиеся артефакты можно посмотреть в одной из [сборок](https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_Infra_Sandbox_SimpleArc?buildTypeTab=overview&branch=&mode=builds)

## Про _JAVA_OPTIONS
 Если в env не задана переменная _JAVA_OPTIONS, то
 - на linux хостах _JAVA_OPTIONS будет выставлен таким образом:
     ```
      _JAVA_OPTIONS=-XX:MaxRAM=<вся доступная для задачи память> -XX:ActiveProcessorCount=<все выделенные ядра> -Djava.io.tmpdir=<путь к RAMDISK> <содержимое ADDITIONAL_JAVA_OPTIONS>
     ```
 - на macos:
     ```
      _JAVA_OPTIONS=<содержимое ADDITIONAL_JAVA_OPTIONS>
     ```
    `java.io.tmpdir` на маках не переопределяется, т.к в Sandbox маках [RAMDISK пока не поддержан](https://st.yandex-team.ru/SANDBOX-9286)

## Про android SDK и эмуляторы под Android { #android_sdk }
### Какие ресурсы с SDK уже есть? { #sdk_resources }
 [список существующих ресурсов с SDK](https://sandbox.yandex-team.ru/resources?type=ANDROID_SDK)
### Что делать с "Cannot find any 'ANDROID_SDK'"? { #how_to_create_sdk_resource }
Если при запуске вы видите подобное сообщение, это означает что нет ресурса с указанными вами версиями SDK/ndk/system-images etc
```
 SandboxEnvironmentError: Cannot find any 'ANDROID_SDK' 'sdk_28-30+tools_30.0.3' resource for Sandbox environment (query: {'state': 'READY', 'type': 'ANDROID_SDK', 'attrs': {'version': 'sdk_28-30+tools_30.0.3'}}).
```

Что делать:
1. Запускаем задачу [ANDROID_SDK_PREPARER_2](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=ANDROID_SDK_PREPARER_2), указываем какие пакеты должны оказаться в ресурсе.
Если указать `Android SDK2 preparer 2's task release type: stable`, запустится стабильный релиз preparer-а (что вам не важно), и собранному ресурсу выставится `ttl=inf`

Результатом запуска примера из скриншота является [ресурс](https://sandbox.yandex-team.ru/resource/2293932597/view) с version `platforms(28,29,30)+tools(30.0.2)+system-images(android-29;google_apis;x86_64)`.
3. В конфиге своей сборки указываем в параметре 'android-sdk' версию:
```yaml
  'android-sdk': 'platforms(28,29,30)+tools(30.0.2)+system-images(android-29;google_apis;x86_64)'
```

### Что нужно сделать для запуска тестов с эмулятором { #run_test_with_emulator }
 1. Указать [lxc контейнер с java8](https://sandbox.yandex-team.ru/resource/1879057891/view) или [lxc контейнер с java11](https://sandbox.yandex-team.ru/resource/2466247729/view).
 В задачах [844199110](https://sandbox.yandex-team.ru/task/844199110/view) или [1088865119](https://sandbox.yandex-team.ru/task/1088865119/view) по сборке контейнера можно посмотреть что в них входит.
 2. Использовать нужный вам [android-sdk](https://sandbox.yandex-team.ru/resources?author=r2d2&children=true&type=ANDROID_SDK&limit=20&created=6_months). Настоятельно рекомендуем использовать system-images с **google_apis** - версии с default api (например system-images;android-29;default;x86) не могут установить ssl handshake к нашим серверам. //эту проблему решим отдельно//. В параметр emulator_system_images вписываем "кусок" system-images из android-sdk.
 пример использования:
```yaml
  'android-sdk': 'platforms(28,29,30)+tools(30.0.2)+system-images(android-29;google_apis;x86_64)'
  'emulator_system_images': android-29;google_apis;x86_64
  'emulator_device_skin': pixel_5 # дефолтное значение - Nexus 5
```

Эмулятор создается перед выполнением теста [вот этим кодом](https://a.yandex-team.ru/arcadia/sandbox/projects/mobile_apps/utils/android_sdk_env/__init__.py).

Параметр ```emulator_device_skin``` пробрасывается as is в вызов ```avdmanager ... -d <emulator_device_skin>```

Задать размер диска для эмулятора можно так (по дефолту - 1024мб)
```
  'emulator_disk_size': 2  # 2048mb
```


## Выбор машин тегами сендбокса { #client_tags }
TSR использует нативные сендбоксовые теги.
- Версии осей требуется писать строго в [сендбоксовом](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/deploy/client.py?rev=r8571333#L357) стиле, пример: ``OSX_BIG_SUR | OSX_CATALINA``.
- Необходимо явно указывать ``USER_MONOREPO`` для выбора ``mobile-mac*`` машин.

Примеры тегов с выбором платформы:

- запуск только на x86, big sur или catalina:

    ``client_tags: USER_MONOREPO & ( OSX_BIG_SUR | OSX_CATALINA )``

- запуск только на M1, big sur или catalina:

    ``client_tags: ( M1 & USER_MONOREPO ) & ( OSX_BIG_SUR | OSX_CATALINA )``

- запуск на маке любой архитектуры:

    ``client_tags: (( M1 & USER_MONOREPO ) | USER_MONOREPO )  & ( OSX_BIG_SUR | OSX_CATALINA )``

Есть отдельный [тикет](https://st.yandex-team.ru/DEVTOOLSSUPPORT-11570) про упрощение выражений выбора архитектуры.


## Сборка ios { #ios }
### Запуск сборки на mac машине { #run_on_mac }

```yaml
   ios:                                         # запустить сборку на mac
     true
   client_tags: ( M1 & USER_MONOREPO ) & ( OSX_BIG_SUR | OSX_CATALINA ) #запустить на M1, с big sur или catalina.
```

### Сертификаты для сборки приложений (Добавление сертификатов в keychain) { #keychain }
Что бы добавить сертификат для сборки (iOS Distribution сертификаты для 'Yandex LLC' и 'Yandex, LLC') в keychain необходимо создать секрет в yav с сертификатом как ```<cert_name>.p12``` в yav и паролем от сертификата под именем ```<cert_name>_pass```.
Секреты необходимо [проделегировать в sandbox](https://wiki.yandex-team.ru/sandbox/yav/#permissions) и дать к ним в yav доступ на чтение роботу robot-sbmonorepo
```yaml
 certs:
  - sec-<sec_id>:<cert_name>
  - sec-<sec_id>:<cert_name>
```

### Provision Profiles { #provision_profiles }
Профайлы на всех сборочные маки сендбокса раскладываются из [репозитория](https://bitbucket.browser.yandex-team.ru/projects/MT/repos/mobile-ios-provisioning-profiles/browse).
Механика привоза:
- Если испрользуется общий аккаунт Yandex LLC, то при генерации профайла используйте сертификат, который истекает 15 февраля 2023г (iOS Distribution). Сам сертификат лежит в секрете: `sec-01etab4be7nn5jnfcs03s11qz0` (добавить в certs).
- На коммит в master в bitbucket с профилями, [триггерится](https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_SandboxProvisioningProfiles) сборка ресурса [PROVISION_PROFILE](https://sandbox.yandex-team.ru/resources?type=PROVISION_PROFILE&limit=10). Ресурсы маркируются хешем коммита.
- При запуске TSR, привозится и распаковывается в ``/Users/isandbox/Library/MobileDevice/Provisioning Profiles`` последний собранный ресурс ``PROVISION_PROFILE``. (в логе указывается ``id`` и ``hash`` ресурса и задача в которой он был собран.
Задержка между коммитом и созданием ресурса обычно минут 15.


### Xcode { #xcode }
Для того что бы использование Xcode разных версий на одном хосте было возможно, мы написали свой [xcode-sandbox-environment](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/sdk2/environments.py?rev=6972840#L1601), который позволяет подменять исходники подменой симлинка. Для того что бы использовать Xcode в своей сборке, добавьте в каждый шаг параметр ```xcode: '<xcode_version>'```, например ```xcode: '11.2.1'```.

{% note warning %}

Версию надо указывать в кавычках

{% endnote %}

Xcode устанавливается из ресурса [XCODE_ARCHIVE](https://sandbox.yandex-team.ru/resources?type=XCODE_ARCHIVE).
Чтобы добавить ресурс со своей версией Xcode, скачайте xip архив с [сайта apple](https://developer.apple.com/download/more/), и залейте его в sandbox:

```shell script
ya upload Xcode_11.5.xip --ttl inf --attr platform="darwin" --attr version=_11.5 -T=XCODE_ARCHIVE --token <сендбокс токен> --owner <ваша группа в Sandbox>
```

Note: [почитать про группы в Sandbox](https://docs.yandex-team.ru/sandbox/groups)


{% cut "Для разработчиков" %}

Перед тем как использовать multi-xcode запустите задачу XCODE_CLEANER на хостах.

{% endcut %}

### Rvm+Ruby { #rvm_ruby }
Для того что бы установить требуемую версию rvm и ruby:
- запустите задачу [RVM_PLUS_RUBY_PREPARER](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=RVM_PLUS_RUBY_PREPARER) с нужной версией
- добавьте параметр ```rvm+ruby: <rvm_version>+<ruby_version>```, например ```rvm+ruby: 1.29.10+2.4.1```

## Версионирование { #versioning_policy }
Для того что бы не ломать чужие сборки, а так же для возможности сборки старых версий мы придумали версионирование. Что бы включить его, необходимо добавить один из номеров версий представленных ниже в конфиг. В случае если версия не указана, будет использована последняя версия.

## Версии { #versions }
**новый формат: YYYY.MM.DD-revision**
- 2022.07.28-9784758
- 2022.06.28-9646330
- 2022.06.20-9611528
- 2022.06.07-9557897
- 2022.05.22-9462912
- 2022.05.12-9447471
- 2022.04.08-9329261
- 2022.02.17-9158232
- 2022.01.21-9055701
- 2022.01.13-9026471
- 2021.12.17-8960012
- 2021.09.27-8673273
- 2021.09.23-8660765
- 2021.09.01-8582214
- 2021.08.27-8567613
- 2021.08.13-8526733
- 2021.08.06-8497613
- 2021.07.19-8430304
- 2021.07.07-8384872
- 2021.06.25-8333125
- 2021.05.31-8226377
- 2021.05.25-8195898
- ~~2021.05.18-8178343~~
- 2021.02.19-7876472
- 2021.02.08-7832518
- 2020.11.26-7626255
- 2020.10.22-7487013
- 2020.10.14-7469356
- 2020.08.26-7257842

{% cut "версии в старом формате (до 2020.08.xx): YY_MM_DD-revision" %}

**формат (старый): YY_MM_DD-revision**
- 20_08_05-7177903
- 20_07_10-7100354
- 20_06_29-7052148
- 20_06_10-6921310
- 20_05_26-6874170
- 20_05_07-6766902
- 20_03_12-6480218
- 20_02_22-6405432
- 20_02_03-6315463
- 20_01_07-6195706
- 19_11_28-6021277
- 19_10_25-5857160

{% endcut %}

## Changelog { #changelog }

### 2022.07.28-9784758 { #2022.07.28-9784758 }
- [учитываем /etc/profile](https://st.yandex-team.ru/MOBDEVTOOLS-602). Вернули чтение `/etc/profile` и делаем теперь это в правильном месте - в самом начале, до привоза любых enviroment-ов.
- [не выставляем ограничения на ядра и память для Java на маках](https://st.yandex-team.ru/MOBDEVTOOLS-608)
- [бекапим сборочные артефакты в S3 c ttl=1](https://st.yandex-team.ru/MOBDEVTOOLS-598)

### 2022.06.28-9646330 { #2022.06.28-9646330 }
- [Дополнительные опции задания кешей](https://st.yandex-team.ru/MOBDEVTOOLS-593)
   - Можно завязать обновление кеша на изменение конфига.
   - Можно расшарить кеш между стейджами по заданному пользователем <shared_common_name> кеша
- [Не ломаем PATH выставленный ruby_rvm окружением несвоевременным чтением /etc/profile](https://st.yandex-team.ru/MOBDEVTOOLS-594)
  Note: чтение /etc/profile нужно для android сборок и будет сделано перед привозом окружений в MOBDEVTOOLS-602
- [добавили ANDROID_SDK_ROOT](https://st.yandex-team.ru/MOBDEVTOOLS-595)

  Все доступные сейчас варианты задания кешей:
  ```yaml
  - ~/.gradle/caches/modules-2   #стейдж специфичный кеш
  - ~/.cocoapods:use_config_hash #обновить кеш если изменился хеш конфига
  - ~/.gradle/wrapper:shared:<shared_common_name>    #расшаренный по shared_common_name кеш
  - ~/.test:<id ресурса с кешем> #запинненный ресурс с кешем
  ```

  кеш безусловно обновляется если
   - если задан force_cache_rebuild
   - если у в конфиге кеш задан как "- /.cocoapods:use_config_hash" и хеш конфига отличается от хеша зашитого в атрибуты ресурса с кешем.

  shared кеши шарятся в рамках одной платформы (нельзя создать кеш на macos_x86 и переиспользовать его на macos_arm)

### 2022.06.20-9611528 { #2022.06.20-9611528 }
- [Экспорт больше не ломается на пересекающихся путях](https://st.yandex-team.ru/MOBDEVTOOLS-543)
  Теперь можно указать пути с пересечением:
  ```
          arc_exported_paths:
            - hypercube/scripts
            - mobile/yaz
            - mobile/hypercube/android/legacy-app
  ```

### 2022.06.07-9557897 { #2022.06.07-9557897 }
- [Недоступность машины в момент сбора логов](https://st.yandex-team.ru/MOBDEVTOOLS-584) больше не фейлит сборку. TEAMCITY_SANDBOX_RUNNER после выполнения всех стейджей, пытается собрать логи от подзадач TEAMCITY_SANDBOX_RUNNER_STAGE (где собственно и происходит сборка приложений). Если в этот момент машина на которой выполнялся stage будет недоступна - RUNNER попытается несколько раз достать логи и затем перейдет к логам следующего stage. Раньше в этом месте RUNNER, LAUNCHER и сборка в Teamcity красились в красный цвет с результатом NO_RES.
Что означает это решение на практике:
    - если сборка упала _И_ машина была недоступной - логи не попадут в тимсити, их нужно будет смотреть в сендбоксе.
- [Можно зафорсить использование определенного ресурса с кешем](https://st.yandex-team.ru/MOBDEVTOOLS-589), добавив к заданию кеша id ресурса после двоеточия.
 в формате ```[путь кешируемой папки]<:resource_id>```:
    ```
            caches:
          - ~/.konan
          - ~/.cocoapods:3183292512
    ```
- [Починили сломаные симлинки в кешах](https://st.yandex-team.ru/MOBDEVTOOLS-590)
    - симлинк при запаковке разыменовывается (на папку и на файл)
    - если симлинк сломан - он скипается.
    - если в кешируемой папке есть пустые папки - они пропадут (это особенность zipfile и она была всегда).

### 2022.05.22-9462912 { #2022.05.22-9462912 }
- Параметризовали [emulator_device_skin](https://a.yandex-team.ru/review/2538860/details) для запуска Android эмулятора

### 2022.05.12-9447471 { #2022.05.12-9447471 }
- задокументировали логику работы с кешами
- сбросить кеши теперь можно перезапустив сборку в Тимсити (больше не нужно коммитить параметр в stage)
- отрефакторили сборку кешей (убрали неиспользуемые сущности, упростили код)
- починили [баг с безусловной очисткой папки-приемника кеша](MOBDEVTOOLS-576). Ранее, если ресурс не существовал или был в состоянии отличном от READY, папку приемник все равно очищали.

### 2022.04.08-9329261 { #2022.04.08-9329261 }
- [уменьшили количество писем](https://st.yandex-team.ru/MOBDEVTOOLS-149) отправляемых в mobdevtools-dev@
- [Добавили возможность задать хост для выполнения задачи](https://st.yandex-team.ru/MOBDEVTOOLS-557) для отладочных целей:

В Teamcity для этого нужно добавить один из параметров в сборку, указав в значении желаемый хост.
- ```sandbox.mac_agent```
- ```sandbox.linux_agent```

Учтите, что все линуковые stage запустятся на одном sandbox.linux_agent, все mac-овые - на одном sandbox.mac_agent.
Формат задания хоста укороченный, так как это используется в sandbox-е. Пример:

    sandbox.mac_agent: mobile-mac039


### 2022.02.17-9158232 { #2022.02.17-9158232 }
- добавили ретраи в течение 5 минут на сбор артефактов от TEAMCITY_SANDBOX_RUNNER_STAGE (это сделано для того чтобы не ломаться если mac машина моргнула).

### 2022.01.21-9055701 { #2022.01.21-9055701 }
 - Останавливаем выполнение дочерних задач (раньше они продолжали работать, занимая вычислительные мощности)
 - Починили пару мест которые могли зациклить выполнение задачи:
   - Проверяем что стейдж указанный в %internal.<stage_name> действительно существует в конфиге
   - В списках depends_on, waiting не храним дубликаты стейджей.
 - Починили сбор артефактов для неаркадийных репозиториев

### 2022.01.13-9026471 { #2022.01.13-9026471 }
 - [сделали кеши платформозависимыми](https://st.yandex-team.ru/MOBDEVTOOLS-536).

### 2021.12.17-8960012 { #2021.12.17-8960012 }
 - [уменьшили время хранения Internal артефактов](https://st.yandex-team.ru/MOBDEVTOOLS-481) до 1 дня
 - [добавили параметр emulator_disk_size](https://st.yandex-team.ru/MOBDEVTOOLS-509) для размера партиции в android эмуляторе
 - [изменили поведение env.ARCADIA_ROOT](https://st.yandex-team.ru/MOBDEVTOOLS-504). Теперь эта переменная указывает на export/mounted arcadia (раньше указывала строго на примонтированную аркадию)
 - отрефакторили часть artifact_processor. Добавили  поддержку tgz архивов. Сделаны интеграционные тесты + небольшое количество unit тестов для этого модуля.

### 2021.09.27-8673273 { #2021.09.27-8673273 }
 - [пофиксили баг](https://st.yandex-team.ru/MOBDEVTOOLS-474) который приводил к тому что удаление ресурса в сендбоксе не запускало генерацию новой версии ресурса.

### 2021.09.23-8660765 { #2021.09.23-8660765 }
 - Добавили определение платформы (linux, macos x64, macos arm).
   - Во время выполнения подкачивается ресурс под нужную платформу (сейчас это должно работать только для ruby+rvm).
   - Команды указанные в cmd выполняются под нативной архитектурой (на практике это означает что для arm команды выполняются не под Rosetta-ой)
   - При этом можно переопределить платформу для arm, указав в для stage-а:

       ```rosetta: true```

 - Добавили возможность [экспортировать папки из Arcadia](#arcadia_export)
 - Добавили переменную ``ARCADIA_ROOT``, содержащую абсолютный путь до корня аркадии.
 - Уменьшили время хранения кешей TeamcitySandboxRunnerCache с 14 до 7 суток, т.к они объемные и забивают место на mobile-mac0*.techadmin.yandex.net машинах.
 - Починили баг с отключением gradle daemon: пишем опцию ``org.gradle.daemon=false`` в корректное место.

### 2021.09.01-8582214 { #2021.09.01-8582214 }
   - TLDR: перешли на нативные сендбоксовые теги.
    Для того чтобы все продолжило работать как есть:
     - переименуйте поле ``osx_version`` в ``client_tags``.
     - к версии оси добавьте префикс ``OSX_``: ``BIG_SUR`` -> ``OSX_BIG_SUR``
     - добавьте к списку осей выражение ``USER_MONOREPO & ``: ``OSX_BIG_SUR`` -> ``USER_MONOREPO & OSX_BIG_SUR``

- Детали:
     - На маках поддержали выбор архитектуры M1/X86.
     - Используем нативные сендбоксовые теги.
       - Больше нельзя писать версию оси как ``CATALINA`` или ``BIG_SUR``. Требуется писать строго в [сендбоксовом](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/deploy/client.py?rev=r8571333#L357) стиле, с префиксом ``OSX_``, пример: ``OSX_BIG_SUR | OSX_CATALINA``.
       - Поле osx_version заменили на ``client_tags``.
       - Необходимо явно указать ``USER_MONOREPO`` для выбора ``mobile-mac*`` машин.

       Примеры тегов с выбором платформы:

       - запуск только на x86, big sur или catalina:

         ``client_tags: USER_MONOREPO & ( OSX_BIG_SUR | OSX_CATALINA )``

       - запуск только на M1, big sur или catalina:

          ``client_tags: ( M1 & USER_MONOREPO ) & ( OSX_BIG_SUR | OSX_CATALINA )``

       - запуск на маке любой архитектуры:

         ``client_tags: (( M1 & USER_MONOREPO ) | USER_MONOREPO )  & ( OSX_BIG_SUR | OSX_CATALINA )``

    Есть отдельный [тикет](https://st.yandex-team.ru/DEVTOOLSSUPPORT-11570) про упрощение выражений выбора архитектуры.

   - Починили баг с поиском linux-овых машин если в конфиге не задан multislot. Раньше таким задачам не назначался тег LINUX и они долго простаивали в очереди.
   - Перестали использовать deprecated sandboxsdk.errors

### 2021.08.27-8567613 { #2021.08.27-8567613 }
   - Не завязаны больше на выкладку сендбокса в раскладке provision profiles:
        - На коммит в master в bitbucket с профилями, [триггерится](https://teamcity.yandex-team.ru/buildConfiguration/MobileNew_Monorepo_SandboxProvisioningProfiles) сборка ресурса [PROVISION_PROFILE](https://sandbox.yandex-team.ru/resources?type=PROVISION_PROFILE&limit=10). Ресурсы маркируются хешем коммита.
        - При запуске TSR, привозится и распаковывается в ``/Users/isandbox/Library/MobileDevice/Provisioning Profiles`` последний собранный ресурс ``PROVISION_PROFILE``. (в логе указывается ``id`` и ``hash`` ресурса и задача в которой он был собран.
   - Задали дополнительные атрибуты в поиске бинарных задач, чтобы уменьшить потребление квоты [SB api](https://grafana.yandex-team.ru/d/000016022/sandbox-api-stats-for-user-production?orgId=1&var-quota_owner=MOBDEVTOOLS&from=now-2d&to=now)

### 2021.08.13-8526733 { #2021.08.13-8526733 }
   - Собрали версию с учетом [правок в sandbox](https://a.yandex-team.ru/review/1948102/details).
   - Можно задать размер tmpfs опцией ramdisk. [Тикет](https://st.yandex-team.ru/MOBDEVTOOLS-423)
   - При перегенерации кешей [учитывается текущее время с часовым поясом](https://st.yandex-team.ru/MOBDEVTOOLS-366)

### 2021.08.06-8497613 { #2021.08.06-8497613 }
   - Используем машины сендбокса с тегом MOBILE_MONOREPO. См [тикет](https://st.yandex-team.ru/SANDBOX-8956) о переезде на abcd ресурсы

### 2021.07.19-8430304 { #2021.07.19-8430304 }
   - [логируем](https://st.yandex-team.ru/MOBDEVTOOLS-398) каждый этап подготовки окружения
   - починили запуск эмулятора Android-а. Заодно перешли на новый ресурс android-sdk с эмулятором. При этом пришлось немного поменять формат указания версии ресурса.
     было:
        ```yaml
        'android-sdk': 'sdk_28-30+tools_29.0.2+packages:system-images;android-29;google_apis;x86_64'
        'emulator_system_images': system-images;android-29;google_apis;x86_64
        ```
     стало:
        ```yaml
        'android-sdk': 'platforms(28,29,30)+tools(30.0.2)+system-images(android-22;default;x86)'
        'emulator_system_images': 'android-29;google_apis;x86_64'
        ```

### 2021.07.07-8384872 { #2021.07.07-8384872 }
   - исправили досадный [баг](https://st.yandex-team.ru/MOBDEVTOOLS-366) с регенерацией кешей
   - убрали синхронную [заливку](https://st.yandex-team.ru/MOBDEVTOOLS-368) артефактов в S3
   - во время выполнения cmd операций можно использовать переменную SANDBOX_TASK_LOG_DIR для обращения к папке с логами сендбокса
   - выставляем явно [TEAMCITY_VERSION=1](https://st.yandex-team.ru/MOBDEVTOOLS-374) в окружение. Считаем это [признаком](#platform_environment) того что задача запущена в сендбоксе.
   - пофиксили [баг](https://st.yandex-team.ru/MOBDEVTOOLS-378) из-за которого тратили время на привоз xcode на маки, даже если он не требуется

### 2021.06.25-8333125 { #2021.06.25-8333125 }
   - монтируем arc с опцией --vfs-version 2 [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-359)
   - [поддержали](https://st.yandex-team.ru/MOBDEVTOOLS-349) множественное указание версии оси в поле osx_version:
     ```yaml
     osx_version:
       OSX_CATALINA | OSX_BIG_SUR
     ```
     Note: указывать версию лучше в [нативном](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/deploy/client.py?rev=r8333345#L319) для сендбокса формате, с `OSX_` в начале строки
### 2021.05.31-8226377 { #2021.05.31-8226377 }
   - добавили сохранение пути к секретному файлу в env:
     Было: `'sec-abc1:key': 'имя файла под которым сохранить содержимое'`
     Стало: `'sec-abc1:key': 'имя файла под которым сохранить содержимое:переменная окружения в которой нужно сохранить путь к файлу'`
     Конфиг:
     ```yaml
         work_dir:
            mobile/hypercube/android/mdm-app/
         secret_files:
            sec-01ey98z5njqf4hpwmr4qxsmj7z:test.txt: test.txt:MYVAR123
            sec-01ey98z5njqf4hpwmr4qxsmj7z:file_key: newfile.txt
      ```
     Результат:
        в work_dir созданы файлы test.txt, newfile.txt.
        в env создана переменная MYVAR123=/place/sandbox-data/tasks/..../arcadia/mobile/hypercube/android/mdm-app/newfile.txt

### 2021.05.25-8195898 { #2021.05.25-8195898 }
   - храним файлы в yav. Файлы из секретницы скачиваются в work_dir. Формат:
     `'sec-abc1:key': 'имя файла под которым сохранить содержимое'`
     пример:
     `secret_files: {'sec-01ey98z5njqf4hpwmr4qxsmj7z:test.txt': 'test.txt','sec-01ey98z5njqf4hpwmr4qxsmj7z:file_key': 'newfile.txt'}`
   - пишем в teamcity_messages.log время затрачиваемое на выполнение этапа сборки в [формате](https://www.jetbrains.com/help/teamcity/service-messages.html#Reporting+Build+Statistics) тимсити для построения графиков
   - --добавили подстановку переменных из env.--
     --Можно задать переменную, значение которой вычислится с использованием переменной из env: `PKG_ROOT: composite_%env.TMP%/root`--
   - ждем запуска эмулятора при старте

### 2021.02.19-7876472 { #2021.02.19-7876472 }
   - заливаем кеши и артефакты в mds - уходим от нестабильного хранилища сендбокса.
### 2021.02.08-7832518 { #2021.02.08-7832518 }
   - монтируем аркадию с fetch_all=False. Это убрало излишнюю нагрузку на arc. [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-246)
   - мелкие фиксы:
     - добавили дополнительный параметр к задаче - custom_config_commit [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-230). Решаемая задача: конфиг сборки и код приложения хранятся в разных репозиториях, Teamcity мониторит изменения в коде. Нужно как-то передавать расположение конфига в TSR.
     Репозиторий и бранч можно переопределить в тимсити в переменных окружения, а для коммита пришлось делать отдельное поле т.к тимситевый плагин обрабатывает переменную commit по-особому.
     - Валидатор запрещает пустой path в artifacts. Ранее этого не требовалось, что приводило к падению задачи в рантайме. [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-62)
     - Починил ошибку с некорректной регулярков при формировании html отчета, заодно починился подсчет затраченного времени на этапы [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-57)

### 2020.11.26-7626255 { #2020.11.26-7626255 }
   - отключили анимацию в эмуляторе
   - починили баг при запуске эмулятора (неверно создавали cmd строку)
   - добавили отлов эксепшна SubprocessError при клонировании репозитория - теперь должны ретраить клонирование в этом случае. [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-123)
   - сделали понятнее (надеюсь) сообщение об ошибке при указании абсолютных путей артефактов [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-106)
   - добавили возможность затребовать машину с определенным размером диска [тикет](https://st.yandex-team.ru/MOBDEVTOOLS-159)
     В примере требуем машину с 30Gb:
     в секции assemble пишем
     ```yaml
        disk_space:
          30
     ```
   - починили баг с неверным указанием "MaxRAM=0G", если не был задан multislot

### 2020.10.22-7487013 { #2020.10.22-7487013 }
   - добавили тип требований к хосту: <['XLARGE': 16CPU, 64GB RAM]>
   - поправили баг при создании архива кешей
### 2020.10.14-7469356 { #2020.10.14-7469356 }
   - добавили создание эмулятора во время запуска TSR [beta]
   - добавили retry на чекаут репозитория
   - поменяли работу с кешами
   - добавили возможность принудительно обновить кеши, задав параметр `force_clean_build: true`
   - локальный архив кешей обновляем если они старее 3 суток и время выполнения задачи < 12 часов дня. Т.е в основное рабочее время не тратим на это время.
   - в системный environment пробрасываем `TC_BUILD_ID`
   - TSR по умолчанию запускается с dns64 - это позволит делать чекаут из github.com
   - в секции artifacts можно использовать переменные из env
```yaml
  env:
    PARAM: param
  artifacts:
    +repo/%env.PARAM%/*.jar: jars <<< здесь подставится param
```
   - для ios задач добавили requirement USER_MONOREPO. Это позволит команде mobdevtools оперативно управлять сборочным пулом машин добавляя пользовательский тег USER_MONOREPO на машины.
   - убрали отправку статистики cocoapods - сэкономили 30 секунд
### 2020.08.26-7257842 { #2020.08.26-7257842 }
   - Добавлена поддержка окружения 'android-sdk'. Доступные варианты: `sdk_28-30+tools_28.0.3`, `sdk_28-30+tools_29.0.3` и `sdk_28-30+tools_30.0.2`, `sdk_28-30+tools_28.0.3+ndk_21.3.6528147`, `sdk_28-30+tools_29.0.3+ndk_21.3.6528147` и `sdk_28-30+tools_30.0.2+ndk_21.3.6528147`.
     другие варианты сделаем по запросу.
Окружение – это одна или несколько `platforms`, `build-tools`, `ndk`, переменная окружения `ANDROID_HOME`. В окружении удалена папка `emulators` для экономии места и `licenses` (для герметичности). Вместе в этим окружением рекомендуется использовать LXC: [1879057891](https://sandbox.yandex-team.ru/resource/1879057891/view), в котором нет вшитого Android SDK. Примеры миграции на новую версию можно посмотреть тут:
   - https://a.yandex-team.ru/review/1405005/files - sdk + tools
   - https://a.yandex-team.ru/review/1439223/files - sdk + tools + ndk

{% cut "предыдущие версии" %}

### 20_08_05-7177903 { #20_08_05-7177903}
   - исправлены проблемы с зависимыми шагами
### 20_07_10-7100354 { #20_07_10-7100354}
   - листинг рабочего дерева остался только в версии test
   - добавлены ssl сертификаты для ios сборки
   - кэши собираются только при успешной сборке
   - отключен gradle daemon
### 20_06_29-7052148 { #20_06_29-7052148}
   - исправлены проблемы прошлой версии
   - добавлено дерево рабочей директории в логи
   - добавлены provision profiles
   - добавлена возможность добавления сертификатов в keychain
### 20_06_10-6921310 { #20_06_10-6921310}
   - переписан модуль для обработки артефактов
   - добавлена переменная окружения ADDITIONAL_JAVA_OPTIONS
   - изменен формат логгирования
### 20_05_26-6874170 { #20_05_26-6874170}
   - добавлена поддержка сложных переменных окружени
   - добавлена поддержка зависимых конфигураций
### 20_05_07-6766902 { #20_05_07-6766902}
   - исправлена проблема с парсингом путей артефактов
   - исправлена проблема с невозможностью ручного запуска
   - исправлена проблема с rvm_ruby
   - добавлена поддержка секретов из teamcity параметров
   - добавлена поддержка build_counter-ов из сторонних квот
### 20_03_12-6480218 { #20_03_12-6480218 }
   - версия аналогична версии без приписки p, содержит патч на arcadia/mobile, что бы конфиги работали без исправлений относительно bb (нужно для переезда)
### 20_03_12-6480218 { #20_03_12-6480218 }
   - добавлена поддержка кэширования относительных путей
### 20_02_22-6405432 { #20_02_22-6405432 }
   - добавлена поддержка arc-а
### 20_02_03-6315463 { #20_02_03-6315463 }
   - добавлена поддержка ios(на тестировании у нескольких команд)
   - добавлена поддержка произвольного названия конфигурации
   - объявление кэшей стало обязательным
   - запуск команд с использованием ssh ключа из параметров
### 20_01_07-6195706 { #20_01_07-6195706 }
   - добавлен процессинг teamcityMessage из логов
   - поддержана общая секретница
### 19_11_28-6021277 { #19_11_28-6021277 }
   - исправлен баг с двойными логами
   - исправлен баг с маппингом файлов
   - добавлены _JAVA_OPTIONS -XX:MaxRAM и -XX:ActiveProcessorCount
   - версионирование стало обязательным

{% endcut %}

## Teamcity агенты { #teamcity_agents}
Так как единственная задача teamcity агентов при запуске TSR - это скачивание ресурсов с sandbox, подойдет агент с любым железом. Для этих целей мы налили маленьких агентов `generic-teamcity-runner*`. Что бы начать их использовать нужно поменять Agent Requirements. И отключить VCS checkout в VCS control settings. Что бы удостовериться что все настроено правильно, зайдите на страницу **Compatible agents** и проверьте что нет конфликтов требований(Implicit requirements) у выбранных агентов и они значатся совместимыми.

## FAQ { #FAQ }
### Не опубликовались артефакты { #artifacts_not_published }
   Скопируйте TEAMCITY_SANDBOX_RUNNER_STAGE задачу того стейджа, артефакты которого не опубликовались. В параметре artifacts укажите путь несколькими директориями выше, тогда после выполнения скопированной задача, в ее ресурсах будет ресурс teamcity_artifacts, в котором можно будет посмотреть, что должно содержаться в интересующем вас месте. Если там все же оказались файлы, но в артефактах их нет, напишите нам.
###  Не пробросились секреты { #can_t_see_artifacts }
Если вам кажется что указанные вами секреты не пробросились, и вы пытаетесь напечатать их приложением, то при выводе вы увидите '' вместо секрета, так как sandbox скрывает все используемые задачей секреты. Правильнее проверять например длину токена, тогда вывод этой информации не будет скрыт.

### Получили ошибку Mount failed { #mount_failed }
Чтобы начать использовать arc, положите токен с именем ARC_TOKEN в [Sandbox vault](https://sandbox.yandex-team.ru/admin/vault) и пошарьте с owner-ом задачи. Это нужно сделать один раз для каждого возможного owner-а. [Как получить ARC_TOKEN](https://docs.yandex-team.ru/devtools/intro/auth#repo-oauth)

### Тестов стало меньше { #tests_number_decreased }
Убедитесь в том, что вы указали все папки с результатами тестов, а проверить это проще всего запустив локально после прогона тестов команду `find . -name "test-results"`

### Как теперь проверить, что мы запущены в Sandbox-е { #platform_environment }
`System.getenv("TEAMCITY_VERSION") != null`

### Не работает сгенерированный ssh-ключ { #ssh_key_not_working }
Подробности про создание ssh ключа можно найти на странице [документации](https://wiki.yandex-team.ru/sandbox/vault/#primersssh-kljuchomnerabotaet) sandbox. Отдельный важный момент, что ключ нужно создавать размером 2048 и под Linux (например временно создать VM из tmp квоты в [QYP](https://qyp.yandex-team.ru/)).

### Как передавать произвольные переменные из teamcity { #pass_variables }

см. [раздел про добавление переменных в Teamcity](#step_4_change_build_parameters)

### Не работает заливка iOS-приложения в бету { #upload_to_beta }
 - обновить fastlane до версии >= 2.190.0
 - [Решение Ильи Лобанова](https://st.yandex-team.ru/DEVTOOLSSUPPORT-6888#60e4cc05def03a30631a4309)

### Сборка iOS-приложения не загружается в AppStoreConnect { #upload_to_appstoreconnect }

Из-за того что инструменты для загрузки артефактов в AppStoreConnect (altool, iTMSTransporter) зачастую пытаются работать только через IPv4, то загрузка не работает (mobile-mac машины ходят во внешнюю сеть по IPv6). Ситуацию можно опознать по наличию в логах чего-то подобного:
     `INFO: An error occurred checking the HEAD for: https://contentdelivery.itunes.apple.com/transporter/repositories/j2se8/latest/repository.xml contentdelivery.itunes.apple.com Exception's name: java.net.UnknownHostException, Exception's message: contentdelivery.itunes.apple.com`

Если для загрузки используется напрямую вызов `altool`, можно попробовать установить в `defaults` значение ключа `ITunesTransporterExtraArgs` в '-Djava.net.preferIPv4Stack=false’ до вызова `altool`:
     `defaults write NSGlobalDomain ITunesTransporterExtraArgs '-Djava.net.preferIPv4Stack=false’`
     И удалить после:
     `defaults delete NSGlobalDomain ITunesTransporterExtraArgs`

Если для загрузки используются action'ы в `Fastlane deliver` или `upload_to_testflight`, то можно попробовать установить следующую переменную окружения:
     `DELIVER_ITMSTRANSPORTER_ADDITIONAL_UPLOAD_PARAMETERS='-Djava.net.preferIPv4Stack=false'`

{% note warning %}

Эти способы работают с инструментами идущими в поставке `Xcode 12.4`, но неизвестно будут ли они работать в будущем.

{% endnote %}

### Не приняты лицензии Android SDK { #android_sdk_licenses_not_accepted }
```
Failed to install the following Android SDK packages as some licences have not been accepted.
    build-tools;30.0.2 Android SDK Build-Tools 30.0.2
To build this project, accept the SDK license agreements and install the missing components using the Android Studio SDK Manager.
Alternatively, to transfer the license agreements from one workstation to another, see http://d.android.com/r/studio-ui/export-licenses.html
```

1. Разные `build-tools` нежелательно миксовать, потому с ними поставляется линт и правила (которые, собственно, зависят от версии `build-tools`), т.е. если билд проходит на `29.0.0`, это не значит, что он пройдёт на `30.0.0`
2. Версию `build-tools` (если она явно не задана) выбирает как-то хитро `agp` - у него есть как минимальная версия, так и возможность взять что-то чуть выше, т.е. это плохо контролируется
По этим причинам мы жёстко фиксируем версию `build-tools` в образе, а чтобы `agp` не сходил и не скачал свежую (это вообще адовая негерметичность вообще!), после установки всего мы делаем тупо `rm -rf licenses` ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/mobile_apps/android_resource_preparer/__init__.py?rev=r7751576#L43))

### Сломалась сборка под Android при обновлении build-tools до 31й версии { #built-tools-31 }
Симптомы:

```
Build-tool 31.0.0 is missing DX at /home/isandbox/android-sdk-linux/build-tools/31.0.0/dx
```
Причина: В версии build-tools 31.0.0 больше не поставляется утилита dx.
Некоторые third-party библиотеки (dexcount-gradle-plugin, android-gradle-aspectj) используют dx и пока не поддержали отказ от нее.

Починить можно пересобрав уже существующий ресурс с build-tools-31. [Как это сделать](https://st.yandex-team.ru/MOBDEVTOOLS-409#610ac17ec128d11015b00a7f)

Уже запатченные версии:
- ```platforms(31)+tools(31.0.0)+dx```
- ```sdk_31+tools_31.0.0+ndk_21.1.6352462+packages:cmake;3.10.2.4988404,dx```

### xcodebuild: error: Could not resolve package dependencies { #xcodebuild_error_resolve_package_dependencies }
Встречается при использовании swift package manager для резолва зависимостей с клонированием репозиториев по ssh@
Например, из bb.yandex-team.ru.
Симптом:
```shell script
xcodebuild: error: Could not resolve package dependencies:
The server SSH fingerprint failed to verify.
```

Чинится добавлением в рецепт сборки
```shell script
defaults write com.apple.dt.Xcode IDEPackageSupportUseBuiltinSCM YES
```

### Хочу хранить в разных репозиториях основной проект и конфиги для Teamcity Sandbox Runner-а. Как быть? { #different_vcs_for_project_and_tsr_configs }
Teamcity Sandbox Runner при выполнении задачи делает checkout репозитория, для того чтобы прочесть конфиг таска. Для проектов не использующих Arc (читай "делающих честный checkout с материализацией исходников") это может быть накладно в случае больших по размеру проектов, особенно если для выполнения таска вся кодовая база проекта не нужна.

Задача:
- Триггерить сборку в teamcity (и видеть изменения в проекте) по коммитам в проект.
- Сэкономить ресурсы за счет неполного чекаута

Решением является хранение конфигов для Teamcity Sandbox Runner-а в отдельном репозитории.

Как сделать:

 1. В настройках проекта Teamcity в разделе Parameters добавляем переменные указывающие на репозиторий с конфигом задачи:
    ```
    custom_config_repo_url
    custom_config_branch
    custom_config_commit="empty"
    ```
    {% cut "Как найти Parameters" %}

    ![Image](https://jing.yandex-team.ru/files/r2d2/photo_2021-09-09%2012.36.12.jpeg)

    {% endcut %}

    Эти параметры во время выполнения TSR-а переопределят "проектные" значения и TSR зачекаутит репозиторий с конфигом.

    ```custom_config_commit="empty"``` нужен для того чтобы TSR не попытался вытянуть коммит "проекта" из репозитория с конфигом.

 2. Чекаут своего проекта необходимо сделать самостоятельно, в скриптах вызываемых на этапе ```cmd```


{% note info %}

Изменения в ```custom_config_repo_url``` не отслеживаются Teamcity и не послужат основанием для запуска сборки.

{% endnote %}

### Как запустить задачу на определенном хосте { #repeat_on_specific_host }
Иногда (при отладке связки TSR/Sandbox) требуется выполнить сборку строго на определенном хосте.
Для этого можно при запуске задачи из Teamcity нужно добавить один из параметров, указав желаемый host
- ```sandbox.mac_agent```
- ```sandbox.linux_agent```

Учтите, что все линуковые stage-и запустятся на одном sandbox.linux_agent, все mac-овые - на одном sandbox.mac_agent. Т.е время прогона билда может оказаться большим

Формат задания хоста укороченный, так как это используется в sandbox-е: например ```mobile-mac039```

{% cut "Скрин запуска Teamcity с выполнением на mobile-mac039" %}

![Image](https://jing.yandex-team.ru/files/r2d2/Screenshot%202022-05-13%20at%2012.29.22.png)

{% endcut %}
