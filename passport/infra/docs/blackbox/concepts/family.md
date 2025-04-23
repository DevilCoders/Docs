# Семьи

Узнать о принадлежности к семье можно в [method=sessionid](../methods/sessionid.md), [method=oauth](../methods/oauth.md), [method=userinfo](../methods/userinfo.md), [method=user_ticket](../methods/user_ticket.md) с помощью параметра [get_family_info=yes](../methods/sessionid.md#get_family_info).
В ответе появится [идентификатор семьи](../methods/sessionid.md#family_info-greaterfamily_id).

Получить информацию о составе семьи и о пользователях в семье можно в [method=family_info](../methods/family_info.md).

## Роли в семье

### Админ

Имеет право на все возможные изменения в семье.

Можно узнать в [method=family_info](../methods/family_info.md) или в прочих методах с помощью параметра [get_family_info=yes](../methods/sessionid.md#get_family_info).

### Управление детьми

Такое право имеют админ и участники семьи, явно получившие это право.

Знание про эту роль можно забрать из [атрибута 1034](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#db-attributes) - он учтёт все возможные факторы.

## Детские акаунты

Ключевое слово - `child`.

{% note warning %}

Не путать с детскими профилями - `kid`: это кастомное решение для Кинопоиска.

{% endnote %}

Опознать акаунт можно по наличию [атрибута](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#db-attributes) 210.
Ещё есть возрастные ограничения, которые могут помочь:
  * 202 - это ограничения общего характера
  * 1026 - возрастное ограничение по музыке (учитывает 202)
  * 1027 - возрастное ограничение по видео (учитывает 202)

Увидеть детей в составе семьи можно в  [method=family_info](../methods/family_info.md) с параметром [get_members_info=all|children](../methods/family_info.md#get_members_info).
