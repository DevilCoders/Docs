
## Api планера

Продакшен – https://planner.market.yandex-team.ru/api/v1\
Тестинг – https://planner-test.market.yandex-team.ru/api/v1

Swagger:
[Testing](https://planner-test.market.yandex-team.ru/swagger-ui/index.html#/)
[Production](https://planner.market.yandex-team.ru/swagger-ui/index.html#/)\
http://localhost:8080/swagger-ui/index.html#/\
http://localhost:8080/v2/api-docs


У планера есть апи, с помощью которого можно автоматизировать некоторую рутинную работу.\
Токен для авторизации можно получить по ссылке\
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=add4041d6cb440ebba4b39b9862b47f3

Токен необходимо передавать в заголовке запроса. Пример запроса:
```
curl https://planner-test.market.yandex-team.ru/api/v1/employees/list/56458 -H "Authorization: OAuth <токен>"
```

#### Доступные ручки:

**GET /employees/list/<department_id>**

Получить список сотрудников в департаменте включая поддепартаменты.\
Пример запроса:
```
curl https://planner-test.market.yandex-team.ru/api/v1/employees/list/56458 -H "Authorization: OAuth <токен>"
```
Формат ответа:
```
{
  "employee_login_1": {
    "login": "employee_login",
    "name": "Имя Фамилия",
    "role": "dev",
    "position": "Разработчик",
    "vacancy": false,
    "job_ticket": null,
    "department_id": 88399,
    "competencies": null,
    "dismissed": false,
    "vacancy_start_date": null,
    "dismissedAt": null
  },
  "employee_login_2" : {
    ...
  },
  ...
}
```

**POST /employees/add**

Создает вакансию\
Передаваемые данные:
```
{
    "department_id": departmentId,
    "login": login,
}
```

Пример запроса:
```
curl -X POST -d '{"department_id":56458, "login":"JOB-test_ticket"}' https://planner-test.market.yandex-team.ru/api/v1/employees/add -H "Authorization: OAuth <oauth_token>" -H "Content-Type: application/json"
```

Формат ответа:
```
{
  "login": "JOB-test_ticket",
  "name": "JOB-TEST_TICKET",
  "role": "unknown",
  "position": null,
  "vacancy": true,
  "job_ticket": "JOB-test_ticket",
  "department_id": 56458,
  "competencies": null,
  "dismissed": null,
  "vacancy_start_date": "26.02.2021",
  "dismissedAt": null
}
```

**POST /employees/delete/<JOB-ticket>**

Удаляет вакансию

Пример запроса:
```
curl -X POST https://planner-test.market.yandex-team.ru/api/v1/employees/delete/JOB-test_ticket -H "Authorization: OAuth <oauth_token>"
```

**POST /projects_with_request_by_logins**

Список проектов и заявок по запрашиваемым сотрудникам. Передаем список логинов сотрудников.

Логика работы ручки:
```
если есть факт, берём его
если есть планы, то любой из них
если планов и фактов нет, то должен быть relocation
```

Пример запроса:
```
curl -X POST -d '["pavellysenko"]' https://planner-test.market.yandex-team.ru/api/v1/projects_with_request_by_logins -H "Authorization: OAuth <oauth_token>" -H "Content-Type: application/json"
```

Формат ответа:
```
{
  "pavellysenko": {
    "project": {
      "project_id": 41160,
      "priority": 0,
      "created_by": "pavellysenko",
      "created_at": "2021-02-16T09:58:48.720+0000",
      "project_desc": "fact-pavellysenko-01.02.2021",
      "hidden": false,
      "requests": [],
      "colors": {
        "w": 1
      },
      "contours": {
        "1": 0.5,
        "2": 0.5
      }
    },
    "request": {
      "request_id": 41768,
      "project_id": 41160,
      "created_at": "2021-02-16T09:58:48.720+0000",
      "type": "fact",
      "status": "accepted",
      "status_changed_by": "pavellysenko",
      "status_changed_at": "2021-02-26T10:45:58.535+0000",
      "department_id_from": 56458,
      "department_id_to": 56458,
      "specialization_id": 0,
      "employee": "pavellysenko",
      "date_start_requested": "01.02.2021",
      "date_start": "01.02.2021",
      "date_end": "28.02.2021",
      "job_size_requested": "1m",
      "job_size": "1m",
      "job_load_requested": 1,
      "job_load": 1,
      "job_load_perc_requested": 100,
      "job_load_perc": 100,
      "description": "fact-rq-pavellysenko",
      "resolution": null,
      "cellId": 0,
      "request_author": "pavellysenko"
    }
  }
}
```

**POST /confirmRelocation/<employee_login>**

Проставляет/меняет дефолт у сотрудника.\
Передаваемые данные:
```
{
    "contours": {
        "contour_id_1": contour_1_load,
        "contour_id_2": contour_2_load,
        ...
    },
    "colors": {
        "color_1": color_1_load,
        "color_2": color_2_load,
        ...
    }
}
```

Список доступных цветов:
```
//список соответствует финанситам за исключением категорий в Беру
r("Bringly (Красный)"), //бывший просто Red
w("Я.Маркет (Белый)"),  //бывший просто White
b("Беру (Синий)"),   // бывший просто Blue
lb("Доставка синего"),
lw("Я.Доставка"),  //бывшая доставка белого
lr("Доставка красного"),
ff("ФФ"),
dp("Аналитическая платформа"), //бывшие Distribution products
o("OverHeads (WB)"),
sc("FMCG (supercheck)"),
s("Советник");  //Советник, относиться к Белому
```

Пример запроса:
```
curl -X POST -d '{"contours":{"1":0.5,"2":0.5}, "colors":{"w":1}}' https://planner-test.market.yandex-team.ru/api/v1/confirmRelocation/pavellysenko -H "Authorization: OAuth <oauth_token>" -H "Content-Type: application/json"
```

Формат ответа:
```
{
  "project": {
    "project_id": 44734,
    "priority": null,
    "created_by": "mstattest",
    "created_at": null,
    "project_desc": "relocation-pavellysenko-01.02.2021",
    "hidden": true,
    "requests": [],
    "colors": {
      "w": 1
    },
    "contours": {
      "1": 0.5,
      "2": 0.5
    }
  },
  "request": {
    "request_id": 45348,
    "project_id": 44734,
    "created_at": null,
    "type": "employee_relocation",
    "status": "accepted",
    "status_changed_by": "mstattest",
    "status_changed_at": null,
    "department_id_from": 56458,
    "department_id_to": 56458,
    "specialization_id": null,
    "employee": "pavellysenko",
    "date_start_requested": "26.02.2021",
    "date_start": "26.02.2021",
    "date_end": "25.02.3021",
    "job_size_requested": "1000y",
    "job_size": "1000y",
    "job_load_requested": 1,
    "job_load": 1,
    "job_load_perc_requested": 100,
    "job_load_perc": 100,
    "description": "relocation-rq-pavellysenko",
    "resolution": null,
    "cellId": null,
    "request_author": "mstattest"
  }
}
```

**POST /confirmFact/<employee_login>**

Подтверждает факт у сотрудника\
Передаваемые данные:
```
{
    "contours": {
        "contour_id_1": contour_1_load,
        "contour_id_2": contour_2_load,
        ...
    },
    "colors": {
        "color_1": color_1_load,
        "color_2": color_2_load,
        ...
    }
}
```

Пример запроса:
```
curl -X POST -d '{"contours":{"1":0.5,"2":0.5}, "colors":{"w":1}}' https://planner-test.market.yandex-team.ru/api/v1/confirmFact/pavellysenko -H "Authorization: OAuth <oauth_token>" -H "Content-Type: application/json"
```

Формат ответа:
```
{
  "project": {
    "project_id": 41160,
    "priority": 0,
    "created_by": "pavellysenko",
    "created_at": "2021-02-16T09:58:48.720+0000",
    "project_desc": "fact-pavellysenko-01.02.2021",
    "hidden": false,
    "requests": [],
    "colors": {
      "w": 1
    },
    "contours": {
      "1": 0.5,
      "2": 0.5
    }
  },
  "request": {
    "request_id": 41768,
    "project_id": 41160,
    "created_at": "2021-02-16T09:58:48.720+0000",
    "type": "fact",
    "status": "accepted",
    "status_changed_by": "pavellysenko",
    "status_changed_at": "2021-02-16T09:58:48.720+0000",
    "department_id_from": 56458,
    "department_id_to": 56458,
    "specialization_id": 0,
    "employee": "pavellysenko",
    "date_start_requested": "01.02.2021",
    "date_start": "01.02.2021",
    "date_end": "28.02.2021",
    "job_size_requested": "1m",
    "job_size": "1m",
    "job_load_requested": 1,
    "job_load": 1,
    "job_load_perc_requested": 100,
    "job_load_perc": 100,
    "description": "fact-rq-pavellysenko",
    "resolution": null,
    "cellId": 0,
    "request_author": "pavellysenko"
  }
}
```

**GET /contours/tree**

Получить актуальный список групп контуров со списком контуров.\
Пример запроса:
```
curl https://planner-test.market.yandex-team.ru/api/v1/contours/tree -H "Authorization: OAuth <токен>"
```
Формат ответа:
```
{
  "0": {
    "id": 0,
    "name": "Без группы",
    "contours": [
      {
        "id": 96,
        "name": "Вендора",
        "target": null,
        "groupId": 0,
        "deleted": true,
        "fteLimit": 0,
        "description": null,
        "createdAt": 1603227600000,
        "tags": {},
        "businessUnitIds": [1]
      },
      {
        "id": 26,
        "name": "Вне контура",
        "target": null,
        "groupId": 0,
        "deleted": true,
        "fteLimit": 0,
        "description": null,
        "createdAt": 1603227600000,
        "tags": {},
        "businessUnitIds": [1]
      }
    ]
  },
  "1": {
    "id": 1,
    "name": "Инфраструктура аналитики",
    "contours": [
      {},
      {},
      ...
    ]
  }
}
```

**GET /contours/groups**

Получить актуальный список групп контуров со списком контуров.\

Есть необязательные фильтры:

`from` - дата начала выборки\
`to` - дата окончания выборки\
`businessUnitId` - бизнесс юнит\
`dep` - департамент\
`supervisors` - список менеджеров

Пример запроса:
```
curl https://planner-test.market.yandex-team.ru/api/v1/contours/groups?dep=56458 -H "Authorization: OAuth <токен>"
```
Формат ответа:
```
[
  {
    "id": 144,
    "name": "B2B Продукт",
    "contours": [
      {
        "id": 2,
        "name": "Маркет для производителей",
        "target": "https://abc.yandex-team.ru/services/market4vendor/",
        "groupId": 144,
        "deleted": false,
        "fteLimit": 0,
        "description": "описание",
        "employer": "заказчик",
        "productOwner": "Product owner",
        "techLead": "Tech lead",
        "stQueues": "очереди в трекере",
        "stProjectTickets": "тикеты",
        "wikiLinks": "ссылки на вики - опционально",
        "boards": "дэшборды - опционально",
        "tags": {
          "2": "tag2",
          "4": "tag4"
        }
      }
    ],
    "size": 0.5,
    "fteLimit": 0,
    "supervisors": null
  },
  {...},
   ...
]
```

**POST /contours/<contour_id>**

Обновить информацию о контуре

Передаваемые данные:
```
{
    contour: {
    "id": 2,
    "name": "Маркет для производителей",
    "target": "https://abc.yandex-team.ru/services/market4vendor/",
    "groupId": 144,
    "deleted": false,
    "fteLimit": 0,
    "description": "описание",
    "employer": "заказчик",
    "productOwner": "Product owner",
    "techLead": "Tech lead",
    "stQueues": "очереди в трекере",
    "stProjectTickets": "тикеты",
    "wikiLinks": "ссылки на вики - опционально",
    "boards": "дэшборды - опционально",
    "tags": {
        "2": "tag2",
        "4": "tag4"
    },
    "businessUnitIds": [
        1
    ]
},
    supervisors: ["логины менеджеров"]
}
```

Пример запроса:
```
curl -X POST -d '{"contour":{"description": "Новый контур","employer": "daniilpozdeev","productOwner": "daniilpozdeev", \
    "techLead": "daniilpozdeev","stQueues": "https://st.yandex-team.ru/PLANNERSDEV/order:updated:true/filter?resolution=empty()",\
    "stProjectTickets": "MARKETQPLANNER-435, MARKETQPLANNER-1151", \
    "wikiLinks": "https://wiki.yandex-team.ru/Market/projects/marketstat/support/mstat-planner/", \
    "boards": "https://st.yandex-team.ru/agile/board/12308","fteLimit":0,"groupId":145,"id":644,"name":"11111", \
    "target":"","businessUnitIds":[1]},"supervisors":["pavellysenko"]}' \
    https://planner-test.market.yandex-team.ru/api/v1/contours/644 \
     -H "Authorization: OAuth <oauth_token>" -H "Content-Type: application/json"
```
