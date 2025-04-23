# Список пользователей и ролей (get-all-roles)

Выдает список пользователей и ролей для сверки и синхронизации данных между БД системы и БД IDM.

При использовании запроса `get-all-roles` информация о ролях передается по сети в одном JSON-документе. Запрос может быть использован для систем с небольшим количеством ролей.

{% include [idm-get-roles-note-1](../_includes/concepts/idm-get-roles/id-idm-get-roles/note-1.md) %}

## Синтаксис запроса {#section_brx_zzj_wcb}

```
GET https://{адрес запрашиваемого ресурса}/get-all-roles
```

## Описание полей ответа {#section_kzm_11k_wcb}

В ответе могут содержаться следующие поля: 

#|
||Поле | Описание | Тип данных||
||`users` | Блок со списком логинов пользователей и выданных им ролей. | Массив||
||`login` | Логин пользователя со [Стаффа](https://staff-api.yandex-team.ru/v3/). | Строка||
||`roles` | Список ролей пользователя или группы. | Массив||
||`groups` | Блок со списком групп и выданных ролей на эту группу. Системы [group-unaware](glossary.md#group-unaware) могут не передавать ключ `groups`. | Массив||
||`group` | В ключе `groups`: идентификатор (id) группы на [Стаффе](https://staff-api.yandex-team.ru/v3/). В ключе `roles`: название группы. | Строка||
|#

## Пример запроса {#section_iqv_1ct_xcb}

```

GET https://doc-test.tools.yandex-team.ru/client-api/get-all-roles/
```

## Примеры ответов {#section_ecv_m4q_wcb}


{% cut "Пример ответа с дополнительными параметрами" %}

Для передачи списка ролей с дополнительными параметрами используется расширенный формат. В расширенном формате каждая роль передается как список из словарей со спецификацией роли и дополнительных параметров.

```
{
  "code": 0,
  "users": [
    {
      "login": "login 1",
      "roles": 
       [
            [{"group": "admin"}, {"passport-login": "yndx.art.admin"}],
            [{"group": "manager"}, {"passport-login": "yndx.art.manager"}],
       ]
    },
       {
      "login": "login 2",
      "roles": 
       [
            [{"group": "admin"}, {"passport-login": "yndx.art.admin"}],
            [{"group": "manager"}, {"passport-login": "yndx.art.manager"}],
       ]
    },
    …
  ],
  "groups": [
     {
       "group": 777,
       "roles": <список ролей группы>
     },
     {
       "group": 179,
       "roles": <список ролей группы>
     }
  ]
}
```

{% endcut %}

{% cut "Пример ответа с простым списком ролей" %}


Для передачи простого списка ролей используется краткий формат.

```
{
  "code": 0,
  "users": [
{
  "login": "login 1",
  "roles":
  [
    {"group": "admin"},
    {"group": "manager"},
  ]
}
]
}
```

{% endcut %}
