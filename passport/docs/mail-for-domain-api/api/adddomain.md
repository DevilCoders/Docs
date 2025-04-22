# Метод addDomain

Создает объект domain, соответствующий подключенному к Почте домену.

## Синтаксис запроса {#id1FD3ABD5}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & taget=<domain>
  & op=<add>
  & domain=<URI>
  & admin=<uid>
  & [enabled=<0|1>]
  & [mx=<0|1>]
```
### Параметры
#### mode
*Обязательный параметр*
#### taget
*Обязательный параметр*
#### op
*Обязательный параметр*
#### domain
*Обязательный параметр*

Имя домена, подключаемого к Почте, например `okna.ru`.

#### admin

*Обязательный параметр*

{% include [domaindef-admin_d](../_includes/api/domaindef/id-domaindef/admin_d.md) %}

#### enabled

{% include [domaindef-enabled_d](../_includes/api/domaindef/id-domaindef/enabled_d.md) %}


Если аргумент не указан, домен регистрируется с `enabled` = 0.
#### mx

{% include [domaindef-mx_d](../_includes/api/domaindef/id-domaindef/mx_d.md) %}


> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=domain&op=add&domain=okna.ru&admin=2862460951282306185`
> Запрос подключает домен `okna.ru` и назначает администратора почты.

## Формат ответа {#section_fy3_5fk_bbb}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <domain_id>43</domain_id>
  <errors> </errors>
  <list>
    <domain>
      <admin>2862460951282306185</admin>
      <aliases> </aliases>
      <born_date>2010-09-14 10:27:56</born_date>
      <default_uid>0</default_uid>
      <domain>okna.ru</domain>
      <domain_id>43</domain_id>
      <enabled>0</enabled>
      <master_domain></master_domain>
      <mx>0</mx>
      <options>
        <can_users_change_password>1</can_users_change_password>
      </options>
    </domain>
  </list>
  <operation>add</operation>
  <status>ok</status>
  <target>domain</target>
</mdapi>
```

В элементе `domain_id` содержится идентификатор домена, присвоенный Паспортом. Идентификатор используется для запроса или редактирования сведений о домене.

Описание других элементов ответа приведено в разделе [Спецификация ответов о доменах](domaindef.md).

## Сообщения об ошибках {#section_gy3_5fk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`, а так же наличие элемента `staus` (как написано) со значением "error". Эти элементы могут присутствовать в ответе независимо друг от друга.

Ниже показаны примеры сообщений об ошибке. В первом примере об ошибке говорит элемент `error` внутри элемента `errors`, во втором — элемент `staus` со значением `error`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>Field error:no-domain</error>
  </errors>
  <operation>add</operation>
  <target>domain</target>
</mdapi>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
  </errors>
  <operation>add</operation>
  <staus>error</staus>
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

#### staus
	
Наличие элемента `staus` (как написано) со значением 'error' говорит об ошибке на стороне Паспорта. Причина ошибки не уточнятся.