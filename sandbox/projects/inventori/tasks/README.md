# Inventori задачи на платформе Sandbox
1. RunInventoriTasks

    Ранер RunInventoriTasks - запускает "продуктовый" бинарь (код с продуктовой логикой, параметр Task executable (<task_name>_executable)).

    Поддерживает разные виды запуска на кластерах (simple/async/replication)

    Подробное описание параметров – ниже, а также [смотреть в readme RunInventoriTasks](RunInventoriTasks/README.md)
2. RunInventoriYqlTask

    Этот раннер запускает YQL, запрос нужно вставить в UI задачи. Также поддерживаются 3 вида запуск simple/replication/async

     Подробное описание парамеров – ниже, а также [смотреть в readme RunInventoriYqlTask](RunInventoriYqlTask/README.md)
3. BuildInventoriTasks

    Cобирает "продуктовый" бинарь. После этого (ресурс вручную меняется в ui конкретного шедулера)

    Подробнее [смотреть в readme BuildInventoriTasks](BuildInventoriTasks/README.md)
4. Также есть общая Sandbox таска DEPLOY_BINARY_TASK

   Эта таска используется для апдейта фундаментальных задач RunInventoriTasks/RunInventoriYqlTask (хотя обычно мы собираем их в CLI на своих dev QYP машинке).

   Важные параметры:
   - Path to target task relative to Arcadia root (target): sandbox/projects/inventori/tasks/RunInventoriTasks/bin/run-inventori-task
   - Binary task archive attributes(attrs): task_type: RUN_INVENTORI_TASKS
       тип таски, по нему RUN_INVENTORI_TASKS будет искать и использовать свежий релиз (если Release type of binary executor resource(binary_executor_release_type) выставлен в testing)
   - Check these task types are present in result program(check_types): RUN_INVENTORI_TASKS
       проверка что в бинаре есть ресурс такого типа
   - Yav secret with OAuth token for Arc (arc_oauth_token): sec-01eb89vakhn60j7ynwmr16a9ne#arc_token
       токен для доступа к коду через arc
   - Arcadia URL (arcadia_url): arcadia-arc:/#trunk
       указание откуда брать коммит для сборки в версии для arc
       После сборки ресурс можно использовать в тасках RUN_INVENTORI_TASKS с параметром

## За что отвечают параметры задач Inventori в UI Sandbox
(Речь про RunInventoriTasks\RunInventoriYqlTask)

## Базовый интерфейс одинаковый в RunInventoriYqlTask и RunInventoriTasks:
![](img/simple.png)

Cсылка на задачу со скриншота: https://sandbox.yandex-team.ru/task/1209809962/view

1. Release type of binary executor resource. Выбор из 7 параметр. Мы в инвентори затрагиваем лишь 4 из них
   - **custom**

     Это значение показывает что будет запускать именно тот бинарь, который указан в _Advanced_. *! Обязательно нужно указать ресурс*
   - none

     В этом случае версия береться из транка. Обновился транк -> поменяется ваш шедулер. Не рекомендуется использовать в шедулерах
   - stable

     Береться версия которая была предварительно зарелижена. [Вот](https://sandbox.yandex-team.ru/task/1182456403/view) пример таски которая зарелизила ресурс в stable, после чего он стал подставляться во все шедулеры
   - testing

   Аналогично предыдущему. Только релиз делается в testing

   В коде эта логика выглядит так: https://a.yandex-team.ru/arc_vcs/sandbox/projects/common/binary_task/__init__.py?rev=r9018843#L36

2. Environment type и Task name
    Эти параметры отвечают за то куда будут писаться метрики в Соломоне.
    - environment_type -> cluster
    - yt_cluster -> выбранному кластеру в поле YT/YQL cluster
    - task_name -> task_name

    Конкретно этот разобранный пример будет писать метрики сюда: https://solomon.yandex-team.ru/?project=inventori&cluster=dev&service=scheduler&l.task_name=alekseyn_test_yql_task_final_simple&l.metric=status&graph=auto&l.yt_cluster=arnold
3. Using custom run_mode

    Переменная отвечающая за тип запсука вашей задачи. Есть 3 варианта
    - simple

      Запустит вашу задачу на конкретно одном выбранном в UI кластере
    - async

      Задача будет запущена на обоих кластерах. Метрики пишутся в оба кластера независимо(упало только на арнольде, на арнольде будет красная, на хане все будет ок). Сама родительская задача будет зеленая, чтобы не случилось с её подзадачами
    - replication

      Запуск в режиме репликации, то есть копировании таблицы-результата с одного кластера на другой. Метрики пушиться только в master(главный) кластер

  Тут View отличается в RunInventoriTasks/RunInventoriYqlTask, поэтому рассмотрим отдельно

## run_mode в RunInventoriTasks
Примеры по которым понятно что за поля
- replication: https://sandbox.yandex-team.ru/task/1209909229/view

    ![replication](img/inventori_replication.png)
- async: https://sandbox.yandex-team.ru/task/1209892790/view

     ![async](img/inventori_async.png)

## run_mode в RunInventoriYqlTask
- replication: https://sandbox.yandex-team.ru/scheduler/702214/view

    ![replication yql](img/yql_replication.png)
- async: https://sandbox.yandex-team.ru/scheduler/702212/view

     ![async](img/yql_async.png)


