# Метод editAccount

Изменяет некоторые параметры аккаунта.

## Синтаксис запроса {#id1FEB4602}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<account>
  & op=<edit>
  & uid=<id>
  & ([passwd=<visible>] | [cryptpasswd=<crypted>])
  & [enabled=<0|1>]
  & [city=<string>]
  & [country=<string>]
  & [email=<string>]
  & [fname=<last_name>]
  & [iname=<first_name>]
  & [hintq=<question>]
  & [hinta=<answer>]
  & [nickname=<string>]
  & [sex=<0|1|2>]
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### op
*Обязательный параметр*
#### uid
*Обязательный параметр*

{% include [accountdef-uid_d](../_includes/api/accountdef/id-accountdef/uid_d.md) %}

#### passwd

{% include [addaccount-password_d](../_includes/api/addaccount/id-addaccount/password_d.md) %}


При смене пароля слабые пароли не принимаются.

#### cryptpasswd

{% include [accountdef-passwd_d](../_includes/api/accountdef/id-accountdef/passwd_d.md) %}


{% include [addaccount-cryptpassword_d](../_includes/api/addaccount/id-addaccount/cryptpassword_d.md) %}

#### enabled

{% include [accountdef-enabled_d](../_includes/api/accountdef/id-accountdef/enabled_d.md) %}

#### city

{% include [accountdef-city_d](../_includes/api/accountdef/id-accountdef/city_d.md) %}

#### country

{% include [accountdef-country_d](../_includes/api/accountdef/id-accountdef/country_d.md) %}

#### email

{% include [accountdef-email_d](../_includes/api/accountdef/id-accountdef/email_d.md) %}

#### fname

{% include [accountdef-fname_d](../_includes/api/accountdef/id-accountdef/fname_d.md) %}

#### iname

{% include [accountdef-iname_d](../_includes/api/accountdef/id-accountdef/iname_d.md) %}

#### hintq

{% include [accountdef-hintq_d](../_includes/api/accountdef/id-accountdef/hintq_d.md) %}

#### hinta

{% include [accountdef-hinta_d](../_includes/api/accountdef/id-accountdef/hinta_d.md) %}

#### nickname

{% include [accountdef-nickname_d](../_includes/api/accountdef/id-accountdef/nickname_d.md) %}

#### sex

{% include [accountdef-sex_d](../_includes/api/accountdef/id-accountdef/sex_d.md) %}


С помощью метода можно изменить только те параметры аккаунта, которым соответствуют какие-либо из приведенных параметров запроса. Полный список параметров аккаунта приведен в разделе [Спецификация ответов об аккаунтах](accountdef.md).

> # Пример
> `http://passport-internal.yandex.ru/passport`
> `/?mode=mdapi&target=account&op=edit&uid=1130000000000002&cryptpasswd=$1$WfOUpN3u$BB1EL6ozXUUnExDQWln4w1`
> Запрос меняет пароль. Ответом является XML-структура с новыми параметрами аккаунта.

## Формат ответа {#id1862229D}

Ответом является XML-структура с параметрами аккаунта.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors> </errors>
  <list>
    <account>
      <aliases> </aliases>
      <birth_date></birth_date>
      <city></city>
      <country></country>
      <domain>okna.ru</domain>
      <domain_id>1</domain_id>
      <email></email>
      <enabled>1</enabled>
      <fio> </fio>
      <fname></fname>
      <glogout>1</glogout>
      <hinta></hinta>
      <hintq></hintq>
      <iname></iname>
      <karma>0</karma>
      <karma_dead_time>0</karma_dead_time>
      <login>petrov.petr@okna.ru</login>
      <login_wanted>petrov.petr@okna.ru</login_wanted>
      <nickname></nickname>
      <passwd>$1$/l4X7BAs$wbF4ox4Wae/Am01x5wsbx.</passwd>
      <regdate>2010-09-16 15:21:07</regdate>
      <sex></sex>
      <signed_eula>0</signed_eula>
      <uid>1130000000000739</uid>
    </account>
  </list>
  <target>account</target>
</mdapi>
```

Описание элементов ответа приведено в разделе [Спецификация ответов об аккаунтах](accountdef.md).

## Сообщения об ошибках {#section_qs5_nhk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>Field error:no-uid</error>
  </errors>
  <operation>edit</operation>
  <target>account</target>
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
Для метода [editAccount](editaccount.md) также предусмотрены следующие сообщения:
* `update accinfo crashed` — ошибка изменения параметров аккаунта;
* `change account log error` — не удалось сделать запись об изменении параметров аккаунта в журнал логирования;
* `update passwd crached` — ошибка изменения пароля на стороне Паспорта;
* `change pass log error` — не удалось сделать запись об изменении пароля в журнал логирования;
* `update access crached` — ошибка изменения одного из параметров: `enabled`, `karma`, `karma_dead_time`, `glogout`;
* `change access log error` — не удалось сделать запись в журнал логирования об изменении одного из параметров: `enabled`, `karma`, `karma_dead_time`, `glogout`.