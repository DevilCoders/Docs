# Service Repo API

## Intro {#intro}

Сервис предоставляет ReST API для управления сервисами и получения информации о них.

Базовый URL: `http://nanny.yandex-team.ru`

##  Аутентификация {#authz}

Все запросы (кроме нескольких исключений, см. ниже) к репозиторию сервисов должны быть аутентифицированы. Даже запросы на чтение. Аутентификация производится через внутренний Паспорт.

* Для запросов из браузера проверяется cookie `Session_id`.
* Для запросов роботами необходимо использовать OAuth токен, добавив его в заголовки запросов: `Authorization: OAuth <access_token>`
При этом так же будет использована паспортная авторизация.
Production и prestable инсталляции nanny требуют различные OAuth-токены для одного и того же пользователя.

Токены пользователя можно получить на страницах:
* [http://nanny.yandex-team.ru/ui/#/oauth/](http://nanny.yandex-team.ru/ui/#/oauth/) для nanny.yandex-team.ru
* [http://dev-nanny.yandex-team.ru/ui/#/oauth/](http://dev-nanny.yandex-team.ru/ui/#/oauth/) для dev-nanny.yandex-team.ru

Исключения:
* `GET /v2/services/<service_id>/_deploy_status/`
* `GET /v2/services/<service_id>/current_state/`
* `GET /v2/services/<service_id>/current_state/hosts/`
* `GET /v2/services/<service_id>/current_state/instances/`
* `GET /v2/services/<service_id>/target_state/`
* `GET /v2/services/<service_id>/runtime_attrs/<section_name>/`

Наличие исключений вызвано тем, что, к сожалению, многие клиенты, которые пользуются этими вызовами не умеют аутентифицироваться.

## Авторизация {#authorization}

В данный момент реализовано несколько ролей пользователей:
* **Owner** - назначает другие роли пользователям, может удалить сервис.
* **Сonfiguration manager** - изменяет атрибуты сервиса.
* **Operations manager** - управляет выкладкой сервиса.
* **Service observers** - прав не имеют, добавляются в копию тикетов на активацию снэпшотов сервиса.
Для удобства при создании сервиса из UI по-умолчанию автору сервиса присваиваются все роли.

## Формат ответа {#authorization-response}

Для корректной работы рекомендуется всегда указывать заголовок `Accept` со значением `application/json`. Ответы так же возвращаются в формате JSON с выставленным заголовком `Content-Type: application/json` .

## Формат запроса {#authorization-request}

Все запросы на изменения в своём теле должны передаваться в формате JSON и содержать заголовок `Content-Type` со значением `application/json`.

### Важное замечание {#authorization-alert-note}

{% note alert %}

Тело модифицирующих запросов, в частности для модификации info_attrs, runtime_attrs сервиса, (за исключением тех, где это указано явно) требует указания полного содержимого модифицируемого объекта, даже если требуется изменить лишь часть его атрибутов.

{% endnote %}

**Пример.** Для модификации лишь один из атрибутов `info_attrs`сервиса (например,`category`, необходимо передать в PUT-запросе в том числе все остальные атрибуты: `recipes`, `tickets_integration`, ...).

## Работа с атрибутами сервисов {#service-attributes}

Ввиду особенностей используемой базы данных, требований к версионировании изменений все объекты атрибутов имеют примерно одинаковый формат.
Каждый документ имеет:

* Идентификатор (`_id`) - строка, представляющая собой глобально уникальный идентификатор объекта.
* Информацию об изменении (`change_info`) - описание последнего изменения атрибута.
Обычно включает в себя автора, дату изменения, комментарий и так далее.
* Содержимое (`content`) - непосредственно документ, содержащий сам набор атрибутов.
Такой формат хранения позволяет изменять атрибуты методом Compare-And-Swap для избежания переписывания устаревшей версии, которую уже кто-то изменил. Поэтому мы требуем, чтобы **все** изменения атрибутов указывали `snapshot_id` - идентификатор объекта, который хотим изменить. Т.к. в запросе мы не указываем автора изменений (логин автора извлекается из OAuth токена или Cookie), то приходим к следующему формату запросов на изменения какого-либо набора атрибутов:

```json
{
  "comment": "Add new config file",
  "snapshot_id": "54b9123569faf370f651424b",
  "content": {}  
}
```
* `comment` — описание изменений;
* `snapshot_id` — идентификатор ревизии атрибутов, которую мы хотим изменить;
* `content` — новое содержимое атрибутов (различное для каждого типа атрибутов).

##  Описание сервиса {#service-desc}

Описание сервиса представляет собой структуру с идентификатором, целевым и текущим состояниями и несколькими секциями описательных атрибутов, которые независимо версионируются.

* Шаблон: `GET /v2/services/<_id>/`
    * `_id` - идентификатор сервиса.   
* Пример: `GET /v2/services/production_nanny/`

Формат ответа:

```json
{
    "_id": "prestable_sleep",
    "current_state": {...},
    "target_state": {...},
    "info_attrs": {...},
    "runtime_attrs": {...},
    "auth_attrs": {...}
}

```
    * **_id** - идентификатор сервиса
    * **target_state** - описание целевого состояния сервиса
    * **current_state** - описание текущего состояния сервиса
    * **info_attrs** - слепок (snapshot) информационных атрибутов сервиса
    * **runtime_attrs** - слепок (snapshot) runtime атрибутов сервиса
    * **auth_attrs** - слепок (snapshot) авторизационных атрибутов сервиса
* Ошибки
    * **404 Not Found** - если сервиса с указанным _id не существует.

## Создание сервиса {#service-create}

Для создания сервиса необходимо 
* сформировать документ, описывающий сервис
* отправить HTTP **POST** запрос `/v2/services/` с сформированным документом в теле запроса
В ответе вернётся полное описание сервиса с кодом `201 CREATED`.

### Формат запроса {#service-create-request}

```json
  "id": "<уникальный идентификатор сервиса>",*
  "comment": "<текстовое описание первого коммита>",
  "info_attrs": {}  # документ с информационными атрибутами,*
  "auth_attrs": {}  # документ с авторизационными атрибутами,
  "runtime_attrs": {}  # документ с runtime атрибутами
```

* Звёздочкой отмечены обязательные поля. Формат атрибутов описан ниже в соотвествующих разделах.
* Если в `auth_attrs` не будет указан владелец (не заполнен атрибут _owner_), то в качестве владельца будет назначен пользователь, совершающий запрос. В противном случае сервис может стать недоступен для управления.

### Целевое состояние {#service-create-target-state}

Описывает целевое состояние сервиса:

```json
{
  "_id": "54b7d18a53ba1f0006ad801a",
  "info": {
    "ctime": 1421332874306,
    "author": "romanovich",
    "comment": "just testing"
  },
  "content": {
    "is_enabled": true,
    "snapshot_id": "54b7bf36494013000648801c",
    "recipe": "common",
    "recipe_parameters": []
  }
}

```
#### Получение {#get-target-state}

* Шаблон: `/v2/services/<_id>/target_state/`
* Пример: `/v2/services/production_balancer_msk/target_state/`

#### Изменение требуемого активного {#changing-active}

Изменение целевого состояния не может быть произведено транзакционно (по объективным причинам), поэтому механизм изменения целевого состояния - это создание события о намерении пользователя, которое будет сохранено и асинхронно обработано системой.
* Метод: `POST`
* Шаблон: `/v2/services/<_id>/events/`

Пример:

```json
{
  "type": "SET_TARGET_STATE",
  "content": {
    "is_enabled": true,
    "snapshot_id": "54b9123569faf370f651424b",
    "comment": "Friendship is magic",
    "prepare_recipe": "default",
    "recipe": "common"
  }
}

```

Для отключения сервиса необходимо так же отправить событие типа `SET_TARGET_STATE`, но при этом выставить поле `is_enabled: false`. 

Пример:

```json
{
    "type": "SET_TARGET_STATE",
    "content": {
        "is_enabled": false,
        "comment": "Enough for today."
    }
}

```

#### Откат на предыдущий активный снэпшот {#rollback-previous-snapshot}

При изменении целевых состояний, система запоминает снэпшот, который был активен последний раз. Таким образом у нас появляется возможно откатить изменения.
* Метод: `POST`
* Шаблон: `/v2/services/<_id>/events/`

Пример:
```json
{
    "type": "ROLLBACK",
    "content": {
        "comment": "Do a barrel roll",
        "recipe": "common",
        "ticket_id": "NANNY-1234234",
        "set_as_current": (True|False)
    }
}
```

Где:
* `comment` - комментарий к событию.
* `recipe` - название рецепта сервиса, которым необходимо выполнить активацию предыдущего снэпшота.
* `ticket_id` - идентификатор тикета, в котором нужно отмечать прогресс отката.
* `set_as_current` - установить откатываемую ревизию в качестве текущей (передвинуть `HEAD`).


#### Изменение состояния снэпшота {#changing-snapshot-state}

Предыдущей метод позволял изменить только активное состояние. Событие `SET_SNAPSHOT_STATE` позволяет указывать любое состояние для любого имеющегося у сервиса снэпшота, **кроме** отключения сервиса.
* Метод: `POST`
* Шаблон: `/v2/services/<service_id>/events/`

Пример:

```json
{
	"type": "SET_SNAPSHOT_STATE",
	"content": {
		"snapshot_id": "54b9123569faf370f651424b",
		"comment": "Deploy new version",
		"recipe": "COMMON_DEPLOY",  # Обязательно только для активации.
                "prepare_recipe": "default",  # Обязателен, если в рецепте активации нет PREPARE-задач
                "state": "ACTIVE|PREPARED|CREATED|DESTROYED",
                "set_as_current": (True|False),
                "labels": [
                    {
                        "key": "deploy_type",
                        "value": "realtime"
                    }
                ]
	}
}
```

Где:
* `snapshot_id` - идентификатор ревизии (снэпшота).
* `comment` - комментарий к действию.
* `recipe` - рецепт для выкладки (активации).
* `prepare_recipe` - рецепт для подготовки (PREPARE стадия).
* `state` - целевое состояние ревизии, которое необходимо выставить.
* `set_as_current` - установить откатываемую ревизию в качестве текущей (передвинуть `HEAD`).
* `labels` - набор пар ключ-значение, которые будут выставлены у запущенных таскгрупп в alemate. Может использоваться для фильтрации таскгрупп на [панелях alemate](../alemate/task_panels.md).

#### Установка/снятие паузы {#pause}

Сервис можно поставить "на паузу", т.е. все действия для приведения сервиса в целевое состояние будут остановлены. Текущие процессы (выкладки) отменены не будут.
* Для постановки "на паузу" необходимо отправить событие `PAUSE_ACTIONS`.
* Для отмены "паузы" необходимо отправить событие `RESUME_ACTIONS`.
* Пользователь **должен иметь права** "Operations Manager"
* Метод: `POST`
* Шаблон: `/v2/services/<service_id>/events/`

Пример установки: 

```json
{
    "type": "PAUSE_ACTIONS",
    "content": {
        "comment": "Stop actions, running tests."
    }
}

```
  * Пример снятия с "паузы": 
      ```json
      {
          "type": "RESUME_ACTIONS",
          "content": {
              "comment": "Please go on."
          }
      }
      ```

### Текущее состояние {#current-state}

Описывает текущее состояние сервиса.

```json
{
  "_id": "54b7d1e753ba1f0006ad802b",
  "entered": 1421332967830,
  "content": {
    "is_paused": {
      "info": {
        "comment": "Initial commit", 
        "ctime": 1419333455986, 
        "author": "nekto0n"
      }, 
      "value": false
    }, 
    "active_snapshots": [
      {
        "taskgroup_id": "search-0000001123", 
        "state": "ACTIVE", 
        "entered": 1421332937630, 
        "conf_id": "prestable_sleep-1421328182941", 
        "snapshot_id": "54b7bf36494013000648801c"
      }
    ], 
    "summary": {
      "entered": 1421332967829, 
      "value": "ONLINE"
    }
  }
}
```

#### Получение {#get-current-state}

* Шаблон:  `/v2/services/<_id>/current_state/`
* Пример:  `/v2/services/production_balancer_msk/current_state/`

Пример ответа:

```json
{
  "_id": "54b908b069faf339952f7d87",
  "entered": 1421412528204,
  "content": {
    "is_paused": {
      "info": {
        "comment": "Initial commit", 
        "ctime": 1421412528204, 
        "author": "anonymous"
      }, 
      "value": false
    }, 
    "active_snapshots": [], 
    "summary": {
      "entered": 1421412528204, 
      "value": "OFFLINE"
    }
  }
}
```

### Получение инстансов и хостов сервиса {#get-instances-hosts}

Про получение инстансов и хостов через HQ можно [посмотреть тут](../hq/service-instances.md)


### Текущая активная ревизия runtime атрибутов {#active-runtime-attributes-rev}

Метод возвращает ревизию runtime атрибутов, которая в данный момент активна:
* Если сервис **ONLINE** - то оно вернёт текущее активное.
* Если же сервис выключен или выключается - вернёт ошибку.

Основная проблема, с переходным состоянием, когда происходит выкладка сервиса. Разные инстансы могут быть активны в разных ревизиях. Надо выбрать по какой-то эвристике, что отдать. Основная проблема в том, что DEACTIVATE_PENDING может быть больше одного. И в каждой ревизии может быть активно какое-то количество инстансов. Т.к. это эвристика, то все варианты примерно одинаково плохие в каких-то пограничных случаях. При реализации приняли решение в такой ситуации отдавать ту ревизию, которая последний раз была полностью активирована (та, на которую будет откат при нажатии Rollback в UI).

* Шаблон запроса: `/v2/services/<service_id>/active/runtime_attrs/`
* Пример: `/v2/services/production_nanny/active/runtime_attrs/`

Пример ответа:

```json
{
    "_id": "0eb6c3b7d8d3c045939621d0f2150f0c194c4b2c",
    "change_info": {
        "author": "romanovich",
        "comment": "nanny: nanny@stable/0.8.17",
        "ctime": 1482405650450
    },
    "content": {}, // Snapshot content
    "meta_info": {  // Snapshot meta information
        "is_disposable": false,
        "startrek_tickets": [],
        "ticket_info": {
            "ticket_id": "NANNY-996337"
        }
    },
    "parent_id": "2daeebfe4192772369b3020ae5551390c6c67033",
    "service_id": "production_nanny"
}
```

### История runtime атрибутов {#attributes-rev-history}

Метод возвращает историю изменения секции runtime.

* Шаблон запроса: `/v2/services/<service_id>/history/runtime_attrs_infos/?offset=&limit=`
* Пример: `/v2/services/prodution_nanny/history/runtime_attrs_infos/?limit=1`

Пример ответа:

```json
{
  "result": [
    {
      "iss_conf_template": {
        // Тут очень много данных
      },
      "meta_info": {
        "startrek_tickets": [],
        "ticket_info": {
          "release_id": "SANDBOX_RELEASE-935901224-STABLE",
          "ticket_id": "WEB-58920132"
        },
        "infra_notifications": {
          "service_name": "renderer_man",
          "environment_name": "production",
          "environment_id": "906",
          "service_id": "582"
        },
        "is_disposable": false,
        "scheduling_config": {
          "sched_activate_recipe": "dynamic resource activation",
          "scheduling_priority": "NONE",
          "sched_prepare_recipe": "dynamic resource preparation"
        },
        "conf_id": "production_report_renderer_man_web_yp-1617353209130",
        "changes_record": {
          "files": [
            {
              "type": "SANDBOX_FILE",
              "sandbox_file_change": {
                "task_type": "SANDBOX_CI_WEB4",
                "task_id": "935901224",
                "resource_type": "WEB_MICRO_PACKAGE"
              }
            }
          ]
        },
        "annotations": {
          "startable": "true",
          "deploy_engine": "YP_LITE"
        }
      },
      "change_info": {
        "comment": "releases\/frontend\/web4\/v1.1182.0",
        "ctime": 1617353209130,
        "author": "robot-morty"
      },
      "parent_id": "fd50230e5a1b0d589c908c9180e70a1d73285736",
      "service_id": "production_report_renderer_man_web_yp",
      "_id": "5239fcf1319d4efb56eed11876939f8e8fba2da5"
    }
  ]
}
```

### Runtime атрибуты оперделенного снапшота {#runtime-attrs-snapshot}

Метод возвращает runtime атрибуты определенного снапшота.

* Шаблон запроса: `/v2/history/services/runtime_attrs/<snapshot_id>/`
* Пример: `/v2/history/services/runtime_attrs/5239fcf1319d4efb56eed11876939f8e8fba2da5/`

Пример ответа:

```json
{
  "meta_info": {
    "startrek_tickets": [],
    "ticket_info": {
      "release_id": "SANDBOX_RELEASE-935901224-STABLE",
      "ticket_id": "WEB-58920132"
    },
    "infra_notifications": {
      "service_name": "renderer_man",
      "environment_name": "production",
      "environment_id": "906",
      "service_id": "582"
    },
    "is_disposable": false,
    "scheduling_config": {
      "sched_activate_recipe": "dynamic resource activation",
      "scheduling_priority": "NONE",
      "sched_prepare_recipe": "dynamic resource preparation"
    },
    "conf_id": "production_report_renderer_man_web_yp-1617353209130",
    "changes_record": {
      "files": [
        {
          "type": "SANDBOX_FILE",
          "sandbox_file_change": {
            "task_type": "SANDBOX_CI_WEB4",
            "task_id": "935901224",
            "resource_type": "WEB_MICRO_PACKAGE"
          }
        }
      ]
    },
    "annotations": {
      "startable": "true",
      "deploy_engine": "YP_LITE"
    }
  },
  "change_info": {
    "comment": "releases\/frontend\/web4\/v1.1182.0",
    "ctime": 1617353209130,
    "author": "robot-morty"
  },
  "content": {} // snapshot content
  "parent_id": "fd50230e5a1b0d589c908c9180e70a1d73285736",
  "service_id": "production_report_renderer_man_web_yp",
  "_id": "5239fcf1319d4efb56eed11876939f8e8fba2da5"
}
```

### Изменение состояния отдельных инстансов

#### Под YP-lite

Нужно использовать метод [SetInstanceTargetState](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/yp_lite_api/proto/pod_sets_api.proto?rev=5876588#L457) из [YP-lite API](../yp/yp-lite-api.md).

#### Под ISS

Данные методы API работают только под ISS. Для управления отдельными инстансами под YP-lite нужно .

```json
POST /v2/services/instances/<service_id>/sn/<snapshot_id>/engines/<engine>/slots/<port>@<host>/set_target_state/
{
    "target":"{ACTIVE|PREPARED|REMOVED}",
    "comment":"-"
}
```

Пример:

```json
POST /v2/services/instances/prestable_[alemate_master_copy_alonger/sn/53ea399b611b020a9b96653ab87588e059437949/engines/ISS_MAN/slots/18112@man1-3050.search.yandex.net](alemate_master_copy_alonger/sn/53ea399b611b020a9b96653ab87588e059437949/engines/ISS_MAN/slots/18112@man1-3050.search.yandex.net)/set_target_state/
{
"target":"ACTIVE",
"comment":"Go go go!"
}
```

### Информационные атрибуты

Атрибуты, изменения которых не должны быть отражены на хостах. 

Пример:

```json
{
  "_id": "549952eafd86263b39fa69e1", 
  "change_info": {
    "comment": "-", 
    "ctime": 1419334378392, 
    "author": "nekto0n"
  }
  "content": {
    "category": "/users/nekto0n", 
    "recipes": {
      "content": [
        {
          "context": [], 
          "id": "common", 
          "name": "_activate_service_configuration.yaml", 
          "desc": "Common deploy script"
        }
      ]
    }, 
    "desc": "Test sleep service"
  }
}
```

#### Схема {#scheme}

JSON-схема полного содержимого атрибутов, в том числе, `info_attrs`, доступна по адресу: [https://nanny.yandex-team.ru/v2/schemas/service/](https://nanny.yandex-team.ru/v2/schemas/service/)

##### Получение {#scheme-get}

* Шаблон: `/v2/services/<_id>/info_attrs/`
* Пример: `/v2/services/production_balancer_msk/info_attrs/`

##### Изменение {#scheme-update}

* Метод: `PUT`
* Шаблон: `/v2/services/<_id>/info_attrs/`

Тело запроса:

```json
{
	"comment": "Change description",
	"snapshot_id": "54b908b069faf339952f7d84",
	"content": {
	    "desc": "Production installation of bla service!",
	    "category": "/",
	    "recipes": {"content": []}
	}
}

```

* Ответ: новая ревизия (snapshot) атрибутов.

#### Конфликты при изменении {#conflicts}

Если при применении изменений указанный в запросе `snapshot_id` не соотвествует тому, который в данный момент хранится в базе данных, то сервис вернёт ошибку `409 Conflict`.

### Runtime атрибуты {#runtime-attributes}

Атрибуты, изменения которых должны быть отражены на хостах. 

```json
{
  "_id": "54b7bf36494013000648801c",
  "change_info": {
    "author": "romanovich",
    "comment": "sleep 10001",
    "ctime": 1421328182941
  },
  "content": {
    "instances": {
      "chosen_type": "INSTANCE_LIST",
      "gencfg_groups": [],
      "instance_list": [
        {
          "host": "ws16-388",
          "port": 34555,
          "tags": []
        }
      ]
    },
    "resources": {
      "balancer_config_files": [],
      "sandbox_files": [
        {
          "local_path": "loop-httpsearch",
          "resource_type": "LOOP",
          "task_id": "19100987",
          "task_type": "RELEASE_LOOP"
        }
      ],
      "static_files": [
        {
          "content": "# Stub for bsconfig (NEW)",
          "local_path": "httpsearch"
        },
        {
          "content": "[nanny]\nbinary = /bin/sleep\narguments= 10001",
          "local_path": "loop.conf"
        },
        {
          "content": "# Stub",
          "local_path": "apache.ywsearch.cfg"
        }
      ],
      "url_files": []
    }
  },
  "meta_info": { "is_disposable": false }
}
```

####  Схема {#runtime-attributes-scheme}

JSON-схема полного содержимого атрибутов, в том числе, `runtime_attrs`, доступна по адресу: [https://nanny.yandex-team.ru/v2/schemas/service/](https://nanny.yandex-team.ru/v2/schemas/service/)

##### Получение {#runtime-attributes-scheme-get}

* Шаблон: `/v2/services/<_id>/runtime_attrs/`
* Пример: `/v2/services/production_balancer_msk/runtime_attrs/`

##### Изменение {#runtime-attributes-scheme-update}

* Метод: `PUT`
* Шаблон: `/v2/services/<_id>/runtime_attrs/`

Тело запроса:
```json
{
  "content": {
    "instances": {
      "instance_list": [], 
      "gencfg_groups": [
        {
          "release": "trunk", 
          "name": "MSK_SG_NANNY", 
          "tags": []
        }
      ], 
      "chosen_type": "GENCFG_GROUPS"
    }, 
    "resources": {
      "sandbox_files": [
        {
          "resource_type": "LOOP", 
          "local_path": "loop-httpsearch", 
          "task_type": "BUILD_LOOP", 
          "task_id": "32435345"
        }
      ], 
      "static_files": [
        {
          "content": "#Some content", 
          "local_path": "loop.conf"
        }
      ], 
      "balancer_config_files": [], 
      "url_files": []
    }
  },
  "meta_info": {  # Optional
      "is_disposable": false,
      "startrek_tickets": ["FAKE-QUEUE-1", "FAKE_QUEUE-2"]
  },
  "comment": "Proper instances description", 
  "snapshot_id": "54be30cd69faf3716165a925"
}
```

#### Конфликты при изменении {#runtime-attributes-scheme-conflicts}

Если при применении изменений указанный в запросе `snapshot_id` не соотвествует тому, который в данный момент хранится в базе данных, то сервис вернёт ошибку `409 Conflict`.

#### Изменение одного файла {#update-single-file}

Для того, чтобы упростить ежедневные задачи пользователя Service Repo предоставляет возможно изменить/добавить конкретный файл сервиса без указания `snapshot_id`.

Формат запроса: `PUT /v2/services/<service_id>/runtime_attrs/resources/files/<file_section>/`

Где:
* **service_id** - идентификатор сервиса, например, production_webmmeta_msk;
* **file_section** - один из поддерживаемых типов файлов:
    * static_files
    * sandbox_files
    * url_files
    * balancer_config_files
    * template_set_files

Пример: `PUT /v2/services/production_nanny/runtime_attrs/resources/files/static_files/`

Тело запроса:

```json
{
    "content": {<атрибуты файла выбранного типа>},
    "comment": "<комментарий описывающий изменения>"
    ["meta_info": {"is_disposable": false}]
}
```

Пример тела запроса:

```json
{
    "content": {
        "local_path": "loop.conf",
        "content": "[search]\nargs=/bin/sleep 100"
        },
    "comment": "Update loop.conf",
    "meta_info": {
        "is_disposable": true
    }
}
```

###### Семантика работы {#semantics}

* Если сервис не найден - возвращается 404 Not Found.
* Если у пользователя отсутствуют права на изменения файлов - возвращается 403 Not Authorized.
* Если условия выполнены, то система начинает в цикле выполнять Compare-And-Set операцию: вычитывает ревизию runtime атрибутов, изменяет/добавляет файл, пытается сохранить.
* Если в запросе указана мета-информация, она будет включена в результирующий снэпшот runtime атрибутов.

#####  Изменение секции runtime атрибутов {#set-runtime-section}

Для того, чтобы упростить ежедневные задачи пользователя Service Repo предоставляет возможно изменить/добавить одну секцию runtime атрибутов сервиса файл сервиса без указания `snapshot_id`.

Формат запроса: `PUT /v2/services/<service_id>/runtime_attrs/<section_name>/`
Где:

* **service_id** - идентификатор сервиса, например, production_webmmeta_msk;
* **section_name** - название одной из секций:
    * resources - описание файловых ресурсов
    * instances - описание расположения и прочие атрибутов инстансов сервиса
    * engines - описание используемой системы выкладки (ISS/Bsconfig)

Пример: `PUT /v2/services/production_nanny/runtime_attrs/instances/`

Тело запроса:

```json
{
    "content": {<атрибуты выбранной секции>},
    "comment": "<комментарий описывающий изменения>",
    ["snapshot_id": "<идентификатор runtime атрибутов, которые необходимо изменить (Compare-And-Swap)>"]
}
```
Пример тела запроса:

```json
{
    "content": {
        "chosen_type": "GENCFG_GROUPS",
    	"gencfg_groups": [
    		{
        		name: "MSK_SG_NANNY",
        		release: "tags/stable-72-r31",
        		tags: []
        	}
    	]
    },
    "comment": "Update gencfg groups",
    "snapshot_id": "b018c05cba7ec41c1a1d3c5780693dc5c0b0e075"  // Можно не указывать
}
```

Чем оно отвечает? Отвечает оно полностью всей конфигурацией из runtime_attrs (что, кстати, не очень удобно)

###### Семантика работы {#semantics-runtime-section}

* Если сервис не найден - возвращается 404 Not Found.
* Если у пользователя отсутствуют права на изменения файлов - возвращается 403 Not Authorized.
* Если указан snapshot_id и при попытке обновления он будет не актуальным - возвращается 400 Bad Request

#### Авторизационные атрибуты {#authorization-attributes}

Описывают права доступа к изменениям остальных атрибутов сервиса.

```json
{
  "_id": "54b9123569faf370f651424b", 
  "change_info": {
    "author": "anonymous", 
    "comment": "Calibrations...", 
    "ctime": 1421414965613
  }, 
  "content": {
    "conf_managers": {
      "groups": [], 
      "logins": ["liara"]
    }, 
    "ops_managers": {
      "groups": [], 
      "logins": ["garrus"]
    }, 
    "owners": {
      "groups": [], 
      "logins": [
        "shepard"
      ]
    }
  }
}
```

##### Получение {#authorization-attributes-get}

* Шаблон: `/v2/services/<_id>/auth_attrs/`
* Пример: `/v2/services/production_balancer_msk/auth_attrs/`

##### Изменение {#authorization-attributes-update}

* Метод: `PUT`
* Шаблон: `/v2/services/<_id>/auth_attrs/`

Формат запроса:

```json
{
  "comment": "-",
  "snapshot_id": "54b9123569faf370f651424b",
  "content": {
    "owners": {
      "logins": [
        "anonymous"
      ], 
      "groups": []
    }, 
    "conf_managers": {
      "logins": [
        "nekto0n"
      ], 
      "groups": []
    }, 
    "ops_managers": {
      "logins": [
        "nekto0n"
      ], 
      "groups": []
    }
  }
}
```

### Получение всех аспектов сервиса {#get-all}

Получаем список всех аспектов сервиса:

```json
{
    "id": "production_nanny",
    "runtime": {...},
    "info": {...},
    "auth": {...},
    "cleanup_policy": (null|{...})
}
```

#### Получение {#receiving}

* Шаблон: `/v2/services/<_id>/aspects/`
* Пример: `/v2/services/production_balancer_msk/aspects/`

### События {#events}

#### Получить конкретное событие {#events-get}

  * Шаблон: `GET /v2/service_events/<event_id>/`
  * Формат ответа (запрошенное событие):
```json
{
 "_id": "551b99643895240ff00da6c5",
 "info": {"author": "nanny-robot", "comment": "-", "ctime": 1427872100614},
 "mtime": 1427872100741,
 "outcome": {"author": "nanny-robot"},
 "service_id": "production_nanny",
 "status": "DONE",
 "tg_status_change": {
      "status": "DONE",
      "taskgroup_id": "search-0000221736"
 },
 "type": "TASK_GROUP_STATUS_CHANGE"
}
```

Возможные статусы событий:
* `IN_QUEUE` - событие в очереди на обработку
* `ACTIVE` - событие в данный момент обрабатывается
* `DONE` - событие было успешно обработано
* `CANCELLED` - обработка события была отменена вручную
* `FAILED` - событие было неуспешно обработано системой, больше попыток обработать не будет
Примеры причин:
  * аллокация для снэпшота была удалена и активировать его больше нельзя.
  * новое состояние снэпшотов сервиса не прошло валидацию, например, слишком много снэпшотов.

#### Получение списка событий сервиса {#events-from-service}

* Шаблон: `GET /v2/services/<service_id>/events/`
    * по-умолчанию события отсортированы по убыванию времени создания (атрибут `info.ctime`)
    * поддерживаются следующие параметры запроса:
        * `limit` и `skip` - число объектов и сдвиг в списке объектов (для реализация страниц).
        * `ctime_gt` - время создания события больше указанного, формат - unix timestamp в миллисекундах (целое число).
* Формат ответа: список событий.

### Список сервисов {#service-list}

* Шаблон: `GET /v2/services/?limit=<limit>&skip=<skip>[&exclude_runtime_attrs=1][&category=<category>]`
    * по-умолчанию сервисы отсортированы лексикографически по возрастанию атрибута `_id`.
    * `limit` и `skip` - число объектов и сдвиг в списке объектов (для реализация страниц). **Skip может игнорироваться, см следующий пункт.**
    * `exclude_runtime_attrs` - возвращать ли runtime атрибуты в описаниях сервисов. Используется для уменьшения длительности запроса к базе данных и размера ответа. При использовании этого параметра паджинация игнорируется, см SWAT-4561
    * `category` - выбрать сервисы только из заданной категории, например, `/traffic/yandex`.
* Формат ответа: список документов с полным описанием каждого сервиса (описано выше).

## Примеры работы с API {#api-samples}

Для работы с API из sandbox предпочтительнее и проще использовать [клиент](../../how-to/sandbox-integration.md), доступный из sandbox-задач, код которого доступен [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/common/nanny/nanny.py).

Приведенные ниже примеры позволяют работать с API вне sandbox-задачи:

### Обновление версии sandbox-ресурса {#sandbox-res-update}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests


NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
OAUTH_TOKEN = 'YOUR_OAUTH_TOKEN'

TASK_TYPE = 'BUILD_INSTANCE_CTL'
RESOURCE_TYPE = 'INSTANCECTL'
TASK_ID = '44835240'


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    services = [
        'my_first_great_service',
        'my_second_great_service',
    ]

    for service in services:
        resources_url = urljoin(NANNY_URL, 'v2/services/{}/runtime_attrs/'.format(service))
        response = session.get(resources_url)

        if not response.ok:
            print 'Could not get resources of service', service
            print response.status_code
            print response.text
            continue

        response_dict = response.json()
        snapshot_id = response_dict['_id']
        content = response_dict['content']

        # look up for appropriate resource
        for resource in content['resources']['sandbox_files']:

            if resource['task_type'] == TASK_TYPE and resource['resource_type'] == RESOURCE_TYPE:

                # bump if new version is newer then current service resource version
                if int(resource['task_id']) < int(TASK_ID):
                    resource['task_id'] = TASK_ID

        request = {
            'snapshot_id': snapshot_id,
            'content': content,
            'comment': 'Bump INSTANCECTL to stable/1.2.54',
        }

        print 'Applying for', service
        response = session.put(resources_url, data=json.dumps(request))
        print 'Result:', response.status_code

        if not response.ok:
            print response.text

```

### Изменение Deploy Engine {#change-deploy-engine}

```python
import requests


NANNY_URL = 'http://nanny.yandex-team.ru/'.rstrip('/')
NEW_ENGINE = 'ISS_MULTI'
OAUTH_TOKEN = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'

if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)

    services = [
        'my_service_id',
    ]

    for service in services:
        resources_url = '{}/v2/services/{}/runtime_attrs/engines/'.format(NANNY_URL, service)
        resp = session.get(resources_url)
        resp.raise_for_status()
        d = resp.json()
        snapshot_id = d['snapshot_id']
        content = d['content']
        content['engine_type'] = NEW_ENGINE

        req = {
            'snapshot_id': snapshot_id,
            'content': content,
            'comment': 'Set deploy engine {}'.format(NEW_ENGINE),
        }

        print 'Applying for', service
        resp = session.put(resources_url, json=req)
        resp.raise_for_status()
        print 'OK'

```

### Изменение версии gencfg-топологии инстансов {#change-gencfg-topo}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests


NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
OAUTH_TOKEN = 'YOUR_OAUTH_TOKEN'

GENCFG_TOPOLOGY_TAG = 'tags/stable-81-r2'


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    services = [
        'my_first_great_service',
        'my_second_great_service',
    ]

    for service in services:
        attrs_url = urljoin(NANNY_URL, 'v2/services/{}/runtime_attrs/'.format(service))
        response = session.get(attrs_url)

        if not response.ok:
            print 'Could not get resources of service', service
            print response.status_code
            print response.text
            continue

        response_dict = response.json()
        snapshot_id = response_dict['_id']
        content = response_dict['content']

        if not content['instances'].get('extended_gencfg_groups'):
            print service, 'has no gencfg groups'
            continue

        for group in content['instances']['extended_gencfg_groups']['groups']:
            group['release'] = GENCFG_TOPOLOGY_TAG

        request = {
            'snapshot_id': snapshot_id,
            'content': content,
            'comment': 'Bump gencfg topology to {}'.format(GENCFG_TOPOLOGY_TAG),
        }

        print 'Applying for', service
        response = session.put(attrs_url, data=json.dumps(request))
        print 'Result:', response.status_code

        if not response.ok:
            print response.text
```

### Активация заданного снэпшота {#snapshot-activate}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests


NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
OAUTH_TOKEN = 'YOUR_OAUTH_TOKEN'

SNAPSHOT_ID = '1234567890'
RECIPE = 'common'


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    service = 'my_great_service'

    events_url = urljoin(NANNY_URL, 'v2/services/{}/events/'.format(service))

    event = {
        'content': {
            'snapshot_id': SNAPSHOT_ID,
            'state': 'ACTIVE',
            'comment': 'Activate {} snapshot!'.format(SNAPSHOT_ID),
            'recipe': RECIPE,
        },
        'type': 'SET_SNAPSHOT_STATE',
    }

    result = session.post(events_url, data=json.dumps(event))

    print 'Result', result.status_code
    if not result.ok:
        print result.text
```

### Удаление всех снэпшотов сервиса {#kill-all-snapshots}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests


NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
OAUTH_TOKEN = 'YOUR_OAUTH_TOKEN'


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    service = 'my_great_service'

    snapshots_url = urljoin(NANNY_URL, 'v2/services/{}/history/runtime_attrs/'.format(service))
    response = session.get(snapshots_url)
    response.raise_for_status()

    events_url = urljoin(NANNY_URL, 'v2/services/{}/events/'.format(service))

    for snapshot in response.json()['result']:

        snapshot_id = snapshot['_id']
        event = {
            'content': {
                'snapshot_id': snapshot_id,
                'state': 'DESTROYED',
                'comment': 'Destroying all service snapshots',
            },
            'type': 'SET_SNAPSHOT_STATE',
        }

        print 'Destroying snapshot', snapshot_id
        result = session.post(events_url, data=json.dumps(event))
        print 'Result', result.status_code
        if not result.ok:
            print result.text
```

### Задание инстансов через список {#instances-list}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests


NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
OAUTH_TOKEN = 'YOUR_OAUTH_TOKEN'
SERVICE = 'my_great_service'

INSTANCES = [
    {'host': 'fake-host.search.yandex.net', 'port': 6666, 'weight': 1},
    {'host': 'fake-host2.search.yandex.net', 'port': 6666, 'weight': 1},
    {'host': 'fake-host3.search.yandex.net', 'port': 6666, 'weight': 1},
]


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    attrs_url = urljoin(NANNY_URL, 'v2/services/{}/runtime_attrs/'.format(SERVICE))
    response = session.get(attrs_url)

    if not response.ok:
        print 'Could not get resources of service', SERVICE
        print response.status_code
        print response.text
    else:
        response_dict = response.json()
        snapshot_id = response_dict['_id']
        content = response_dict['content']

        content['instances'] = {'instance_list': INSTANCES,
                                'chosen_type': 'INSTANCE_LIST'}

        request = {
            'snapshot_id': snapshot_id,
            'content': content,
            'comment': 'Set {} instances as INSTANCE_LIST'.format(len(INSTANCES)),
        }

        print 'Applying for', SERVICE
        response = session.put(attrs_url, data=json.dumps(request))
        print 'Result:', response.status_code

        if not response.ok:
            print response.text
```

### Копирование сервиса {#service-copy}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests


NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
OAUTH_TOKEN = 'YOUR_OAUTH_TOKEN'

COPY_INSTANCES = False
COPY_AUTH_ATTRS = True


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    source_service = 'my_source_service'
    destination_service = 'my_destination_service'

    events_url = urljoin(NANNY_URL, 'v2/services/{}/copies/'.format(source_service))

    req = {
        'id': destination_service,
        'copy_auth_attrs': COPY_AUTH_ATTRS,
        'copy_instances': COPY_INSTANCES,
        'category': '/my_category/',
        'desc': 'My new service human-readable description',
    }

    result = session.post(events_url, data=json.dumps(req))
    print result.status_code
    print result.text
```


### Удаление всех событий по изменению состояния сервиса {#cler-by-trigger}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests
from werkzeug.urls import url_encode


NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
OAUTH_TOKEN = 'YOUR_OAUTH_TOKEN'


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    service = 'my_great_service'

    events_url = urljoin(NANNY_URL, '/v2/service_events/')
    response = session.get(events_url,
                           params={'filter': url_encode({'service_id': service})})
    response.raise_for_status()

    for event in response.json()['result']:
        if event['status'] == 'IN_QUEUE':
            url = urljoin(events_url, '/v2/service_events/{}/cancel/'.format(event['_id']))
            response = session.post(url,
                                    data=json.dumps({'comment': 'Clear event queue'}))
            response.raise_for_status()
            print event['_id'], response.status_code
```

### Перенос сервиса между инсталляциями Nanny {#move-service}

```python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

import json
from urlparse import urljoin

import requests


SRC_NANNY_URL = 'http://nanny.yandex-team.ru/'
DST_NANNY_URL = 'http://dev-nanny.yandex-team.ru/'
SRC_OAUTH_TOKEN = 'SRC_OAUTH_TOKEN'
DST_OAUTH_TOKEN = 'DST_OAUTH_TOKEN'
SRC_SERVICE_NAME = 'src_fake_service'
DST_SERVICE_NAME = 'dst_fake_service'


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(SRC_OAUTH_TOKEN)
    session.headers['Content-Type'] = 'application/json'

    src_attrs_url = urljoin(SRC_NANNY_URL, 'v2/services/{}/runtime_attrs/'.format(SRC_SERVICE_NAME))
    response = session.get(src_attrs_url)
    response.raise_for_status()
    src_content = response.json()['content']

    dst_attrs_url = urljoin(DST_NANNY_URL, 'v2/services/{}/runtime_attrs/'.format(DST_SERVICE_NAME))
    session.headers['Authorization'] = 'OAuth {}'.format(DST_OAUTH_TOKEN)
    response = session.get(dst_attrs_url)
    response.raise_for_status()
    snapshot_id = response.json()['_id']

    request = {
        'snapshot_id': snapshot_id,
        'comment': 'Copying service content from {} from {}'.format(SRC_SERVICE_NAME, SRC_NANNY_URL),
        'content': src_content,
    }

    print 'Applying...'
    response = session.put(dst_attrs_url, data=json.dumps(request))
    response.raise_for_status()
```

### Добавление администратора в несколько сервисов {#one-admin-in-services}

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals
from __future__ import print_function

import os
from urlparse import urljoin

import requests

NANNY_URL = 'http://nanny.yandex-team.ru/'
OAUTH_TOKEN = os.getenv('OAUTH_TOKEN')

COMMENT = 'Batch add new admins'

GROUPS_TO_REMOVE = []
LOGINS_TO_ADD = []
SERVICES = ['service_one', 'service_two']


def update_services(session):
    for s_id in SERVICES:
        resp = session.get(urljoin(NANNY_URL, 'v2/services/{}/'.format(s_id)))
        resp.raise_for_status()
        service = resp.json()
        snapshot_id = service['auth_attrs']['_id']
        auth_attrs = service['auth_attrs']['content']

        for category in ['owners', 'ops_managers', 'conf_managers']:
            for g in GROUPS_TO_REMOVE:
                if g in auth_attrs[category]['groups']:
                    auth_attrs[category]['groups'].remove(g)
            for l in LOGINS_TO_ADD:
                if l not in auth_attrs[category]['logins']:
                    auth_attrs[category]['logins'].append(l)

        service_url = urljoin(NANNY_URL, 'v2/services/{}/auth_attrs/'.format(s_id))
        print('Updating', service['_id'])
        # print(json.dumps(auth_attrs, indent=4))

        r = session.put(service_url, json={
            'snapshot_id': snapshot_id,
            'content': auth_attrs,
            'comment': COMMENT,
        })
        print(r.status_code)
        r.raise_for_status()


if __name__ == '__main__':
    session = requests.Session()
    session.headers['Authorization'] = 'OAuth {}'.format(OAUTH_TOKEN)
    update_services(session)

```
