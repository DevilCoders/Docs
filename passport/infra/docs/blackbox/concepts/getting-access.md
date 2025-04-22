# Получение доступа к Черному ящику

Черный ящик имеет два уровня защиты от несанкционированного доступа. Чтобы получить доступ к ЧЯ, необходимы разрешения для каждого из уровней:

- [сетевой экран ("дырки")](#section_puncher).

- [список разрешений (грантов), выданных потребителям (Access Control List, ACL)](#section_grants).


ЧЯ не отправляет ответы на запросы сервисов, не имеющих доступа через сетевой экран.

Попытка выполнить метод или получить значения поля, доступ к которому явно не разрешен через гранты, вызывает ошибку. Описание ошибки возвращается в ответе Черного ящика (см. раздел [Ошибки обращения к Черному ящику](../concepts/blackboxErrors.md)).

Пример: компьютер, для которого разрешена только проверка пар логин/пароль, также запрашивает значение какого-либо поля БД. В ответе на такой запрос возвращается только описание ошибки доступа, переданная пара логин/пароль не проверяется.

## Получение доступов через сетевой экран {#section_puncher}

Чтобы запросить дырку, создайте [заявку в Puncher](https://puncher.yandex-team.ru/). Параметры заявки:

- **Источник** — сетевой макрос вашего сервиса, например `_MAILNETS_`.
- **Назначение** — необходимое вам [окружение ЧЯ](../concepts/location.md), например, `blackbox.yandex-team.ru`.
- **Протокол** — TCP.
- **Порт** — `80`, `443`.
- **Действует до** — вечная.
- **Комментарий на создание или удаление правила** — причина запроса доступа, например <q>Почта ходит в ЧЯ проверять авторизацию пользователей</q>.

## Получение грантов {#section_grants}

Каждый грант — это разрешение, выданное вашему сервису. В общем случае доступ к боевому Черному ящику предоставляется только боевым серверам сервисов. Гранты для тестового Черного ящика выданы почти всем сетям Яндекса.

Различают гранты:

- [с TVM](#tvm-grants);
- [без TVM](#network-grants).

### Гранты для TVM-приложений и хостов {#tvm-grants}

При использовании грантов с TVM, в заголовках каждого запроса к ЧЯ передается [Service-тикет](https://wiki.yandex-team.ru/passport/tvm2/stbrief). Данный способ является рекомендуемым и [наиболее безопасным](https://wiki.yandex-team.ru/passport/tvm2/#obshheeopisanietvm2.0).

Чтобы получить гранты с TVM:

1. [Зарегистрируйте](https://wiki.yandex-team.ru/passport/tvm2/stbrief/#kakmozhnopoluchitidentifikatorservisadljatiketov) новое TVM-приложение для вашего сервиса.

1. Заполните [форму запроса грантов](https://forms.yandex-team.ru/surveys/4901/).


Чтобы подписать запросы Service-тикетами:

1. Выписывайте Service-тикеты при помощи [TVM API](https://wiki.yandex-team.ru/passport/tvm2/api/).

    При запросе Service-тикета, в параметре `src` указывайте идентификатор вашего TVM-приложения, а в параметре `dst` — идентификатор необходимого вам [окружения ЧЯ](../concepts/location.md). Идентификаторы для окружений ЧЯ приведены в [таблице](#okruzheniya).

1. Передавайте полученные тикеты в заголовке `X-Ya-Service-Ticket` всех запросов к ЧЯ.

#### Окружения

Окружение | Enum в libtvmauth/tvmtool | tvmid | Хосты
----- | ----- | ----- | -----
Prod | Prod / PROD | 222 | blackbox.yandex.net<br/>blackbox-rc.yandex.net<br/>blackbox-mail.yandex.net
Mimino | Prod / PROD | 239 | blackbox-mimino.yandex.net
Test | Test / TEST | 224 | blackbox-test.yandex.net
ProdYateam | ProdYateam / PROD_YATEAM | 223 | blackbox.yandex-team.ru
TestYateam | TestYateam / TEST_YATEAM | 225 | blackbox-test.yandex-team.ru
Stress | Stress / STRESS | 226 | blackbox-stress.yandex.net<br/>pass-stress-i1.sezam.yandex.net<br/>pass-stress-m1.sezam.yandex.net<br/>pass-stress-s1.sezam.yandex.net

### Гранты для хостов {#network-grants}

При использовании данного способа доступ выдается для отдельных хостов, сетевых макросов или кондукторных групп. Проверки TVM-тикета не происходит.

Чтобы получить гранты без TVM, заполните [форму запроса грантов](https://forms.yandex-team.ru/surveys/4901/). В поле **ID (номер) приложения в TVM** поставьте прочерк (`-`), а в поле **Комментарий** укажите причину, почему вашему сервису не подходят гранты с TVM-тикетами.

{% note alert %}

Гранты без TVM в настоящий момент выдаются только в виде исключения после отдельного одобрения СИБ.

{% endnote %}

## Проверка грантов через API

### Зачем
Часто бывает так, что нужно на старте сервиса проверить, есть ли все необходимые гранты. Т.е. до того, как на инстанс сервиса польётся боевой трафик

Например.
В коде какого-нибудь сервиса уже есть запрос в blackbox - в проде всё корректно работает. В очередной релиз попадает патч, где в запрос добавили новые параметры или атрибуты, которые требуют гранта. Нужные гранты заказали для дева/тестинга, а для прода - забыли. Релиз выкатывается, запросы в blackbox начинают падать с ошибкой ACCESS_DENIED - при этом на пол проливается продный трафик.

Чтобы не проливать запросы пользователей, можно на старте сделать запрос в blackbox и проверить наличие грантов.

### Ручка /blackbox/check_grants

В эту ручку можно перенаправить ваш обычный запрос в blackbox. API вернет код 200, если запрос составлен корректно, и имеются все необходимые гранты для его выполения. Иначе - код 4XX с описанием проблемы в теле ответа.

Надо:
1) взять свой код, который обычно генерирует запросы в blackbox, и в пользовательские данные (куки, токены, uid, userip, host и тд) подставить пустые значения.
2) отправить запрос не в `blackbox.yandex.net/blackbox`(например), а в `blackbox.yandex.net/blackbox/check_grants`
3) по коду ответа понять, можно ли наливать нагрузку на этот инстанс сервиса или нет

На текущий момент выглядит так, что сервису не надо смотреть в тело ответа, если код 4XX: надо записать в лог или кинуть исключение со всем ответом. Надо идти править запрос/конфиги/гранты.

Например:
  * `method=userinfo&login=&attributes=1,2,3,4,5&get_user_ticket=yes`
  * `method=sessionid&sessionid=&attributes=1,2,3,4,5&get_family_info=yes`

{% cut "Для использования ручки не требуется никаких грантов." %}

Т.е. можно руками собрать запрос в `blackbox-test.yandex.net/blackbox/check_grants`, добавить в запрос заголовок `X-Ya-Service-Ticket: kek` и по телу ошибки понять, что вообще нужно заказывать для такого запроса.
Например
```
$  curl -v 'http://blackbox-test.yandex.net/blackbox/check_grants?method=login&password=&attributes=26,27,28,29&login=' -H 'X-Ya-Service-Ticket: kek'
...
< HTTP/1.1 403 Forbidden
...
<
<?xml version="1.0" encoding="UTF-8"?>
<doc>
<grants_status>ACCESS_DENIED</grants_status>
<description>Missing some grants for consumer: _unknown_ (tvm_id=NULL;IP=2a02:6b8:c02:500:8000:611:0:1d). request_id=6affdfb558f11a59. ext=Please request grants here: https://forms.yandex-team.ru/surveys/4901 . If you are sure you have grants, please mail to passport-admin@yandex-team.ru. method=login. host=. hostname=. current_time=2020-08-31T14:59:23.431894+0300</description>
<check_grants_errors>
<error>failed to check service ticket: Malformed ticket. status=malformed;: &apos;kek&apos;</error>
<error>no grants for attribute &apos;26&apos;</error>
<error>no grants for attribute &apos;27&apos;</error>
<error>no grants for attribute &apos;28&apos;</error>
<error>no grants for attribute &apos;29&apos;</error>
<error>no grants for method=login</error>
</check_grants_errors>
</doc>
```
{% endcut %}

### Формат ответа

Коды ответа:
  * 200 - ок
    Пример ответа:
```xml
<doc>
<grants_status>OK</gants_status>"
</doc>
```
```json
{"grants_status":"OK"}
```
  * 400 - невалидный запрос
    Пример ответа:
```xml
<doc>
<grants_status>INVALID_PARAMS</grants_status>
<description>Unrecognized method: &apos;&apos;. request_id=...</description>
<check_grants_errors/>
</doc>
```
```json
{
  "grants_status": "INVALID_PARAMS",
  "description": "Unrecognized method: ''. request_id=...",
  "check_grants_errors": []
}
```
  * 403 - не хватает грантов
    Пример ответа:
```xml
<doc>
<grants_status>ACCESS_DENIED</grants_status>
<description>Missing some grants for consumer: _unknown_ (tvm_id=NULL;IP=2a02:6b8:c02:500:8000:611:0:1d). request_id=...</description>
<check_grants_errors>
<error>failed to check service ticket: Malformed ticket. status=malformed;: &apos;kek&apos;</error>
<error>no grants for attribute &apos;26&apos;</error>
<error>no grants for attribute &apos;27&apos;</error>
<error>no grants for attribute &apos;28&apos;</error>
<error>no grants for attribute &apos;29&apos;</error>
<error>no grants for method=login</error>
</check_grants_errors>
</doc>
```
```json
{
  "grants_status": "ACCESS_DENIED",
  "description": "Missing some grants for consumer: _unknown_ (tvm_id=NULL;IP=2a02:6b8:c02:500:8000:611:0:1d). request_id=...",
  "check_grants_errors": [
    "failed to check service ticket: Malformed ticket. status=malformed;: kek",
    "no grants for attribute 26",
    "no grants for attribute 27",
    "no grants for attribute 28",
    "no grants for attribute 29",
    "no grants for method=login"
  ]
}
```
