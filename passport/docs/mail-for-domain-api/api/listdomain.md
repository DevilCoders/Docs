# Метод listDomain

Возвращает данные о нескольких доменах или о конкретном домене.

## Синтаксис запроса {#id1FD472EE}

Сведения о домене можно запрашивать по имени или идентификатору домена. Синтаксис запроса показан ниже.
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<domain>
  & [op=<list>]
  & domain=<URI>
  & domain_id=<id>
```
### Параметры
#### mode
*Обязательный параметр*
#### target
*Обязательный параметр*
#### op
#### domain
*Обязательный параметр*

Имя домена.

#### domain_id

*Обязательный параметр*

{% include [domaindef-domain_id_d](../_includes/api/domaindef/id-domaindef/domain_id_d.md) %}


Аргумент `op` может быть опущен, что подразумевает `op = list`.

Сведения о доменах можно получать блоками по несколько последовательных записей. Для этого указывают порядковый номер записи, с которой начнется вывод, и количество записей в блоке. Синтаксис запроса показан ниже.
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<domain>
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

Порядковый номер записи, с которой начнется вывод. Нумерация ведется с нуля. Если аргумент не задан, подразумевается `start = 0`.
#### count

Количество последовательных записей в блоке (максимум — 100). Если аргумент не задан, подразумевается `count = 20`.

> # Пример 1
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=domain&domain=okna.ru`
> Запрос возвращает запись о домене `okna.ru`.

> # Пример 2
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=domain?op=list&start=20&count=8`
> Запрос возвращает восемь записей о доменах, начиная с двадцать первой записи.

## Формат ответа {#id0063E59B}

Ответом является XML-структура следующего вида.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <count>8</count>
  <errors> </errors>
  <found>28</found>
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
      ...
    </domain>
    ...
  </list>
  <operation>list</operation>
  <start>20</start>
  <target>domain</target>
</mdapi>
```

Ниже описаны элементы, характеризующие количество записей в ответе.

#### count	

Запрос блока записей: содержит количество возвращенных записей.

Запрос по конкретному аккаунту: содержит 1, если он найден, или 0 в противном случае.

#### found	

Запрос блока записей: содержит общее количество доменных аккаунтов в Паспорте.

{% note info %}

Чтобы организовать постраничную выборку последовательными запросами, необходимо проверять, возвращены ли данные о последнем аккаунте. Если выполняется условие `start + count = found`, данные о последнем аккаунте присутствуют в ответе.

{% endnote %}

#### start
	
Запрос блока записей: содержит порядковый номер первой записи в ответе. Нумерация ведется с нуля.

Запрос по конкретному аккаунту: не заполняется.

Описание других элементов ответа приведено в разделе [Спецификация ответов о доменах](domaindef.md).

## Сообщения об ошибках {#section_zst_wfk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`. Ниже показан пример сообщения об ошибке.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>SearchCrashed</error>
  </errors>
  <operation>list</operation>
  <target>domain</target>
</mdapi>
```

