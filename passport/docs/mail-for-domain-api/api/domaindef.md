# Спецификация ответов о доменах

В разделе описаны элементы, включаемые в ответы Паспорта о доменах.

Методы [addDomain](#addDomain), [listDomain](#listDomain), [editDomain](#editDomain), [deleteDomain](#deleteDomain), [domainAlias](#domainAlias) возвращают ответы в формате XML. Ответы содержат параметры доменов и сведения о результатах выполнения запросов.

## Параметры доменов {#section_brj_rfk_bbb}

Ниже описаны элементы, содержащие параметры доменов.

#### admin

{% include [domaindef-admin_d](../_includes/api/domaindef/id-domaindef/admin_d.md) %}

#### aliases

Содержит элементы `alias` с именами доменов-синонимов, если имеются. Вновь зарегистрированные домены не имеют синонимов.

#### alias

Имя домена-синонима, например `okna-1.ru`.

#### born_date

Дата и время подключения домена.

#### default_uid

{% include [domaindef-default_uid_d](../_includes/api/domaindef/id-domaindef/default_uid_d.md) %}

#### default

{% include [domaindef-default_d](../_includes/api/domaindef/id-domaindef/default_d.md) %}

#### domain

Элемент `domain` внутри элемента `list` содержит параметры почтовой базы. Одним из параметров является вложенный элемент `domain`, содержащий имя домена, например `okna.ru`.

#### domain_id

{% include [domaindef-domain_id_d](../_includes/api/domaindef/id-domaindef/domain_id_d.md) %}

#### enabled

{% include [domaindef-enabled_d](../_includes/api/domaindef/id-domaindef/enabled_d.md) %}

#### master_domain

Имя основного домена, для которого текущий домен является синонимом (см. метод [domainAlias](domainalias.md)).

#### options

Содержит дополнительные параметры домена:

* `can_users_change_password`;
* `change_password_url`.

При подключении домена автоматически задается параметр `can_users_change_password` со значением 1. Задать дополнительные параметры можно с помощью метода [editDomain](editdomain.md).

#### mx

{% include [domaindef-mx_d](../_includes/api/domaindef/id-domaindef/mx_d.md) %}

#### can_users_change_password

{% include [domaindef-can_users_change_password_d](../_includes/api/domaindef/id-domaindef/can_users_change_password_d.md) %}

#### change_password_url

{% include [domaindef-change_password_url_d](../_includes/api/domaindef/id-domaindef/change_password_url_d.md) %}

## Результаты выполнения запросов {#section_drj_rfk_bbb}

Ниже описаны элементы, содержащие результаты выполнения запросов.

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

#### list	

Содержит список доменов с параметрами.

#### status	

Содержит значение 'ok', если запрос выполнен без ошибок, или 'error' если произошла ошибка.

#### staus
	
Наличие элемента `staus` (как написано) со значением 'error' говорит об ошибке на стороне Паспорта. Причина ошибки не уточнятся.

#### operation	

Название операции. Совпадает с аргументом `op` из запроса.

#### target	

Название информационного объекта, над которым выполнена операция. Совпадает с аргументом target из запроса.

#### count	

Запрос блока записей: содержит количество возвращенных записей.

Запрос по конкретному домену: содержит 1, если он найден, или 0 в противном случае.

#### found	

Запрос блока записей: содержит количество доменов, подключенных к Почте.

{% note info %}

Чтобы организовать постраничную выборку последовательными запросами, необходимо проверять, возвращены ли данные о последнем домене. Если выполняется условие `start + count = found`, данные о последнем домене присутствуют в ответе.

{% endnote %}

Запрос по конкретному домену: содержит 1, если он найден, или 0 в противном случае.

#### start
	
Запрос блока записей: содержит порядковый номер первой записи в ответе. Нумерация ведется с нуля.

Запрос по конкретному домену: не заполняется.