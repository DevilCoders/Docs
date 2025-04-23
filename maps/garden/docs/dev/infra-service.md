# Yandex Infra

Пресеты:

* [События деплоя данных в infra (stable)](https://infra.yandex-team.ru/timeline?preset=Ln7tUnSQxq9)
* [События деплоя данных в infra (datatesting)](https://infra.yandex-team.ru/timeline?preset=3oiKXLvcnEh)
* [События деплоя данных в infra (testing)](https://infra.yandex-team.ru/timeline?preset=iC5A3Vs3ftn)

Огород постит события по deployment-билдам в сервис
[Yandex Infra](https://infra.yandex-team.ru/).
За Огородом закреплён отдельный неймспейс "Maps Garden" (id: 372).
Каждый сервис в данном неймспейсе соответствует одноименному модулю.
За каждым модулем закреплён набор окружений.
Каждому окружению соответствует одноименный контур.

Текущая реализация предполагает, что все необходимые сервисы и
их окружения уже были проинициализированы в infra. Они вычитываются
[на этапе запуска сервера](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/server/lib/notification/infra.py?rev=7517425#L35).

REST API сервиса infra можно посмотреть [здесь](https://infra-api.yandex-team.ru/swagger/).
Авторизация API осуществляется через OAuth токен, который можно получить [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=5dd9c4ae3ecd4e73942858d992f2f341).
Ниже приведены примеры кода по поддержанию списка сервисов и их окружений.
Переменная `session` проинициализирована вот так:

```python
from requests_toolbelt.sessions import BaseUrlSession

GARDEN_NAMESPACE_ID = 372
YANDEX_INFRA_TOKEN = "PUT YOUR INFRA TOKEN HERE"

session = BaseUrlSession(base_url='https://infra-api.yandex-team.ru/v1/')
session.headers['Authorization'] = f'OAuth {YANDEX_INFRA_TOKEN}'

```

## Добавление нового контура

```python
for service in session.get(f'namespace/{GARDEN_NAMESPACE_ID}/services').json():
    session.post('environments', json={
        'name': new_contour_name,
        'serviceId': service['id'],
        'myt': False,
        'man': False,
        'sas': True,
        'vla': False,
        'iva': False,
        'createCalendar': False,
    })
```

Я не уверен, что признак `sas` является значимым. Оставляю его из-за того, что
кластер `hahn` живет в Сасово

## Добавление нового модуля

Необходимо создать сервис в Огородном неймспейсе, создать для него необходимый
набор окружений и указать в acl владельцев этого сервиса

```python
new_service_name = "REPLACE WITH YOUR SERVICE NAME"

service = session.post('services', json={'name': new_service_name, 'namespaceId': GARDEN_NAMESPACE_ID}).json()

for env in ['stable', 'datatesting', 'testing']:
    session.post('environments', json={
        'name': env,
        'serviceId': service['service_id'],
        'myt': False,
        'man': False,
        'sas': True,
        'vla': False,
        'iva': False,
        'createCalendar': False,
    })

garden_admins = [
    owner["subject"]["value"]
    for owner in session.get(f'namespace/{GARDEN_NAMESPACE_ID}').json()["owners"]
]

for user in garden_admins + ['robot-garden']:
    session.post('acl', json={'userLogin': user, 'serviceId': service['service_id']})
```

Чтобы события начали отправляться из Огорода в Yandex Infra, после регистрации нового модуля нужно перезагрузить scheduler сервис.

### Добавление нового модуля в пресет

Пресеты редактируются от имени robot-garden в UI Yandex Infra.

В окне выбора пресета нужно нажать карандашик для редактирования
и поставить чекбокс напротив соответствующего окружения для нового модуля.
