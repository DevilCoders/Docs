# Sandbox API

Для программного управления Sandbox следует использовать его API.

## Описание API { #spec }

* **[OpenAPI Specification](https://sandbox.yandex-team.ru/api/v1.0/swagger.json)**. Содержит машиночитаемое описание Sandbox API хранится в формате [OpenAPI](https://en.wikipedia.org/wiki/OpenAPI_Specification) (Swagger). По данному описанию можно сгенерировать клиентскую библиотеку для требуемого языка программирования.
* **[Swagger UI](https://sandbox.yandex-team.ru/media/swagger-ui/)**. Позволяет вручную вызывать различные методы API.
* **[ReDoc](https://sandbox.yandex-team.ru/api/redoc)**. Еще один вариант просмотра документации по API с подробным описанием методов и параметров.

## Аутентификация { #auth }

Sandbox API поддерживает 2 способа аутентификации: [OAuth](https://en.wikipedia.org/wiki/OAuth) и [TVM](https://wiki.yandex-team.ru/passport/tvm2/).

### OAuth { #auth-oauth }

Получить OAuth-токен можно [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=968e0e6d85d647feb327d893a42cf26f&optional_scope=sandbox:api) (минимальный скоуп для использования API)
или [здесь](https://sandbox.yandex-team.ru/oauth) (полный набор скоупов для работы всех API-методов, включая делегацию секретов).
Токен нужно передавать в HTTP-заголовке `Authorization`:

```
Authorization: OAuth <token-value>
```

Также можно использовать собственные OAuth-приложения. В них нужно добавить скоуп `sandbox:api`.

### TVM { #auth-tvm }

При использовании TVM для аутентификации в Sandbox следует использовать следующие [идентификаторы](https://abc.yandex-team.ru/services/sandbox/resources/?supplier=14&type=47&type=50&state=requested&state=approved&state=granted&view=consuming&show-resource=4544864):

```
id = 2002826
name = sandbox-production
```

Sandbox API ожидает, что в HTTP-запросе будет выставлено два заголовка:

```
X-Ya-Service-Ticket: <TVM2-service-ticket>
X-Ya-User-Ticket: <TVM2-user-ticket>
```

## Клиентские библиотеки { #client-library }

### Официальный Python-клиент { #python-client }

Официальный Python-клиент хранится в [sandbox/common/rest](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/rest).

{% note info %}

По факту он является универсальным REST API клиентом, его можно использовать и для других API.

{% endnote %}

* Поддерживается Python 2 и 3.
* Клиента можно использовать, как для проектов из единого репозитория, так и в виде PyPI-пакета [sandbox-library](https://pypi.yandex-team.ru/dashboard/repositories/default/packages/sandbox-library/).
* Протестировать клиента можно через [Sandbox shell](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/scripts/api).

### Требования к сторонним клиентам { #third-party-client-reqs }

Для работы с Sandbox API под любой язык программирования можно использовать любой доступный клиент. Клиент должен удовлетворять следующим требованиям:

* При получении следующих кодов ответа на HTTP-запрос клиент должен выполнять перезапросы с увеличивающимся интервалом между запросами (например, [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff)):
    - `HTTP 503 Service Overloaded` (Sandbox API перегружено);
    - `HTTP 429 Too Many Requests` (исчерпана квота на запросы к API).
* Для удобства отладки следует передавать HTTP-заголовки:
    - `User-Agent` для идентификации источника запроса (сервис, компонент, имя пользователя, FQDN сервера, и т.п.);
    - `X-Request-Id` с уникальным идентификатором запроса в формате [UUID v4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random)). Идентификатор запроса не должен изменяться при перезапросе. Идентификаторы следует записывать в лог на стороне клиента.

### Список известных сторонних клиентов { #third-party-client }

* [@yandex-int/sandboxer](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/sandboxer) для node.js

## Квота на использование API { #quota }

**Потребление API** — сумма длительностей обработанных запросов пользователя за последние 15 минут. Потребление обновляется раз в секунду. Долгие запросы к API учитываются в процессе исполнения, а не в момент завершения.

* Запросы к API, исполняемые на сервере Sandbox (создать, сохранить или запустить задачу), потребляют API от имени пользователя, который отправил соответствующий запрос (например, `robot-sandbox@`).

* Запросы к API из методов задач, исполняемых на агентах (все кроме `on_create`, `on_save` и `on_enqueue`), потребляют API от имени владельца (owner) задачи (обычно это [одна из групп Sandbox](https://sandbox.yandex-team.ru/admin/groups)).

* При превышении квоты сервер будет возвращать ответ с кодом `429 Too Many Requests`. Предполагается, что при получении такой ответа нужно отправлять запрос еще раз, но с увеличивающимся интервалом между запросами (например, [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff)). Официальный Python клиент Sandbox умеет правильно обрабатывать этот код.

* По умолчанию каждому пользователю дана квота в **30 минут**. Это, например, позволяет, непрерывно потреблять два серверных потока в течение 15 минут.

* Для запросов из UI Sandbox квоты считаются отдельно в трехминутном окне. Для таких запросов установлена **единая квота в 12 минут**.

### Мониторинг расхода API квоты { #consumption-monitoring }

Подробно проанализировать характер потребления API квоты конкретного пользователя можно [на нашем дашборде в Grafana](https://grafana.yandex-team.ru/d/000016022/sandbox-api-production-by-user).

Также значения текущего потребления и квоты есть в Solomon ([пример для пользователя zomb-sandbox@](https://solomon.yandex-team.ru/?project=sandbox&cluster=sandbox_consumption&service=sandbox_consumption&l.owner=zomb-sandbox&l.sensor=api_quota&graph=auto&stack=false)).
Для графиков потребления в Solomon можно быстро создать мониторинг с эскалацией, если воспользоваться нашим шаблоном `API quota usage` на [странице шаблонов](https://solomon.yandex-team.ru/admin/projects/sandbox/alerts/templates?serviceProviderId=sandbox).


## Актуальность данных { #dataaccuracy }

При выполнении запросов на чтение в API Sandbox подразделяет все запросы на три типа, которым обеспечивает различные гарантии получения актуальных данных:

* Анонимные запросы — такие запросы всегда выполняются на SECONDARY-инстансах безусловно.

* Авторизованные запросы из внешних систем — запросы по-умолчанию выполняются на SECONDARY-инстансах, однако можно изменить это поведение передав [заголовок](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/types/misc.py?rev=r7933813#L284) `X-Read-Preference: PRIMARY`. Список возможных значений перечислен [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/types/database.py).

* Запросы из задач (с сессионным токеном) — запросы по-умолчанию выполняются на PRIMARY-инстансах, это поведение можно изменить по инструкции выше.


## Логи доступа к API { #logs }

Sandbox выгружает логи доступа к API в YT.
Найти их можно в таблицах [//home/sandbox/production/logs/api/access](https://yt.yandex-team.ru/hahn/navigation?path=//home/sandbox/production/logs/api/access).

## Sandbox rest client

Sandbox поддерживает свой python23 [Rest Client](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/rest/__init__.py) для использования Sandbox API.

### Установка
* Для проектов в Аркадии добавьте `PEERDIR` на `sandbox/common/rest` в файл `ya.make`.
* Для внешних проектов клиент доступен как sandbox-library package во внутреннем PyPI. Устанавливается командой `pip install -i https://pypi.yandex-team.ru/repo/default sandbox-library`.

В обоих случаях модуль с клиентом импортируется как `from sandbox.common import rest`.

### Использование в Sandbox-задаче

* В Sandbox-задачах Sandbox Rest Client уже настроен и доступен из объекта класса задачи как `self.server`.
* Вне объекта задачи Sandbox Rest Client можно получить как `sdk2.Task.server`.
* Можно создать другой инстанс Sandbox Rest Client как `rest.Client()`. Он будет автоматически авторизован автором работающией задачи.

### Как этим пользоваться

Sandbox Rest Client использует Python атрибуты класса и получение итема как часть URl пути, разделенного символовами `/`. Кроме этого есть служебные методы.

Служебные методы:
* `read(p1=v1, p2=v2)` - выполнить GET запрос по составленному URL с `query` аргументами `p1=v1&p2=v2`
* `update(p1=v1, p2=v2)` - выполнить PUT запрос по составленному URL с телом `{p1: v1, p2: v2}`
* `create(p1=v1, p2=v2)` - выполнить POST запрос по составленному URL с телом `{p1: v1, p2: v2}`

То есть код
```python
client = common.rest.Client()
client.resource[1].read()
```
создает инстанс Sandbox Rest Client'а и делает запрос GET `SERVICE_URL/resource/1`.

Добавить header к запрос из клиента можно через подкласс HEADERS:

```python
client = common.rest.Client() << common.rest.Client.HEADERS({"X-User-Header": "value"})
```

Получить словать header'ов ответа тоже можно через подкласс HEADERS:

```python
response_headers = common.rest.Client.HEADERS()
client = common.rest.Client() >> response_headers
client.resource[1].read()
```

после этого `response_headers` будет словарем с header'ами ответа.

### Примеры использования

```python
# GET /<base path>/resource:
sandbox.resource[:]
sandbox.resource[...]
sandbox.resource.read()

# GET /<base path>/resource?limit=10:
sandbox.resource[:10]
sandbox.resource.read(limit=10)
sandbox.resource.read({"limit": 10})

# GET /<base path>/resource?limit=10&offset=20:
sandbox.resource[20:10]
sandbox.resource.read(offset=20, limit=10)
sandbox.resource.read({"offset": 20, "limit": 10})

# GET /<base path>/resource?limit=10&offset=20&order=-id:
sandbox.resource[20:10:"-id"]
sandbox.resource.read(offset=20, limit=10, order="-id")
sandbox.resource.read({"offset": 20, "limit": 10, "order": "-id"})

# GET /<base path>/resource?type=OTHER_RESOURCE&limit=10&order=state:
sandbox.resource[{"type": "OTHER_RESOURCE"}, : 10: "state"]
sandbox.resource.read(type="OTHER_RESOURCE", limit=10, order="state")
sandbox.resource.read({"type": "OTHER_RESOURCE", "limit": 10, "order": "state"})

# GET /<base path>/resource/12345:
sandbox.resource[12345][:]
sandbox.resource[12345][...]
sandbox.resource[12345].read()

# GET /<base path>/resource/12345/attribute:
sandbox.resource[12345].attribute[:]
sandbox.resource[12345].attribute[...]
sandbox.resource[12345].attribute.read()

# POST /<base path>/resource:
sandbox.resource(**fields)
sandbox.resource({<fields>})
sandbox.resource.create(**fields)
sandbox.resource.create({<fields>})

# PUT /<base path>/resource/12345:
sandbox.resource[12345] = {<fields>}
sandbox.resource[12345].update(**fields)
sandbox.resource[12345].update({<fields>})

# WARNING: PUT endpoints in Sandbox API normally *replace*
# the whole resource rather than partially update it as one
# would expect from a method called `update()`.
# DELETE /<base path>/resource/12345/attribute/attr1:
del sandbox.resource[12345].attribute
del sandbox.resource[12345].attribute.attr1
del sandbox.resource[12345].attribute["attr1"]
sandbox.resource[12345].attribute.delete("attr1")
```
