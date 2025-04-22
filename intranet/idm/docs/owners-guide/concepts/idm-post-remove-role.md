# Удаление роли (remove-role)

Удаляет роль из БД.

Запрос необходимо отправлять по протоколу HTTPS c помощью метода POST. Данные о роли передаются в теле запроса в формате URL-encoded c заголовоком `application/x-www-form-urlencoded`.

## Синтаксис запроса {#section_thw_g1k_wcb}

```
POST /remove-role/
```

#|
|| **Поле** | **Описание** | **Тип данных** ||
||`login` | Логин пользователя со [Стаффа](https://staff-api.yandex-team.ru/v3/). | Строка||
||`role` | Спецификация роли в одной из форм: 
- Словарь — основная спецификация роли. Содержит пару «ключ-значение». Ключом является строка, указанная в поле [`slug`](glossary.md#slug) в запросе [get-info](idm-get-info.md).

    Например, `{"group": "moderator"}` или `{"project": "subs", "role": "manager"}`.
    
- Slug path — спецификация роли в виде строки.
    Например, «/group/moderator/» или «/project/subs/role/manager/».
    
- Value path — спецификация роли в виде строки по полю [`values`](glossary.md#values).
    Например, «/moderator/» или «/subs/manager/». | Массив ||
||`path` | Спецификация роли в формате пути узла в дереве ролей. 

{% include [idm-post-add-role-path-1](../_includes/concepts/idm-post-add-role/id-idm-post-add-role/path-1.md) %}


{% include [idm-post-add-role-path-2](../_includes/concepts/idm-post-add-role/id-idm-post-add-role/path-2.md) %}


{% include [idm-post-add-role-path-3](../_includes/concepts/idm-post-add-role/id-idm-post-add-role/path-3.md) %} 

| Массив||
||`fields` | Дополнительные данные о роли. Подробнее см. раздел [Информация о системе и ролях](idm-get-info.md). | Массив||
||`fired` | Параметр передается для уволенного пользователя. | Логическое||
||`group` | Идентификатор (id) группы на [Стаффе](https://staff-api.yandex-team.ru/v3/) (только для [систем group-aware](glossary.md#group-aware)). | Число||
||`deleted` | Параметр передается, если группа была удалена (только для [систем group-aware](glossary.md#group-aware)). Для существующих групп параметр не передается. | Логическое||
|#

## Формат ответа {#section_tvn_yl5_xcb}

При успешном выполнении запроса возвращается ответ cо статусом "ok" и кодом 0. Если ответ содержит другой код, доступ не удален. Подробнее см. раздел [Возвращаемые результаты](errors.md).

```
{
  "code": 0
  "status": "ok"
}
```

{% note info %}

Если у сотрудника уже удален доступ на момент выполнения запроса `/remove-role/`, то должен возвращаться ответ `{"code": 0}` или `{"code": 0, "warning": "У сотрудника уже нет такого доступа."}`.

{% endnote %}


## Примеры запросов {#section_axy_dct_xcb}

#### Отозвать доступ уволенного сотрудника

```
POST /remove-role/ HTTP/1.1
Host: {адрес запрашиваемого ресурса}
Content-Type: application/x-www-form-urlencoded

login=terran&role={"project": "direct", "role": "manager"}&fired=1
```

#### Отозвать доступ для групповой роли, если группа-владелец удалена

```
POST /remove-role/ HTTP/1.1
Host: {адрес запрашиваемого ресурса}
Content-Type: application/x-www-form-urlencoded

group=777&role={"project": "direct", "role": "manager"}&deleted=1&fields={"some_key": "some-value"}
```

#### Отозвать доступ у сотрудника

```
POST /remove-role/ HTTP/1.1
Host: {адрес запрашиваемого ресурса}
Content-Type: application/x-www-form-urlencoded

login=art&role={"project": "direct", "role": "manager"}&fields={"passport-login": "some-login"}

```

