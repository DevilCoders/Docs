# Метод editDomain

Изменяет параметры домена.

## Синтаксис запроса {#id1FD50376}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<domain>
  & op=<edit>
  & domain_id=<id>
  & [admin=<uid>]
  & [default_uid=<uid>]
  & [default=<uid или логин>]
  & [enabled=<0|1>]
  & [mx=<0|1>]
  & [can_users_change_password=<0|1>]
  & [change_password_url=<URL>]
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### op
*Обязательный параметр*
#### domain_id
*Обязательный параметр*

{% include [domaindef-domain_id_d](../_includes/api/domaindef/id-domaindef/domain_id_d.md) %}

#### admin

{% include [domaindef-admin_d](../_includes/api/domaindef/id-domaindef/admin_d.md) %}

#### default_uid

{% include [domaindef-default_uid_d](../_includes/api/domaindef/id-domaindef/default_uid_d.md) %}

#### default

{% include [domaindef-default_d](../_includes/api/domaindef/id-domaindef/default_d.md) %}

#### enabled

{% include [domaindef-enabled_d](../_includes/api/domaindef/id-domaindef/enabled_d.md) %}

#### mx

{% include [domaindef-mx_d](../_includes/api/domaindef/id-domaindef/mx_d.md) %}

#### can_users_change_password

{% include [domaindef-can_users_change_password_d](../_includes/api/domaindef/id-domaindef/can_users_change_password_d.md) %}

#### change_password_url

{% include [domaindef-change_password_url_d](../_includes/api/domaindef/id-domaindef/change_password_url_d.md) %}


Невозможно изменить следующие параметры домена:

- `domain_id` — идентификатор домена;
- `domain` — имя домена;
- `born_date` — дата подключения домена к Почте;
- `aliases` — синонимы домена (для назначения синонимов служит метод [domainAlias](#domainAlias));
- `master_domain` — название основного домена (заполняется автоматически для доменов-синонимов — см. метод [domainAlias](#domainAlias)).

> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=domain&op=edit&mx=1&domain_id=44`
> Запрос меняет состояние параметра `mx` у домена с идентификатором 44.

## Формат ответа {#id0065C19F}

Ответом является XML-структура с новыми параметрами домена.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <domain_id>44</domain_id>
  <errors> </errors>
  <list>
    <domain>
      <admin>1130000000000383</admin>
      <aliases>
        <alias>ocna.ru</alias>
        <alias>windows.ru</alias>
      </aliases>
      <born_date>0000-00-00 00:00:00</born_date>
      <default_uid>1130000000000658</default_uid>
      <domain>okna.ru</domain>
      <domain_id>1</domain_id>
      <enabled>1</enabled>
      <master_domain></master_domain>
      <mx>1</mx>
      <options>
        <can_users_change_password>0</can_users_change_password>
        <change_password_url>http://rbc.ru/</change_password_url>
      </options>
    </domain>
    <domain>
  </list>
  <operation>list</operation>
  <status>ok</status>
  <target>domain</target>
</mdapi>
```

Описание элементов ответа приведено в разделе [Спецификация ответов о доменах](domaindef.md).

## Сообщения об ошибках {#section_skb_dgk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`, а так же наличие элемента `status` со значением `error`. Эти элементы могут присутствовать в ответе независимо друг от друга.

Ниже показаны примеры сообщений об ошибке. В первом примере об ошибке говорит элемент `error` внутри элемента `errors`, во втором — элемент `status` со значением `error`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>BadTraget</error>
  </errors>
  <operation>edit</operation>
  <target>domain</target>
</mdapi>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
  </errors>
  <operation>edit</operation>
  <status>error</status>
  <target>domain</target>
</mdapi>

```

#### errors	

Содержит элементы `error`, если при выполнении запроса возникли ошибки. В ответе всегда присутствует элемент errors, даже если ошибок не было.

#### error	

Сообщение об ошибке. Ниже перечислены сообщения, общие для всех методов:

* `Field error:err-<name>` — в запросе указан аргумент `<name>` с некорректным форматом значения;
* `Field error:no-<name>` — в запросе отсутствует требуемый аргумент `<name>`;
* `Access denied` — запрашивающая сторона не обладает полномочиями на выполнение запроса;
* `NoTraget` (как написано) — в запросе не указан аргумент `target`;
* `BadTraget` (как написано) — аргумент `target` имеет недопустимое значение;
* `BadOperation` — аргумент `op` имеет недопустимое значение;
* `internal` — ошибка на стороне Паспорта, причина ошибки не уточняется.
При попытке установить несуществующий аккаунт для неизвестных адресатов (catch-all) возвращается следующее сообщение об ошибке:
* `not found default_uid` — указан несуществующий `uid` в параметре `default_uid`.

#### status	

Содержит значение 'ok', если запрос выполнен без ошибок, или 'error' если произошла ошибка.
