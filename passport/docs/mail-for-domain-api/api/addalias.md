# Метод addAlias

Добавляет синоним аккаунта.

{% note info %}

Синонимы аккаунтов сочетаются с синонимами доменов (см. метод [domainAlias](domainalias.md)). Например, если у домена `okna.ru` имеется домен-синоним `windows.ru`, а у аккаунта `petrov.petr@okna.ru` есть синоним `petr`, то письма на адрес `petr@windows.ru` также будут поступать в почтовый ящик данного аккаунта.

{% endnote %}


## Синтаксис запроса {#id1FECD627}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<account>
  & op=<addalias>
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

Идентификатор пользователя.
#### alias
*Обязательный параметр*

Альтернативное имя пользователя в домене. Должно быть уникально в рамках домена.

> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=account&op=addalias&uid=1130000000000742&alias=petr`
> Запрос добавляет синоним `petr` аккаунту 1130000000000742.

## Формат ответа {#section_gmb_shk_bbb}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors> </errors>
  <operation>addalias</operation>
  <result>ok</result>
  <target>account</target>
</mdapi>
```

При запросе параметров аккаунта синонимы в сочетании с именем домена содержатся в элементах `aliase`, как показано ниже.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <count>1</count>
  <errors> </errors>
  <found>1</found>
  <list>
    <account>
      <aliases>
        <alias>petr@okna.ru</alias>
      </aliases>
      ...
```

## Сообщения об ошибках {#section_hmb_shk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>requesting account info failed</error>
  </errors>
  <operation>addalias</operation>
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
Для метода [addAalias](addalias.md) также предусмотрены следующие сообщения об ошибках:
* `requesting account info failed` — не найден аккаунт или произошла внутренняя ошибка во время поиска;
* `occupied` — на домене существует имя пользователя, совпадающее с добавляемым синонимом;
* `alias adding failed` — ошибка добавления синонима;
* `change account log error` — не удалось сделать запись об изменении аккаунта в журнал логирования.