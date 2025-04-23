# Метод editHost

Изменяет параметры почтовой базы.

Можно изменять любые параметры почтовых баз, кроме автоматически присвоенного идентификатора.

## Синтаксис запроса {#id1FD277BA}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<host>
  & op=<edit>
  & [host_id=<id>]
  & [db_id=<post_db_id>]
  & [prio=<N>]
  & [sid=<2>]
  & [host_ip=<IP>]
  & [host_name=<name>]
  & [host_number=<N>]
  & [mx=<dns-mx>]
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### op
*Обязательный параметр*
#### host_id

{% include [hostdef-host_id_p](../_includes/api/hostdef/id-hostdef/host_id_p.md) %}

#### db_id

{% include [hostdef-db_id_p](../_includes/api/hostdef/id-hostdef/db_id_p.md) %}

#### prio

{% include [hostdef-prio_p](../_includes/api/hostdef/id-hostdef/prio_p.md) %}

#### sid

{% include [hostdef-sid_p](../_includes/api/hostdef/id-hostdef/sid_p.md) %}

#### host_ip

{% include [hostdef-host_ip_p](../_includes/api/hostdef/id-hostdef/host_ip_p.md) %}

#### host_name

{% include [hostdef-host_name_p](../_includes/api/hostdef/id-hostdef/host_name_p.md) %}

#### host_number

{% include [hostdef-host_number_p](../_includes/api/hostdef/id-hostdef/host_number_p.md) %}

#### mx

{% include [hostdef-mx_p](../_includes/api/hostdef/id-hostdef/mx_p.md) %}


> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?op=edit&host_id=18&prio=120`
> Запрос устанавливает приоритет 120 для почтовой базы с идентификатором 18.

## Формат ответа {#id006968CD}

Ответом является XML-структура с новыми параметрами почтовой базы.

```xml
<mdapi>
  <errors> </errors>
  <host_id>18</host_id>
  <list>
    <host>
      <db_id>mdb201</db_id>
      <host_id>18</host_id>
      <host_ip></host_ip>
      <host_name></host_name>
      <host_number>0</host_number>
      <mx>mxc10.yandex.ru</mx>
      <prio>101</prio>
      <sid>2</sid>
    </host>
  </list>
  <operation>add</operation>
  <status>ok</status>
  <target>host</target>
</mdapi>
```

Описание элементов ответа приведено в разделе [Спецификация ответов о почтовых базах](hostdef.md).

## Сообщения об ошибках {#section_lxk_hwj_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`, а так же наличие элемента `status` со значением `error`. Эти элементы могут присутствовать в ответе независимо друг от друга.

Ниже показаны примеры сообщений об ошибке. В первом примере об ошибке говорит элемент `error` внутри элемента `errors`, во втором — элемент `status` со значением `error`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>Field error:err-prio</error>
  </errors>
  <operation>edit</operation>
  <target>host</target>
</mdapi>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
  </errors>
  <operation>edit</operation>
  <status>error</status>
  <target>host</target>
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

#### status 

Cодержит значение 'ok', если запрос выполнен без ошибок, или 'error' если произошла ошибка.
