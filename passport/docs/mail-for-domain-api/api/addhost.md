# Метод addHost

Создает объект host, соответствующий почтовой базе.

{% note warning %}

В Паспорте должна быть зарегистрирована по меньшей мере одна почтовая база с приоритетом больше 100 (аргумент `prio`). В противном случае Паспорт не будет связывать новые аккаунты с почтовыми базами, в результате чего письма не будут доставляться в почтовые ящики этих аккаунтов.

{% endnote %}


## Синтаксис запроса {#id1FCEF819}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<host>
  & op=<add>
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
> `?op=add&sid=2&db_id=mdb201&mx=mxc10.yandex.ru&prio=101`
> Запрос регистрирует почтовую базу с именем `mdb201` и назначает ей приоритет 101.

## Формат ответа {#id00683108}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors> </errors>
  <host_id>18</host_id>2
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

В элементе `host_id` возвращается идентификатор почтовой базы, присвоенный Паспортом. Идентификатор используется для запроса или редактирования сведений о базе.

Описание других элементов ответа приведено в разделе [Спецификация ответов о почтовых базах](hostdef.md).

## Сообщения об ошибках {#section_o52_pwj_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`, а так же наличие элемента `staus` (как написано) со значением "error". Эти элементы могут присутствовать в ответе независимо друг от друга.

Ниже показаны примеры сообщений об ошибке. В первом примере об ошибке говорит элемент `error` внутри элемента `errors`, во втором — элемент `staus` со значением `error`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>Field error:err-prio</error>
  </errors>
  <operation>add</operation>
  <target>host</target>
</mdapi>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
  </errors>
  <operation>add</operation>
  <staus>error</staus>
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

#### staus
	
Наличие элемента `staus` (как написано) со значением 'error' говорит об ошибке на стороне Паспорта. Причина ошибки не уточнятся.
