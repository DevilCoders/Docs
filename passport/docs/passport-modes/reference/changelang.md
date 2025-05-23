# changelang

Изменяет значение поля [userinfo.lang](https://docs.yandex-team.ru/authdevguide/concepts/DB_About#userinfo) для пользователя, перенаправленного на режим. Если пользователь не авторизован, Паспорт предлагает ему авторизоваться в режиме [auth](auth.md).

Сервисы Яндекса используют поле `userinfo.lang`, чтобы определить предпочитаемый язык интерфейса для конкретного пользователя. Подробнее об определении языка интерфейса читайте в документе [Библиотека lang-detect. Руководство разработчика](https://doc.yandex-team.ru/lib/lang-detect/).


## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
https://passport.yandex.ru/passport?
mode=changelang
 & lang=<язык>
 & sk=<секретный ключ>
[& from=<короткое название сервиса>]
[& retpath=<URL>]
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Обязательные параметры**| | ||
||`mode`|changelang|
Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||`lang`{#lang}|<язык>|
Новый язык интерфейса.

Используемые значения:

- «az» — азербайджанский;
- «be» — белорусский;
- «en» — английский;
- «hy» — армянский;
- «ka» — грузинский;
- «kk» — казахский;
- «ro» — румынский (Молдавия);
- «ru» — русский;
- «tr» — турецкий;
- «tt» — татарский;
- «uk» — украинский.||
||`sk`|<секретный ключ>|
Ключ должен быть сгенерирован в следующем формате:

`u<сумма MD5 для строки UID::days>`, где

- `UID` — UID учетной записи, для которой изменяется язык;
- `days` — результат деления текущего UNIX-времени на 86400.

Пример ключа: `u5b6f847421b7d2c42902fbe8da4401d8`.||
||**Дополнительные параметры**| | ||
||`from`|<короткое название сервиса>|
Короткое название сервиса, который перенаправил пользователя на смену языка.

{% include [request-from-sid](../_includes/reference/register/id-request/from-sid.md) %}||
||`retpath`{#retpath}|\<URL\>|
Адрес, на который пользователя следует перенаправить после завершения работы режима. Должен указываться в формате URL-encoded.

Если параметр не указан, пользователь перенаправляется на режим [passport](passport.md).||
|#


## Формат ответа {#response}

Паспорт перенаправляет пользователя на адрес, указанный в значении параметра [retpath](#retpath). Если изменить язык не удалось, сообщение об ошибке будет передано в параметрах URL.

Используемые параметры:

- `error_mode` — принимает значение «changelang», обозначая источник ошибки.
- `error_id` — номер ошибки.
    
    Используемые ошибки описаны в таблице:
    
    #|
    ||**Номер ошибки**|**Комментарий**||
    ||0|Внутренняя ошибка Паспорта. Следует повторить запрос.||
    ||1|В запросе не указан язык (параметр [lang](#lang)).||
    ||2|Указано неизвестное значение параметра [lang](#lang).||
    ||3|Превышен лимит обращений к режиму для данной учетной записи.||
    |#
    

