# Метод listHost

Возвращает данные о всех почтовых базах или о конкретной почтовой базе.

## Синтаксис запроса {#id1FD12F2C}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<host>
  & [op=<list>]
  & [host_id=<id>]
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### op
#### host_id

{% include [hostdef-host_id_p](../_includes/api/hostdef/id-hostdef/host_id_p.md) %}


Если не указан или задан неверный идентификатор, выводится список всех баз с параметрами.

Аргумент `op` может быть опущен, что подразумевает `op = list`.

> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?host_id=18`
> Запрос возвращает данные о почтовой базе с идентификатором 18.

## Формат ответа {#id0068AD8B}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <count>1</count>
  <errors> </errors>
  <found>1</found>
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
  <operation>list</operation>
  <start>0</start>
  <target>host</target>
</mdapi>
```

Описание элементов ответа приведено в разделе [Спецификация ответов об аккаунтах](accountdef.md).

## Сообщения об ошибках {#section_lgx_jwj_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>SearchCrashed</error>
  </errors>
  <operation>list</operation>
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
Для метода [listHost](listhost.md) также предусмотрены следующие сообщения:
* `SearchCrashed` — ошибка поиска на стороне Паспорта.

{% note info %}

Если в запросе указан неверный идентификатор почтовой базы, ошибка не возникает, но выводится список всех баз.

{% endnote %}


