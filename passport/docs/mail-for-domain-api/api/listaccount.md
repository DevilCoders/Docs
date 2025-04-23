# Метод listAccount

Возвращает параметры нескольких аккаунтов или конкретного аккаунта.

## Синтаксис запроса {#id1FE6EC0E}

Запрашивать аккаунты можно по уникальному идентификатору пользователя, по логину, а также по имени или идентификатору домена. Синтаксис запроса показан ниже.
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<account>
  & [op=<list>]
  & (uid=<id> | login=<user@domain> | domain=<uri> | domain_id=<id>)
  & [sort=<field.direction>]
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### op
#### uid
*Обязательный параметр*

{% include [accountdef-uid_d](../_includes/api/accountdef/id-accountdef/uid_d.md) %}

#### login
*Обязательный параметр*

Логин либо часть логина и символ подстановки . Ниже описаны сценарии поиска.

- Указан полный логин в формате `user@domain`. Выполняется поиск по полному совпадению логина.
- Указано имя пользователя `user`. Во всех доменах выполняется поиск аккаунтов с указанным именем пользователя.
- Указана часть имени пользователя, завершающаяся символом подстановки . Во всех доменах выполняется поиск аккаунтов, у которых имена пользователей начинаются с указанных символов, а вместо  находиться любое количество произвольных символов.
- Указана часть имени пользователя, символ подстановки  и домен — `user*@domain`. В указанном домене выполняется поиск аккаунтов, у которых имена пользователей начинаются с указанных символов, а вместо  находиться любое количество произвольных символов.
- Указан только символ подстановки . Эквивалентно выполнению запроса без указания каких-либо параметров поиска. Возвращаются первые 20 аккаунтов.

#### domain
*Обязательный параметр*

{% include [accountdef-domain_d](../_includes/api/accountdef/id-accountdef/domain_d.md) %}

#### domain_id
*Обязательный параметр*

{% include [accountdef-domain_id_d](../_includes/api/accountdef/id-accountdef/domain_id_d.md) %}

#### sort

Указывает параметр аккаунтов для сортировки. Возможны следующие значения:

- `login.asc` — сортировка по возрастанию логина;
- `login.desc` — сортировка по убыванию логина;
- `uid.asc` — сортировка по возрастанию `uid`;
- `uid.desc` — сортировка по убыванию `uid`.

Аргумент `op` может быть опущен, что подразумевает `op = list`.

Аккаунты можно запрашивать блоками по несколько записей. Для этого указывают порядковый номер записи, с которой начнется вывод, и количество записей в блоке. Синтаксис запроса показан ниже.
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<account>
  & [op=<list>]
  & [start=<N>]
  & [count=<N>]
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### op
#### start

Порядковый номер записи, с которой начнется вывод. Нумерация ведется с нуля. Если аргумент не задан, подразумевается `start = 0`.
#### count

Количество выводимых записей (максимум — 100). Если аргумент не задан, подразумевается `count = 20`.

> # Пример 1
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=account&domain=okna.ru&sort=login.asc`
> Запрос аккаунтов на домене `okna.ru`. Если имеется несколько аккаунтов, запрос возвращает их все в порядке возрастания логинов.

> # Пример 2
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=account&op=list&start=20&count=8`
> Запрос возвращает восемь аккаунтов, начиная с двадцать первого.

## Формат ответа {#section_pgn_lhk_bbb}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <count>4</count>
  <errors> </errors>
  <found>202</found>
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
      <fio>nikitin mike</fio>
      <fname>nikitin</fname>
      <glogout>1</glogout>
      <hinta></hinta>
      <hintq></hintq>
      <iname>mike</iname>
      <karma>0</karma>
      <karma_dead_time>0</karma_dead_time>
      <login>mike@okna.ru@okna.ru</login>
      <login_wanted>mike@okna.ru@okna.ru</login_wanted>
      <nickname></nickname>
      <passwd>$1$yTDUUW6b$Y/YLWK.tXZtoEhSUd7uWx/</passwd>
      <regdate>2009-04-27 19:33:29</regdate>
      <sex></sex>
      <signed_eula>0</signed_eula>
      <uid>1130000000000002</uid>
      </account>
    <account>
      ...
    </account>
    ...
  </list>
  <operation>list</operation>
  <start></start>
  <target>account</target>
</mdapi>
```

Описание других элементов ответа приведено в разделе [Спецификация ответов об аккаунтах](accountdef.md).

## Сообщения об ошибках {#section_rgn_lhk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>SearchCrashed</error>
  </errors>
  <operation>list</operation>
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
Для метода [listAccount](listaccount.md) также предусмотрено следующее сообщение:
* `SearchCrashed` — ошибка поиска на стороне Паспорта.