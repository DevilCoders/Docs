# Конфигурация Merge Queue

* `requiredChecksBranchName` — имя ветки, обязательные статусы которой будут являться обязательными проверками (настраивается в репозитории проекта на **GitHub**).

  :warning: Эта настройка может быть использована только в репозиториях _организаций_, у робота на репозиторий должны быть права уровня **Admin**. В репозиториях отдельных пользователей нет возможности дать коллабораторам доступ к Protected Branch API.

* `requiredChecks` — Список обязательных статусов на **GitHub**. В списке указываем контексты обязательных статусов. Если свойство указано, то оно переопределит статусы полученные из настроек **GitHub**.
     Например:

     ```json
     [
        "Gemini (desktop)",
        "Gemini (touch-pad)",
        "Gemini (touch-phone)"
     ]
     ```

    ![github-statuses](../assets/github-statuses.png)

* `startrekQueue` — Список необходимых статусов задач из Трекера для проверки перед вливанием. Проверки пропускаются если `startrekQueue` пуст.

     :warning: Роботу понадобится доступ для работы с очередью в Трекера. См. раздел про доступы.

     Можно указать один или несколько объектов в формате:

     ```json
     {
         "name": "Название очереди",
         "mergeStatuses": ["Список статусов для проверки"],
         "enqueueStatus": "Статус в который нужно перевести тикет",
         "enableIssueTransition": true
     }
     ```

     :warning: Это поле не должно быть пустым. Если вам не нужны проверки статусов в задачах Трекера — удалите поле.

     Например, для того чтобы проверить, что задачи указанные в заголовке пулл-реквеста из очереди `QUEUE` находятся в статусах `status1` или в `status2`, необходимо добавить в конфиг:

     ```json
     [
        {
            "name": "QUEUE",
            "mergeStatuses": ["status1", "status2"]
        }
     ]
     ```

     По умолчанию включен перевод тикета в статус `readyForDev`, можно определить другой статус:

     ```json
     [
        {
            "name": "QUEUE",
            "enqueueStatus": "close"
        }
     ]
     ```

     Или вовсе выключить перевод тикета по команде `/merge`:

     ```json
     [
        {
            "name": "QUEUE",
            "enableIssueTransition": false
        }
     ]
     ```

* `mergeQueueTask` — Параметры для запуска MQ таски в Sandbox.

* `projectTask` — Параметры для запуска проектной таски в Sandbox CI.

* `sandboxBaseUrl` — Url адрес Sandbox, которому будут адресованы запросы. Допускается указание порта путём добавления суффикса `:<port>`.

* `onlyFromForks` — Проверять, что пулл-реквест отправлен из форка. По умолчанию `false`.

* `fastFail` — Сервис, не дожидаясь прохождения mq-билда целиком, удалит PR из очереди при падении первой проверки в билде. Работает только для trendbox-ci. По умолчанию `false`.
![Fast fail](../assets/mq-fast-fail.png)

* `syncCommitRetries` — Количество попыток для проверки, что коммит из форка синхронизировался с базовым репозиторием.

* `poll` — Настройки ожидания обязательных проверок.

    Опция включает режим ожидания GitHub-статусов для обязательных проверок. Данный режим подходит для работы с любым CI.

    Для Sandbox CI рекомендуется использовать опцию `projectTask`, вместо `poll`. Это позволяет запускать обязательные проверки заранее (сразу после постановки в очередь), что ускоряет влитие пулл-реквеста при наличии очередей. Для trendbox_ci рекомендуется выставить значение `project_build` в опции `checkRunMode`.

    ```json5
    {
        // Ожидаем прокраски обязательных проверок в течение 15 минут (30 попыток через каждые 30 секунд)
        "poll": {
            "maxRetries": 30,     // количество попыток для проверки GitHub-статусов
            "attemptDelay": 30000 // интервал между попытками в ms
        }
    }
    ```

    Выбирайте общее время ожидания так, чтобы ваши проверки гарантированно укладывались во время ожидания. Иначе MQ-задачи могут завершаться с ошибкой таймаута.

    Выбирайте интервал между попытками так, чтобы, с одной стороны, не замедлять работу MQ-задачи, а с другой стороны не создавать лишнюю нагрузку на GitHub. Рекомендуемое значение — 30 секунд.

:warning: По умолчанию настройка выключена.

* `afterMerge` — Объект, который содержит в себе инструкции, выполняемые после вливания пулл-реквеста.

    * `commands` — массив команд, которые будут выполнены после вливания пулл-реквеста. В окружении выполняемых команд доступны `node.js` и `git` (версии совпадают с текущими версиями в конвейере). Также в окружении команд доступны переменные среды окружения `PR_NUMBER` с номером пулл-реквеста и `REPO` — с репозиторием. При балковом вливании скрипты запускаются для каждого вливаемого пулл-реквеста. Если необходимо запустить скрипт всего один раз (после первого вливаемого пулл-реквеста), нужно указать опцию `"shouldRunOnce": true`.

    ```json5
    {
        //
        "afterMerge": {
            "commands": [
                {
                    "name": "get-pr-number-and-repo",
                    "value": "echo $PR_NUMBER $REPO"
                },
                {
                    "name": "git-status",
                    "value": "git status",
                    "shouldRunOnce": true
                }
            ]
        }
    }
    ```

    * `secrets` — массив с перечислением имён секретов, которые будут прокинуты в `process.env` в трендбоксовой джобе. При этом, если имя секрета начиналось с  `env.` , то он будет доступен в переменных окружения без этого префикса.

    ```json5
    {
        //
        "afterMerge": {
            "commands": [
                // ...
            ],
            "secrets": [
                "env.my_secret_omg", // Будет доступен как process.env.my_secret_omg
                "my_other_secret"    // Будет доступен как process.env.my_other_secret
            ]
        }
    }
    ```

* <a name="before-merge"></a> `beforeMerge` — Объект, содержащий инструкции, выполняемые после ожидания очереди и завершения всех проверок, но непосредственно перед влитием пулл-реквеста.

    * ⚠️ Использование доступно ограниченному списку проектов, который определяется командой разработки Merge Queue в переменной окружения [`ALLOW_BEFORE_MERGE`][ALLOW_BEFORE_MERGE].
    * `command` — команда, которая будет выполнена перед влитием пулл-реквеста.
    * В окружении доступен Node.js (версии совпадают с текущими версиями в конвейере).
    * Секреты должны быть определены в [Sandbox Vault][sandbox-vault] с префиксом `env.` и доступны для владельца таски (`mergeQueueTask.owner`).
    * Команды выполняются в рабочей копии Аркадии в ветке пулл-реквеста.
    * Если команда так или иначе изменяет ветку, или добавляет коммиты, то для пуша нужно дополнительно включить настройку `needsUserOauthToken`.

    ```json5
    {
        "beforeMerge": {
            "command": "arc status"
        }
    }
    ```

* `needsUserOauthToken` — при `true` для постановки в очередь Merge Queue будет просить автора выдать разрешение на чтение и запись в Arc VCS от имени автора. По умолчанию изменение пользовательских веток в Arc (префикс `users/`) разрешено только их владельцу.

    * Используется вместе с настройкой `beforeMerge` для добавления в ветку коммитов с каким-либо сгенерированным кодом.
    * Разрешение выдаётся единожды, зашифрованный токен сохраняется в базе данных.
    * Отозвать разрешение можно в любой момент [в Паспорте][revoke-access].
    * Идентификатор приложения: `8e7828fea36b422187be31fb078ee3d5`.

* `strict` — если `false`, после успешного прохождения проверок пулл-реквеста, MQ выполнит ребейз пулл-реквеста от основной ветки репозитория, но не будет дожидаться проверок для обновлённого состояния, а вольёт пулл-реквест сразу.

* `checksRunMode` — режим, в котором будут запущены проверки.
    * `project_build` — в этом режиме перед вливанием будет запущен билд в ci системе и при успешном его завершении пулл-реквест будет влит. Является альтернативой для опции `poll` и работает только с `trendbox_ci`.
    Номер билда можно узнать из сервиса [MQS]:
    ![MQS link](../assets/mqs-link.png)
    На данную страницу есть прямая ссылка из пулл-реквеста:
    ![PR link](../assets/pr-link.png)
    Пример базовой конфигурации:
    `merge-queue.json`:
    ```json
    {
        "trendboxBaseUrl": "https://latest-trendbox-ci.si.yandex-team.ru/api/v1",
        "checksRunMode": "project_build",
        "requiredChecksBranchName": "master",
        "mergeQueueTask": {
            "type": "SANDBOX_CI_MERGE_QUEUE",
            "owner": "<MY_OWNER>"
        }
    }
    ```
    `.trendbox.yml`:
    ```yml
    jobs:
      my-job:
        ...

    workflows:
    ...
    mq:
      jobs:
        - my-job

    triggers:
    ...
    - trigger: merge_queue
      workflows: mq
      filters:
      events:
        only: queued
    ```
    * `project_build_forward` — в данном режиме проверки будут запускаться заранее, во время постановки пулл-реквеста в очередь, с учетом уже имеющихся в очереди пулл-реквестов. Если очередность вливания перед данным пулл-реквестом будет полностью соблюдена, он будет влит сразу же, без дополнительного запуска проверок. Работает только для trendbox-ci. Является аналогом кэшей для sandbox-ci.

* `bulkMode` — Оптимизация, при включении которой MQ вливает сразу несколько пулл-реквестов за одну итерацию.
    * `max_green` — за одну итерацию MQ вольет N пулл-реквестов, для которых успешно завершились запущенные наперед билды. На данный момент работает вместе с режимом `checksRunMode: project_build_forward`

* `forceMerge` — MQ разрешает влить пулл-реквест, даже если одна из проверок красная. Данный режим работает только для trendbox-ci.
![force merge](../assets/force-merge.png)
Список проверок, которым разрешено упасть, задается в конфиге. В качестве ключей проверок следует задать ключи из конфигурации в `.trendbox.yml`:

    `.trendbox.yml`:
    ```yml
    jobs:
      my-job:
        ...

    workflows:
    ...
    mq:
      jobs:
        - my-job
    ```
    `merge-queue.json`:
    ```json
    {
        "forceMerge": {
            "enabled": true,
            "allowedToFail": ["my-job"]
        }
    }

[MQS]: ../guides/ui.md
[ALLOW_BEFORE_MERGE]: https://deploy.yandex-team.ru/stages/merge-queue/config/du-merge-queue/box-merge-queue/wl-merge-queue
[robot-merge-queue]: https://staff.yandex-team.ru/robot-merge-queue
[sandbox-vault]: https://sandbox.yandex-team.ru/admin/vault
[revoke-access]: https://passport.yandex-team.ru/profile/access
