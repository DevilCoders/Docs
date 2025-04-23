# Метод deleteAlias

Удаляет синоним аккаунта.

## Синтаксис запроса {#id1FF1D3BE}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<account>
  & op=<deletealias>
  & uid=<id>
  & alias=<username>
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

Уникальный идентификатор пользователя.
#### alias
*Обязательный параметр*

Удаляемый синоним.

> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=account&op=deletealias&uid=1130000000000742&alias=petr`
> Запрос удаляет синоним `petr` у аккаунта 1130000000000742.

## Формат ответа {#section_jgw_5hk_bbb}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors> </errors>
  <operation>deletealias</operation>
  <result>ok</result>
  <target>account</target>
</mdapi>
```

## Сообщения об ошибках {#section_kgw_5hk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>requesting account info failed</error>
  </errors>
  <operation>deletealias</operation>
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
Для метода [deleteAalias](deletealias.md) также предусмотрены следующие сообщения об ошибках:
* `account info requesting failed` — не найден аккаунт или произошла внутренняя ошибка во время поиска;
* `alias deleting failed` — произошла ошибка во время удаления синонима;
* `alias not found` — указанный синоним не найден;
* `change account log error` — не удалось сделать запись об изменении аккаунта в журнал логирования.