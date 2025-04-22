# Cервисный балансер Nanny, комуналка

Документ описывает [интерфейс управления сервисным балансером](https://nanny.yandex-team.ru/ui/#/services/balancer/).

При использовании сервисного балансера Nanny следует учитывать:
* во время закрытия любой локации коммунальный балансер не обновляет конфигурации;
* возможные проблемы в обработке долгоживущих запросов по причине частых обновлений конфигурационного файла балансера. Каждое из обновлений вызывает обрыв всех соединений, не завершившихся по истечении определённого промежутка времени;
* отсутствие гарантий на производительность балансера. Слишком большой поток запросов в один из сервисов может вызвать проблемы в работе всего балансера;
* долгое время обновления конфигурации этого балансера (десятки минут в лучших случаях).

{% note alert %}

В связи с этим мы рекомендуем использовать сервисный балансер Няни только для ваших тестовых сервисов и некритичных сервисов с нагрузкой до 100 RPS.

Во всех остальных случаях следует использовать выделенные балансеры, которые вы можете завести самостоятельно, воспользовавшись следующей [инструкцией](https://wiki.yandex-team.ru/cplb/howtocreatebalancer).

{% endnote %}

## Немного технических деталей {#details}

Интерфейс редактирования конфига является обёрткой над обычным сервисом Няни. Он предоставляет удобную форму для редактирования специального типа ресурсов сервиса — services balancer config file, а также производит дополнительную валидацию данных и авторизацию пользователей.

## Конфиг балансера {#config}

Конфиг имеет иерархическую структуру с одним уровнем вложенности: section — traffic slice.

В **секции** задаются:

* уникальный идентификатор;
* матчер. В данный момент матчинг производится по хосту и (опционально) префиксу. Префикс это строка, которая может содержать не более одного плейсхолдера `.*`.
* заголовки, которые балансер будет передавать бэкендам;
* настройки балансировки (balancing options), которые будут унаследованы всеми бэкендами.

На уровне секций происходит авторизация. Менеджером секции считается любой, кто является менеджером любого из вложенных бэкендов.

Секция может содержать один или более трафик слайсов.

В **трафик слайсе** задаются:

* уникальный идентификатор;
* идентификатор сервиса и его конкретного снапшота, задающего список инстансов бэкенда;
* опционально — настройки балансировки, которые переопределят те, что указаны в секции.

Настройки балансировки подробно описаны в [документации на балансер](https://beta.wiki.yandex-team.ru/JandeksPoisk/Sepe/balancer/Cookbook/#balansiruemnagruzku).

## API {#api}

RESTful JSON API живёт по адресу `https://nanny.yandex-team.ru/v2/services_balancers/`.

Автоматически сгенерированная документация доступна в Няне: [https://nanny.yandex-team.ru/ui/#/services/balancers/api-docs](https://nanny.yandex-team.ru/ui/#/services/balancers/api-docs). Она описывает структуру запросов и ответов всех доступных методов API.

Механизм аутентификации используется [тот же, что и в остальном API Няни](../api/rest.md).

## Пример использования {#sample}

Подразумевается, что указатель `production` уже существует. Пример использует API dev-nanny.

```python
# coding: utf-8
import requests  # pip install requests==2.7.0


API_URL = 'http://dev-nanny.yandex-team.ru/v2/services_balancers'
# OAuth-токен можно получить здесь: https://dev-nanny.yandex-team.ru/ui/#/oauth
AUTH_TOKEN = '...'
POINTER = 'production'
SECTION_ID = 'new-section-id'

session = requests.Session()
session.headers.update({
    'Authorization': 'OAuth {}'.format(AUTH_TOKEN),
})

# Получаем данные об указателе
r = session.get('{}/{}/'.format(API_URL, POINTER))
data = r.json()
# data['configuration_errors'] — пустой список, если с сервисом всё хорошо
# data['pointer']['id'] == 'production'
# data['pointer']['service_id']
# data['pointer']['domain']

# Получаем список секций
r = session.get('{}/{}/config/sections/'.format(API_URL, POINTER))
data = r.json()
# data['content'] — список секций
# data['snapshot_id'] — идентификатор runtime-атрибутов сервиса, используемый для concurrency control

# Создаём свою секцию
r = session.post('{}/{}/config/sections/'.format(API_URL, POINTER), json={
    'snapshot_id': data['snapshot_id'],
    'content': {
        'id': SECTION_ID,
        'matcher': {'host': 'test.n.yandex-team.ru'},
        'headers': [
            {'name': 'X-Forwarded-For', 'type': 'create_func_weak', 'value': 'realip'}
        ],
        'balancing_options': {
            'connection_timeout': '300ms',
            'backend_timeout': '3s',
            'retries_count': 3,
            'keepalive_count': 5,
            'fail_on_5xx': False,
            'balancing_type': {
                'mode': 'rr'
            }
        },
        'traffic_slices': [
            {
                'name': 'main',
                'weight': 100,
                'backend': {
                    'service_id': 'prestable_sleep',
                    'snapshot_id': '5452b89eea6f8e057c2545fe088a00b2bb526ecd',
                },
                'balancing_options': {}
            }

        ]
    }
})
data = r.json()

# Удаляем свою секцию
r = session.delete('{}/{}/config/sections/{}/'.format(API_URL, POINTER, SECTION_ID), json={
    'snapshot_id': data['snapshot_id'],
})
# r.status_code == 204
```

##  Копирование секции сервисного балансера {#copy-balancer-section}

```python
# coding: utf-8
import requests  # pip install requests==2.7.0


API_URL = 'http://nanny.yandex-team.ru/v2/services_balancers'
# OAuth-токен можно получить здесь: https://nanny.yandex-team.ru/ui/#/oauth
AUTH_TOKEN = '...'
SRC_BALANCER = 'production'
DST_BALANCER = 'fake_services_msk'
SECTION_ID = 'test'


if __name__ == '__main__':

    session = requests.Session()
    session.headers.update({
        'Authorization': 'OAuth {}'.format(AUTH_TOKEN),
    })

    # Получаем содержимое исходной секции
    r = session.get('{}/{}/config/sections/{}/'.format(API_URL, SRC_BALANCER, SECTION_ID))
    r.raise_for_status()
    data = r.json()
    content = data['content']

    # Получаем snapshot_id конечного балансера для concurrency control
    r = session.get('{}/{}/config/sections/'.format(API_URL, DST_BALANCER))
    r.raise_for_status()
    data = r.json()
    snapshot_id = data['snapshot_id']

    # Создаём свою секцию
    r = session.post('{}/{}/config/sections/'.format(API_URL, DST_BALANCER), json={
        'snapshot_id': snapshot_id,
        'content': content
    })
    r.raise_for_status()
    print r.status_code

```
