# Описание протокола

```yaml
# [optional] включает указанные файлы
# файлы вставляются в начало этого файла в порядке перечисления 
# при вставке include_files и import_tasks не учитываются
# если путь начинается с '/', то он берется от корня арка, иначе от текущей директории
include_files:
  - relative/path/to/config.yaml
  - /absolute/path/from/arc/root/to/config.yaml
# [optional] считывает задачи из указанных в файлах, чтобы потом их можно было использовать в extends
# файл загружается в изолированном окружении и разрешаются все include_files и import_tasks, затем сохраняются только задачи 
import_tasks:
  - relative/path/to/config.yaml
  - /absolute/path/from/arc/root/to/config.yaml
# описание задач для запуска. Будут запущены все задачи перечисленные тут
tasks:
  # уникальный идентификатор задач. Он будет использоваться в extends
  task_id:
    # [optional] имя задачи, которое будет отображаться в sandbox. Если не задан, то используется task_id
    name: Task Name
    # тип sandbox задачи
    type: TASK_TYPE
    # [optional] идентификатор задачи, которую расширяет эта
    # тип у extends_task_id должен совпадать с типом этой задачи
    # будут скопированы блоки info, requirements, parameters
    extends: extends_task_id
    # системные параметры задачи (т.е. параметры которые не являются кастомными полями задачи)
    # указанные тут параметры будут переопределять параметры из extends_task_id. 
    # чтобы дополнить параметр нужно в конце его добавить '+'. Например, 'tags+:'. Верно только для массивов и мэпок
    # все параметры можно посмотреть тут https://a.yandex-team.ru/arc_vcs/sandbox/sdk2/task.py?rev=trunk#L224
    info:
      # [optional] от чей группы будет запускаться задача
      owner: OWNER
      # [optional] описание задачи
      description: Run ...
      # [optional] теги задачи
      tags: [ TAG1, TAG2 ]
      # [optional] приоритет задачи, смотри https://wiki.yandex-team.ru/sandbox/tasks/priorities/
      priority:
        class: SERVICE
        subclass: NORMAL
    # [optional] требования к задаче (нужно место, ядер, теги клиента)
    # указанные тут параметры будут переопределять параметры из extends_task_id. 
    # чтобы дополнить параметр нужно в конце его добавить '+'. Например, 'tags+:'. Верно только для массивов и мэпок
    # все параметры можно посмотреть тут https://a.yandex-team.ru/arc_vcs/sandbox/sdk2/task.py?rev=trunk#L168
    requirements:
      # [optional] теги клиента
      client_tags: MOBILE_MONOREPO & USER_MONOREPO & OSX_CATALINA
      # [optional] id ресурса с бинарной задачей
      tasks_resource: 1234
      # [optional] id ресурса с контейнером
      container_resource: 1234
      # [optional] хост на котором будет выполнена задача
      host: ymake-dev-mac05
    # [optional] параметры задачи, зависят от конкретной задачи
    # указанные тут параметры будут переопределять параметры из extends_task_id. 
    # чтобы дополнить параметр нужно в конце его добавить '+'. Например, 'tags+:'. Верно только для массивов и мэпок
    # тут приведен чисто пример параметров
    parameters:
      # переопределит параметр secret_gradle_parameters из extends_task_id
      secret_gradle_parameters:
        yav.oauth.token: sec-...[yav.token]
      # дополнит параметр gradle_parameters из extends_task_id
      gradle_parameters+:
        buildType: source
      # если '*' стоит в начале, то надо брать всю строку в кавычки. Иначе оно будет пробовать подставить сюда алиас
      tests_pattern: '*ActivateTest.testActivate*'
```
