# Configdepot
Описание работы депота и его компонентов.

## Общий алгоритм работы

@startuml
== Команда от конфигуратора ==
actor Manager
participant configshop
queue "Callback SQS"
queue "SQS to configdepot" as SQS
participant configdepot
database "MDB"

Manager -> configshop: execute
configshop -> SQS: execute: (config_id, env, component)
SQS -> configdepot

activate configdepot
configdepot -> MDB: Создать t_deploy или взять текущий в ожидании
configdepot -> MDB: Прикопать новую ревизию (config_id, env, component) в базе, выставить deploy_id
configdepot -> "Internal SQS": Задача на деплой
deactivate configdepot


== Выполнение конфигурации ==

"Internal SQS" -> configdepot: Взять задачу на деплой
MDB -> configdepot:
note left
  1. Выбираем последние ревизии конфигураций, относящиеся к деплою
  2. Массив конфигураций (config_id) передать в шаблонизатор конфига
  3. Отрендерить конфиг
end note

configdepot -> Sandbox: Upload отрендеренный конфиг
configdepot -> Sandbox: Get or create таск из конфига для компонента (например create_release или ya_exec)

activate configdepot
configdepot ->  "Internal SQS": Перепоставить задачу или завершить работу
destroy configdepot


== Обратная связь к конфигуратору ==
configdepot -> "Callback SQS"
"Callback SQS" -> configshop
configshop -> Manager
@enduml


Configdepot представляет собой web-сервис, который общается с Конфигуратором посредством SQS очередей.
Configdepot умеет работать с задачами вида **configuration_task** и **deploy_selection_task**.
После получения задачи от Конфигуратора, Депот валидирует запрос и кладет задачу во внутреннюю SQS очередь.

{% note info %}

### Task delay
Так как конфигурация влечет за собой запуск Sandbox таски и зачастую работу с релизами в Deploy, чтобы сократить количество случаев, когда сразу после завершения одной конфигурации запускается сразу же следующая,
мы ожидаем какой-то промежуток времени для получения дополнительных задач.
Данное поведение может измениться в будущем, на данный момент время ожидания состовляет 5 минут.

{% endnote %}

Когда задача из внутренней очереди попадает в обработчик, обработчик проверяет статус конфигурации и запускает процессор компонентов, который
сначала агрегирует указанным методом пользовательские конфигурации, а потом запускает экшн, исполняющий конфигурацию.

После чего, задача опять становится во внутреннюю очередь и при получении этого задания в следующий раз,
обработчик проверяет статус экшена.

В конце работы экшена (в случае успеха или неуспеха) депот отвечает в callback очередь конфигшопа.

### Агрегация конфигураций
TODO(@kraysent): расписать про configuration_key и взаимодействие со state и про хитрый SELECT из базы.


## Таски

### Configuration task
TODO(@kraysent): расписать про configuration_task

### Deploy selection task
TODO(@kraysent): расписать про deploy_selection_task

## Процессор компонентов
Процессор компонентов занимается подготовкой конфигураций для активного экшена и управлением экшеном.

Работа процессора компонентов делится на 2 части.
- Подготовить конфигурации клиентов в соответствии с указанным методом
- Запустить экшен с этими конфигурациями и отслеживать его работу

### Методы агрегации конфигураций
Перед тем как запустить экшн необходимо объединить все конфигурации в соответствии с неким правилом.
Для этого применяются методы агрегации.

#### Raw
Метод агрегации сохраняющий конфигурации сервисов в виде массива.

#|
|| Параметр метода | Описание | Поля | Пример ||
|| target
|
ключ в параметрах экшена, <br/> куда положить полученный массив конфигураций
|
- dst: string -- путь до ключа, через точку.
| `"target": {"dst": "task_input.parameter"}`
В данном случае массив неизмененных конфигураций попадет в `"task_input": {"parameter": <here>, "other_param": "foo"}` ||
|#


TODO(@bremk): заинклюдить реальный пример, когда появятся реальные компоненты в conponents.yaml

#### Render
Метод агрегации, отрендиривающий конфигурации в соответствии с указанным шаблоном и сохраняющим их в параметры экшена.

#|
|| Параметр метода | Описание | Поля | Пример ||
|| target
|
ключ в параметрах экшена, <br/> куда положить полученный массив конфигураций
|
- dst: string -- путь до ключа, через точку.
|
`"target": {"dst": "task_input.parameter"}` <br/> В данном случае массив неизмененных конфигураций попадет в `"task_input": {"parameter": <here>, "other_param": "foo"}` ||
|| template
|
  параметры шаблона для рендеринга
|
- path: string -- путь до шаблона
- explicit: string -- шаблон сохраненный в виде строки

{% note warning %}

Необходимо, чтобы был заполнен или `path` или `explicit`, приоритет для `path`

{% endnote %}

- serialize_type: string[RAW, YAML, JSON] -- необходимо ли сериализовать массив конфигураций. Сериализованные конфигурации нельзя использовать в сложных шаблонах, можно только подставлять всю сериализованную строку.
|
```json
"template": {
  "path": "./configs/test/templates/processor.yaml.tpl"
  "serialization_type": "YAML"
}
```
||
|#


Сам рендеринг осуществляется с помощью библиотеки [templates](https://pkg.go.dev/text/template) для Go, что позволяет
гибко конфигурировать компоненты.

После сериализации конфигурации доступны в шаблоне по ключу `.configurations`.
Если указан тип сериализации RAW, то конфигурации попадут в шаблон как `[]map[string]any` и их можно использовать в сложных шаблонах.

Пример:
В реальном шаблоне переменные описываются в двойных скобках, но YMF сам умеет в шаблоны и пытается это отрендерить, поэтому
в примерах шаблонов будут одинарные скобки.

```gotemplate
users:
{ range .configurations }
  - username: { .name }
    personal_data: { .data }
{end}
```
<small> example.yaml.tpl </small>

```go
configurations := []map[string]any{
	{
		"name": "Tigran",
		"data": map[string]any{
			"interests": []string{"foo", "bar"},
        }
    },
	{
		"name": "Ivan",
		"data": map[string]any{
			"favourite_movie": "Roki"
        },
    }
}
```
<small> configurations </small>


```yaml
users:
    - username: Tigran
      personal_data:
        interests: [foo, bar]
    - username: Ivan
      personal_data:
        favourite_movie: "Roki"
```
<small> result </small>


При использовании типов сериализации YAML/JSON массив конфигураций будет сериализован в строку и его можно будет вставить только как строку.
Это полезно, когда нужно в YAML/JSON шаблон подставить массив конфигураций без шаблонизирования.
Пример:
```gotemplate
users:
{ .configurations }

foo:
    bar: test
```
<small> example.yaml.tpl </small>

```go
configurations := []map[string]any{
	{
		"name": "Tigran",
		"data": map[string]any{
			"interests": []string{"foo", "bar"},
        }
    },
	{
		"name": "Ivan",
		"data": map[string]any{
			"favourite_film": "Roki"
        },
    }
}
```
<small> configurations </small>

```yaml
users:
    - name: Tigran
      data:
        interests: [foo, bar]
    - name: Ivan
      data:
        favourite_film: Roki
foo:
  bar: test
```
<small> result </small>

TODO(@bremk): заинклюдить реальный пример, когда появятся реальные компоненты в conponents.yaml


#### RenderAndUpload
Метод агрегации, который рендерит конфигурации в соответствии с указанным шаблоном аналогично Render, после чего загружает
полученный файл в Sandbox и сохраняет ID полученного ресурса в параметры экшена.

#|
|| Параметр метода | Описание | Поля | Пример ||
|| target
|
ключ в параметрах экшена, <br/> куда положить полученный массив конфигураций
|
- dst: string -- путь до ключа, через точку.
  |
  `"target": {"dst": "task_input.parameter"}` <br/> В данном случае массив неизмененных конфигураций попадет в `"task_input": {"parameter": <here>, "other_param": "foo"}` ||
  || template
  |
  параметры шаблона для рендеринга
  |
- path: string -- путь до шаблона
- explicit: string -- шаблон сохраненный в виде строки

{% note warning %}

Необходимо, чтобы был заполнен или `path` или `explicit`, приоритет для `path`

{% endnote %}

- serialize_type: string[RAW, YAML, JSON] -- необходимо ли сериализовать массив конфигураций. Сериализованные конфигурации нельзя использовать в сложных шаблонах, можно только подставлять всю сериализованную строку.
  |
```yaml
template:
  path: "./configs/test/templates/processor.yaml.tpl"
  serialization_type: "YAML"
```
||
|| resource_type
|
тип ресурса, который будет создан для хранения отрендереного файла
| |
`resource_type: OTHER_RESOURCE`
||
|| owner
|
владелец ресурса
| |
`owner: BILLING-CI`
||
|| resource_name
|
название файла сгенерированного файла, по умолчанию **resource**.

{% note alert %}

При скачивании ресурса через `ya download` ресурс в любом случае будет иметь название равное его ID, поэтому на название ресурса нельзя завязываться при разработке

{% endnote %}

| |
`resource_name: test_file.yaml`
||
|#

Перед рендерингом метод проверяет, что ресурса с указанным deploy_id уже нет в Sandbox и если ресурс уже существует, то
сразу сохраняет его ID в параметры экшена.

TODO(@bremk): заинклюдить реальный пример, когда появятся реальные компоненты в conponents.yaml


### Экшены компонентов
После агрегирования конфигураций запускается экшн, который выполняет произвольную конфигурацию.
Экшн предполагается как универсальный компонент, который не придется изменять при добавлении новых сервисов в зону ответственности депота.

На данный момент реализован экшн Sandbox, который позволяет запустить произвольную задачу в Sandbox.
Доступный набор задач в Sandbox позволяет конфигурировать большинство сервисов в Яндексе, но если их будет недостаточно,
то предполагается, что будет реализована новая задача в Sandbox, вместо добавления нового экшена в Configdepot.

В соответствии с алгоритом работы депота, экшен должен уметь проверять статус выполнения перед запуском и если для данного deploy_id уже выполняется экшн, то необходимо вернуть текущий статус выполения без запуска экшена 2 раз.

#### Статусы

Экшн возвращает текущий статус выполения. Статусы описываются следующими значениями

{% code '/billing/configdepot/pkg/core/actions/component_processor/root.go' lang='go' lines='[BEGIN processor statuses]-[END processor statuses]' %}

#### Sandbox
Экшн Sandbox запускает произвольную Sandbox задачу с указанными входными параметрами.

Экшн позволяет запускать как классические registry задачи, так и бинарные/tasklet задачи через taskbox, однако для этого
необходимо предварительно загрузить бинарные файлы задачи как SANDBOX_BINARY_TASK ресурс, добавить в его аттрибуты `task_type: <TASK_TYPE>` и запомнить ID ресурса.

Этот процесс аналогичен работе CI, где для tasklet и бинарных задач нужно явно указывать версии ресурсов в ci/registry.

Подробнее про различные виды задач можно прочитать в документации Sandbox про [задачи](https://docs.yandex-team.ru/sandbox/tasks) и про [бинарные задачи](https://docs.yandex-team.ru/sandbox/dev/binary-task)


#|
|| Параметр экшена | Описание | Пример ||
|| type |
тип SANDBOX таска. Может быть registry таска, может быть binary task.
Для запуска tasklet нужно пользоваться registry таской [TASKLET_EXECUTOR](https://sandbox.yandex-team.ru/tasks?children=true&hidden=false&type=TASKLET_EXECUTOR&created=14_days)

{% note warning %}

Если необходимо запускать не registry таску, параметр task_resource должен быть заполнен, иначе процессор не сможет создать таску

{% endnote %}
|
`type: BILLING_FAAS_BUILD_TASK` ||
|| task_resource |

ID ресурса с бинарными файлами, должен быть stable зарелизен и иметь аттрибут `task_type`

{% note warning %}

аттрибут `task_type` не проставляется сам при использовании `sb-upload`. См. [пояснение](https://st.yandex-team.ru/DEVTOOLSSUPPORT-20635#62ceea41d8119f724e444d9b)

{% endnote %}

| `task_resource: 123456789` ||
|| owner | владелец ресурса | `owner: BILLING-CI` ||
|| sandbox_tag |
дополнительный тег, который будет добавлен к таске в формате `CONFIGDEPOT:<sandbox_tag>`.
Sandbox автоматически делает все теги upper-cased
| `sandbox_tag: faas` ||
|| task_input |
входные параметры, которые будут переданы на вход в таску

{% note info %}

Для того чтобы понять какие входные параметры у таски можно или посмотреть на вкладку Context у завершившийся таски или посмотреть в код таски.

{% endnote %}
|
```yaml
task_input:
    client_tags: MULTISHOT
    live_time: 10
    suspend: false
```
|#
