# Взаимодействие с Alemate

## Доступ к API {#api-access}

* Система предоставляет ReST API по протоколу HTTP(s).
* Базовый URL: `http(s)://nanny.yandex-team.ru/`.
* Тело запроса (POST, PUT) — всегда json.
* Тело ответа — всегда json.

### Аутентификация {#api-authentication}

* Для аутентификации всех ресурсов API используется внутренний сервис **Паспорт**.
* Аутентификация может быть проведена через Cookie `Session_id` — так работает UI сервиса при запросах из браузера.
* Для программного доступа (роботы, скрипты, другие сервисы) может быть использован механизм **Oauth**:
* Необходимо получить OAuth токен, например, на странице [https://nanny.yandex-team.ru/ui/#/oauth](https://nanny.yandex-team.ru/ui/#/oauth). Если необходимо токен для робота, необходимо в браузере иметь Session_id куку робота, т.е. залогиниться роботным пользователем.
* Для каждого запроса в HTTP заголовки необходимо добавить заголовок `Authorization: OAuth {access_token}`.


### Авторизация {#api-authorization}

* Любой аутентифицированный пользоваль имеет право на чтение всего API. Под чтением подразумеваются HTTP GET- и HEAD-запросы.
* API разделен на «модули»: `api.auth`, `api.alemate.recipes`, `api.alemate.task_groups`, и так далее. Модуль представляет собой набор доступных для взаимодействия ресурсов.
* Пользователь может совершать модифицирующие HTTP-запросы к ресурсам модуля, если он имеет права на этот модуль или на любой из его надмодулей.
    Так, например, право на модуль `api` даёт доступ ко всем подмодулям. Право на модуль `api.alemate` даёт доступ ко всем подмодулям `api.alemate.*`.
* Управлять правами можно через UI: [http://nanny.yandex-team.ru/ui/#/auth/](http://nanny.yandex-team.ru/ui/#/auth/)
    Права можно давать как отдельному пользователю, так и группе со Стаффа.
* Если вам не хватает прав для необходимой операции, напишите на рассылку [nanny@yandex-team.ru](nanny@yandex-team.ru)

## Ресурсы API {#api-resources}

### Применить YAML-рецепт {#apply-yaml-recipe}

* URL: `/v1/alemate/yaml_recipes/<recipe>/apply/`
* Метод: POST
* Пример:

```python
import json
import requests
> requests.post(
    "http://nanny.yandex-team.ru/v1/alemate/yaml_recipes/deploy_nanny.yaml/apply/",
    data=json.dumps({
        "parameters":
        		{
        			'base_configuration': 'SG', 
        			'new_configuration': 'prestable_nanny-1398151513'
        		}
    }),
    headers={
        'accept':'application/json',
        'content-type': 'application/json',
        'authorization': 'OAuth bba98da4aa924544ace2530511d3175b'
    }
    ).text
< {"id": "search-0000011063"}
```

Или с передачей текста рецепта:
* URL: `/v1/alemate/yaml_recipes/apply/`
* Метод: POST
* Пример:

```python
import json
import requests
> requests.post(
    "http://nanny.yandex-team.ru/v1/alemate/yaml_recipes/apply/",
    data=json.dumps({
        "content": """
description: It is my {{my_parameter}}

tasks:
    init:
        manual_confirm: False
        type: empty


    init2:
        manual_confirm: False
        type: empty
        dependencies:
          - init
"""
        "parameters":
        		{
        			'my_parameter': 'WAT', 
        		}
    }),
    headers={'accept':'application/json', 'content-type': 'application/json'}
    ).text
< {"id": "search-0000011063"}
```

### Провалидировать YAML-рецепт {#yaml-recipes-validate}

* URL: `/v1/alemate/yaml_recipes/validate/`
* Метод: POST
* Пример:

```python
import requests
import json
> requests.post("http://nanny.yandex-team.ru/v1/alemate/yaml_recipes/validate/",
                data=json.dumps({"content": "recipe-body-or-name", "parameters": {}}),
                headers={
                    'accept': 'application/json',
                    'content-type': 'application/json'}).json
< 200 OK {
  "is_valid": True
  "schema": {...}  // JSON-схема параметров рецепта
}
< 200 OK {
  "is_valid": False
  "errors": ["error1", "error2", ...]
}
```

### Информация о группе {#task-group-info}

* URL: `/v1/alemate/task_groups/<task_group>/info/`
* Метод: GET

### Информация о тасках группы {#task-group-children}

* URL: `/v1/alemate/task_groups/<task_group>/children/`
* Метод: GET

### Смена состояния таск группы {#task-group-status-modify}

* URL: `/v1/alemate/task_groups/<task_group>/status/`
* Метод: POST
* Пример:

```python
import requests
import json
> requests.post("http://nanny.yandex-team.ru/v1/alemate/task_groups/search-0000006892/status/",
                data=json.dumps({"status": "<STATUS>"}),
                headers={
                    'accept': 'application/json',
                    'content-type': 'application/json'}).text
< 200 OK {}
```
* Доступные статусы: 
    * **REJECTED** — таск группа отменена

### Статус группы {#task-group-status}

* URL: `/v1/alemate/task_groups/<task_group>/status/`
* Метод: GET

### Информация о задании (task) группы {#tasks}

* URL: `/v1/alemate/task_groups/<task_group>/tasks/<task>/info/`
* Метод: GET
* Пример: `/v1/alemate/task_groups/search-0000007305/tasks/job-0000000000/info/`

### Подтверждение задачи (confirm task) {#confirm-task}

* URL: `/v1/alemate/task_groups/<task_group>/tasks/<task>/commands/`
* Метод: POST
* Пример:

```python
import requests
import json
> requests.post("http://nanny.yandex-team.ru/v1/alemate/task_groups/search-0000006892/tasks/job-0000000001/commands/",
                data=json.dumps({"type": "confirm"}),
                headers={
                    'accept': 'application/json',
                    'content-type': 'application/json'}).text
< 200 OK {}
```

### Отмена задачи (cancel task) {#cancel-task}

* URL: `/v1/alemate/task_groups/<task_group>/tasks/<task>/commands/`
* Метод: POST
* Пример:

```python
import requests
import json
> requests.post("http://<hostname>:[port]/v1/alemate/task_groups/search-0000006892/tasks/job-0000000001/commands/",
                data=json.dumps({"type": "cancel"}),
                headers={
                    'accept': 'application/json',
                    'content-type': 'application/json'}).text
< 200 OK {}
```

### Изменение degrade_levels запущенной задачи {#degrade-levels-modify}

* URL: `/v1/alemate/task_groups/<task_group>/tasks/<task>/degrade_levels/`
* Метод PUT
* Пример:

```python
import requests
> requests.put("http://nanny.yandex-team.ru/v1/alemate/task_groups/search-0000006892/tasks/job-0000000001/degrade_levels/",
               json={
                   "degrade_levels": {"operating_degrade_level": 0.1, "stop_degrade_level": 0.1, "max_degrade_speed": 1},
                   "task_group_revision_id": "31a99c64893c901fbb82302bd76b27ddffd2a3aa" # get from API, method task/info
               },
               headers={'Authorization': 'OAuth XXX'}).text
< 200 OK {}
```
