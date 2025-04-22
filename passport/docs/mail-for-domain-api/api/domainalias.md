# Метод domainAlias

Создает объект domain и делает его синонимом другого домена.

{% note info %}

При запросе сведений о домене методом [listDomain](listdomain.md) имена доменов-синонимов выводятся в элементе `aliases`.

{% endnote %}


## Синтаксис запроса {#id1FD576B2}
```
http://passport-internal.yandex.ru/passport
  ? mode=<mdapi>
  & target=<domain>
  & op=<addalias>
  & domain_id=<id>
  & alias=<domain>
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

#### alias
*Обязательный параметр*

{% include [domaindef-alias_d](../_includes/api/domaindef/id-domaindef/alias_d.md) %}


{% note warning %}

Добавление домена-синонима не будет выполнено, если в Паспорте уже зарегистрирован домен с таким же именем. Необходимо удалить одноименный домен с помощью метода [deleteDomain](deletedomain.md), а затем зарегистрировать домен-синоним c этим именем.

{% endnote %}


> # Пример
> `http://passport-internal.yandex.ru/passport`
> `?mode=mdapi&target=domain&op=addalias&domain_id=44&alias=okna-1.ru`
> Запрос добавляет синоним `okna-1.ru` к домену с идентификатором 44.

## Формат ответа {#id00669068}

Ответом является XML-структура с параметрами подключенного домена-синонима.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <domain_id>45</domain_id>
  <errors> </errors>
  <list>
    <domain>
      <admin>0</admin>
      <aliases> </aliases>
      <born_date>2010-09-15 16:21:57</born_date>
      <default_uid>0</default_uid>
      <domain>okna-1.ru</domain>
      <domain_id>45</domain_id>
      <enabled>0</enabled>
      <master_domain>okna.ru</master_domain>
      <mx>0</mx>
      <options>
        <can_users_change_password>1</can_users_change_password>
      </options>
    </domain>
  </list>
  <operation>addalias</operation>
  <status>ok</status>
  <target>domain</target>
</mdapi>
```

В элементе `master_domain` содержится имя основного домена, для которого подключенный домен является синонимом.

Описание других элементов ответа приведено в разделе [Спецификация ответов о доменах](domaindef.md).

## Сообщения об ошибках {#section_ggl_hgk_bbb}

Для проверки ошибок необходимо выяснить наличие элементов `error` в элементе `errors`, а так же наличие элемента `staus` (как написано) со значением "error". Эти элементы могут присутствовать в ответе независимо друг от друга.

Ниже показаны примеры сообщений об ошибке. В первом примере об ошибке говорит элемент `error` внутри элемента `errors`, во втором — элемент `staus` со значением `error`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
    <error>bad-domain</error>
  </errors>
  <operation>addalias</operation>
  <target>domain</target>
</mdapi>
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<mdapi>
  <errors>
  </errors>
  <operation>addalias</operation>
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
Для метода [domainAlias](domainalias.md) также предусмотрено сообщение:
* `bad-domain` — указан несуществующий идентификатор основного домена.

#### staus
	
Наличие элемента `staus` (как написано) со значением 'error' говорит об ошибке на стороне Паспорта. Причина ошибки не уточнятся.
