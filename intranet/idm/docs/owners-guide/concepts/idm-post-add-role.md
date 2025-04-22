# Добавление роли (add-role)

Добавляет роль в БД.

Запрос необходимо отправлять по протоколу HTTPS c помощью метода POST. Данные о роли необходимо передавать в теле запроса в формате URL-encoded c заголовоком `application/x-www-form-urlencoded`.

## Синтаксис запроса {#section_yq2_k1k_wcb}

```
POST /add-role/
```

#|
||Поле | Описание | Тип данных ||
|| `login` | Логин пользователя со [Стаффа](https://staff-api.yandex-team.ru/v3/). | Строка ||
|| `role` | Спецификация роли в одной из форм: 

- Словарь — основная спецификация роли. Содержит пару «ключ-значение». Ключом является строка, указанная в поле [`slug`](glossary,md#slug) в запросе [get-info](idm-get-info.md).
    Например, `{"group": "moderator"}` или `{"project": "subs", "role": "manager"}`.
    
- Slug path — спецификация роли в виде строки.
    Например, «/group/moderator/» или «/project/subs/role/manager/».
    
- Value path — спецификация роли в виде строки по полю [`values`](glossary.md#values).
    Например, «/moderator/» или «/subs/manager/». 
	
| Массив ||
|| `path` | Спецификация роли через путь узла в дереве ролей. 
Узел дерева ролей представлен в виде строки, в которой каждый элемент передается из поля [`slug`](glossary.md#slug) в запросе [get-info](idm-get-info.md).

Например, спецификации в виде словаря `{"project": "subs", "role": "manager"}` соответствует путь «/project/subs/role/manager/».

Используется при синхронизации данных для [потоковой выдачи ролей](idm-get-roles.md). | Массив ||
|| `fields` | Дополнительные данные о роли. Подробнее см. раздел [Информация о системе и ролях](idm-get-info.md). | Массив||
|| `group` | Идентификатор (id) группы на [Стаффе](https://staff-api.yandex-team.ru/v3/) (только для систем [group-aware](glossary.md#group-aware)). | Число ||
|#

## Формат ответа {#section_ar2_k1k_wcb}

При успешном выполнении запроса возвращается ответ cо статусом "ok" и кодом 0. Если ответ содержит другой код, доступ не добавлен. Подробнее см. раздел [Возвращаемые результаты](errors.md).

```
{
  "code": 0
  "status": "ok"
}
```

Если в системе используются дополнительные поля, их значения необходимо передавать в ключе `data`. Для передачи секретных данных используйте ключ `context`.
```
{
  "code": 0
  "status": "ok"
  "data": {"passport-login": "some-login"}
  "context": {"passport-password": "secret-password"}
}
```

## Примеры запросов {#section_sd3_fct_xcb}

#### Добавить роль пользователю в системе с простым списком узлов

```
POST /add-role/ HTTP/1.1
Host: {адрес запрашиваемого ресурса}
Content-Type: application/x-www-form-urlencoded

login=frodo&role={"project": "direct", "role": "manager"}&fields={"passport-login":"yndx.some.login", "another-field": "some-value"}
```

#### Выдать доступ для групповой роли

```
POST /add-role/ HTTP/1.1
Host: {адрес запрашиваемого ресурса}
Content-Type: application/x-www-form-urlencoded

group=777&role={"project": "direct", "role": "manager"}&fields={"another-field": "some-value"}
```

