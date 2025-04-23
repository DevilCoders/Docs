# admchangereg

В режиме `admchangereg` Паспорт изменяет данные учетной записи. Данные, которые можно изменить, соответствуют поддерживаемым параметрам режима. Пользовательский интерфейс управления данными учетной записи реализован в рамках режима [changereg](changereg.md).

{% note alert %}

Режим `admchangereg` устарел. Команда Паспорта рекомендует использовать запрос нового API, предназначенный для [изменения персональных данных](https://wiki.yandex-team.ru/passport/python/api/bundle/changeaccount#izmenitpersonalnyedannye).

{% endnote %}


{% include [admsubscribe-grant](../_includes/reference/admsubscribe/id-admsubscribe/grant.md) %}



## Формат запроса {#request}

{% include [request-http-get](../_includes/reference/register/id-request/http-get.md) %}


```httpget
http://passport-internal.yandex.ru/passport?
mode=admchangereg
& uid=<UID>
& sid=<SID сервиса> |
  from=<короткое название сервиса>
[& timezone=<часовой пояс>]
[& birth_date=<дата>]
[& sex=0 | 1 | 2]
[& iname=<имя>]
[& fname=<фамилия>]
[& lang=<идентификатор языка>]
[& display_name=<отображаемое имя>]
[& profile_id=<идентификатор социального профиля>]
[& provider=<код провайдера профиля>]
```

#|
||**Параметр**|**Значение**|**Описание**||
||**Обязательные параметры**| | ||
||`mode`|admchangereg|
Название вызываемого режима.

{% note alert %}

Параметр не должен передаваться в теле запроса.

{% endnote %}||
||`uid`|<UID пользователя>|
Идентификатор пользователя в системе авторизации.||
||**Взаимоизаменяющие обязательные параметры**| | ||
||`sid`|<SID сервиса>|
Идентификатор сервиса, вызывающего режим `admchangereg`.||
||`from`|<короткое название сервиса>|
Короткое название сервиса, вызывающего режим `admchangereg`. Параметр `from` игнорируется, если в запросе указан параметр `sid`.

Короткое название присваивается сервису при создании SID.||
||**Дополнительные параметры**| | ||
||`timezone`{#timezone}|<часовой пояс>|
Часовой пояс пользователя.

Значение должно быть в формате tz database, например: «Australia/Adelaide». В вики размещен [список часовых поясов](http://wiki.yandex-team.ru/MixailNikitin/timezones) в двух форматах: с разделителем «;;» и для tt2.||
||`birth_date`|<дата>|
Новая дата рождения пользователя, в формате ГГГГ-ММ-ДД.||
||`sex`{#sex}|<0 \| 1 \| 2>|
Новый пол пользователя.

Используемые значения:

- 0 — пол не указан;
- 1 — мужской;
- 2 — женский.||
||`iname`|<имя>|
Новое имя пользователя.||
||`fname`|<фамилия>|
Новая фамилия пользователя.||
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
||`display_name`{#display-name}|<отображаемое имя>|
Новое имя пользователя для отображения в интерфейсе (например, в шапке сервиса или в подписи к комментариям).

Вместе с отображаемым именем необходимо указать источник имени: идентификатор социального профиля (параметр [profile_id](#profile-id)) и код провайдера профиля (параметр [provider](#provider)).||
||`profile_id`{#profile-id}|<идентификатор социального профиля>|
Идентификатор социального профиля, из которого получено отображаемое имя.

Обязателен, если в запросе передан параметр [display_name](#display-name).||
||`provider`{#provider}|<код провайдера профиля>|
Двухбуквенный код провайдера социального профиля, указанного в значении параметра [profile_id](#profile-id). Поддерживаемые провайдеры перечислены в вики: [http://wiki.yandex-team.ru/social/providers](http://wiki.yandex-team.ru/social/providers).

Обязателен, если в запросе передан параметр [display_name](#display-name).||
|#

## Формат ответа {#response}

### Данные учетной записи изменены {#success}

{% include [response-result-ok](../_includes/reference/admkarma/id-response/result-ok.md) %}


Ответ содержит все измененные данные учетной записи (каждый XML-элемент соответствует одноименному параметру запроса).

Пример ответа:

```
<result status="ok">
  <uid>11806412</uid>
  <sid>2</sid>
  <birth_date>1990-12-12</birth_date>
  <timezone>Europe/Moscow</timezone>
  <sex>1</sex>
  <iname>Вася</iname>
  <fname>Пупкин</fname>
  <lang>kk</lang>
  <display_name>Суровый Мститель</display_name>
  <profile_id>1293124</profile_id>
  <provider>vk</provider>
</result>
```

### Произошла ошибка {#error}

{% include [response-result-error](../_includes/reference/admkarma/id-response/result-error.md) %}


Пример ответа:

```
<result status="error">
  <error>nofield</error>
  <text>Some of required fields not specified</text>
</result>
```

Элементы ответа:

- **error**
  Код возникшей ошибки.
- **text**
  Описание ошибки.

{% include [response-error-table](../_includes/reference/changelang/id-response/error-table.md) %}

#|
||**error**|**Комментарий**||
||nofield|Не указан один из обязательных параметров.||
||unknownuid|Пользователь с указанным UID не найден.||
||badtimezone|Недопустимое значение параметра [timezone](#timezone).||
||badlang|Недопустимое значение параметра [lang](#lang).||
||badsex|Недопустимое значение параметра [sex](#sex).||
||baddisplayname|
Ошибка в одном из параметров, характеризующих отображаемое имя:

- [display_name](#display-name),
- [profile_id](#profile-id),
- или [provider](#provider)||
|#

