# Метод deleteDomain

Удаляет объект domain, в результате чего домен отключается от Почты.

Объект domain можно удалить, только если с ним не связаны аккаунты.

## Синтаксис запроса {#id1FD736A1}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<domain>
  & op=<delete>
  & (domain_id=<id> | domain=<name>)
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

#### domain
*Обязательный параметр*

Имя домена.

{% note warning %}

Если у домена имеются синонимы, они также удаляются.

{% endnote %}


> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=domain&op=delete&domain=okna.ru`
> Запрос отключает от Почты домен с именем `okna.ru`.

## Формат ответа {#id00670A0D}

При успешном удалении возвращается XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors> </errors>
  <result>ok</result>
  <target>domain</target>
</mdapi>
```

## Сообщения об ошибках {#section_h41_kgk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>bad-domain</error>
  </errors>
  <target>domain</target>
</mdapi>
```

#### errors	

Содержит элементы `error`, если при выполнении запроса возникли ошибки. В ответе всегда присутствует элемент `errors`, даже если ошибок не было.

#### error	

Сообщение об ошибке. Ниже перечислены сообщения, общие для всех методов:

* `Field error:err-<name>` — в запросе указан аргумент `<name>` с некорректным форматом значения;
* `Field error:no-<name>` — в запросе отсутствует требуемый аргумент `<name>`;
* `Access denied` — запрашивающая сторона не обладает полномочиями на выполнение запроса;
* `NoTraget` (как написано) — в запросе не указан аргумент `target`;
* `BadTraget` (как написано) — аргумент `target` имеет недопустимое значение;
* `BadOperation` — аргумент `op` имеет недопустимое значение;
* `internal` — ошибка на стороне Паспорта, причина ошибки не уточняется.
Для метода [deleteDomain](deletedomain.md) также предусмотрены следующие сообщения:
* `bad-domain` — указан несуществующий идентификатор домена;
* `has-user` — домен не может быть удален из-за наличия аккаунтов (необходимо предварительно удалить аккаунты методом [deleteAccount](deleteaccount.md));
* `delete-error` — прочие ошибки удаления.