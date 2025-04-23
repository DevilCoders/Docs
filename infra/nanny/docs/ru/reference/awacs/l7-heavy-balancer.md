# Интерфейс управления весами L7-балансеров

Документ описывает [интерфейс управления весами L7-балансеров](https://nanny.yandex-team.ru/ui/#/list-l7heavy/).

## Краткое описание функциональности {#intro}

* Пользователь может видеть [список доступных админок](https://nanny.yandex-team.ru/ui/#/list-l7heavy/);
* Любой пользователь может создать новую админку, указав следующие данные:
    * идентификатор (например, `production_com_tr`);
    * ITS value path (например, `balancer/l7_heavy/web_com_l7/search_l7_balancer_switch`);
    * список менеджеров админки.
* Менеджер может удалить админку, все веса которой равны нулю (такая проверка реализована во избежание случайностей);
* Менеджер админки может редактировать:
    * ITS value path;
    * список менеджеров;
    * конфиг админки.

Конфиг админки представляет собой список конфигов секций. Конфиг секции содержит:

* список менеджеров секции;
* упорядоченный список обычных локаций;
* упорядоченный список fallback-локаций.

Таким образом, менеджер админки может создавать, редактировать и удалять любые секции (кнопки **Add Section**, **Edit Section** и **Delete Section**).

* Менеджер секции может изменять её веса, которые впоследствии будут записаны в указанную ручку ITS.
* При сохранении веса записываются в ITS, в путь, указанный в настройках админки, в следующем формате:

    ```json
    {
        "comment": "Pushed by <author>. DO NOT EVER edit it by hand -- it will break the Nanny UI!", 
        "config_version": "82ba1e38a434322d74d37fa16e11971eb97f0f75", 
        "payload": {
            "section_name": {
                "location_name_1": 28, 
                "location_name_2": 0, 
                "fallback_location_name_1": 0, 
                "fallback_location_name_2": 0
            }, 
           ...
        }
    }
    ```

Для того, чтобы преобразовать эти данные в формат, который ожидает балансер, предлагается использовать форматтеры в ITS (см. [документацию](../its/its.md#konfigurirovanie)).

## Работа с весами {#weight}

Существующим локациям (то есть, перечисленным в конфиге) можно назначать веса.

При назначении ненулевых весов fallback-локациям интерфейс запросит отдельное подтверждение.

Интерфейс предоставляет возможность производить массовые действия с весами: например, закрыть определённую локацию во всех секциях или вернуть текущие значения весов к дефолтным. Стоит отметить, что нажатие на кнопку из выпадушки **Bulk Actions** изменяет веса только в интерфейсе. Для того, чтобы их сохранить, необходимо нажать на одну из синих кнопок (**Save all weights**, **Save section weights**).

Существует возможность сделать так, чтобы массовые действия секции не касались: для этого необходимо нажать на чекбокс **exclude from bulk actions** в окне редактирования секции.

Данные о существующих секциях и локациях (конфиг админки), а также их веса, хранятся в базе данных Няни.

Любые изменения интерфейс сначала пытается сохранить в БД, и лишь затем записывает словарь с новыми весами в указанную ручку в ITS. В случае, если вызов к ITS завершился неудачей, пользователь увидит плашку с предупреждением о том, что данные в интерфейсе не отражают актуальные веса, записанные в ITS и доставляющиеся на балансер, и кнопками **попробовать ещё раз** (записать данные из БД в ITS) и **забыть об изменениях** (данные в ITS не трогать, откатить содержимое БД).

## Структура весов {#weight-structure}

Веса имеют иерархическую структуру: section → location.

Каждая локация имеет два веса: актуальный (weight) и дефолтный (default weight). Балансеру доставляются только актуальные веса; дефолтные веса предназначены для удобства пользователей.

## API {#api}

RESTful JSON API живёт по адресу `https://ext.its.yandex-team.ru/v2/l7/heavy/`.

Автоматически сгенерированная документация доступна в Няне: [https://nanny.yandex-team.ru/ui/#/l7heavy-api-docs/](https://nanny.yandex-team.ru/ui/#/l7heavy-api-docs/). Она описывает структуру запросов и ответов всех доступных методов API.

Аутентификация точно такая же, [как и в остальном API Няни](../api/rest.md#authz).

### Пример использования {#samples}

Подразумевается, что указатель `production` уже существует. Пример использует API dev-nanny.

```python
# coding: utf-8
import requests  # pip install requests==2.7.0


API_URL = 'https://ext.its.yandex-team.ru/v2/l7/heavy/'
# OAuth-токен можно получить здесь: https://nanny.yandex-team.ru/ui/#/oauth
AUTH_TOKEN = '...'
BALANCER_ID = 'production'
SECTION_ID = 'newsectionid'

session = requests.Session()
session.headers.update({
    'Authorization': 'OAuth {}'.format(AUTH_TOKEN),
})

# Получаем данные об указателе
r = session.get('{}/{}/weights/'.format(API_URL, BALANCER_ID))
data = r.json()
# data['configuration_errors'] — пустой список, если с ручкой ITS всё хорошо
# data['config']['its_value_path']

# Получаем список секций
r = session.get('{}/{}/weights/sections/'.format(API_URL, BALANCER_ID))
data = r.json()
etag = r.headers['ETag']
# data['items'] — список секций
# etag — етаг, используется для concurrency control. Содержит
# версию текущих весов в кавычках (например, "bf2a8e57ee29e62b1e8c228f405e4e2eec2dd00c")

# Создаём свою секцию
r = session.post('{}/{}/weights/sections/'.format(API_URL, BALANCER_ID), json={
    'id': SECTION_ID,
    'locations': [{'id': 'SAS'}, {'id': 'MSK'}],
}, headers={'If-Match': etag})
data = r.json()
etag = r.headers['ETag']
# data['id']
# data['locations']
# data['fallback_locations']

# Получаем веса
r = session.get('{}/{}/weights/values/'.format(API_URL, BALANCER_ID))
data = r.json()
etag = r.headers['ETag']
"""
data имеет следующий вид
{
    'sections': {
        ...
        'newsectionid': {
            'locations': {
                'SAS': {'default_weight': 50, 'weight': 0},
                'MSK': {'default_weight': 50, 'weight': 0},
            },
            'fallback_locations': {
                'DEVNULL': {'default_weight': 0, 'weight': 0},
                'PUMPKIN': {'default_weight': 0, 'weight': 0}
            }
        }
        ...
    }
}
"""

# Обновляем веса секции
for l in ('SAS', 'MSK'):
    data['sections']['newsectionid']['locations'][l]['weight'] = 1
r = session.post('{}/{}/weights/values/'.format(API_URL, BALANCER_ID), json=data, headers={'If-Match': etag})
etag = r.headers['ETag']
current_db_version = etag.strip('"')

# Получаем текущие веса из ITS
r = session.get('{}/{}/weights/its_value/'.format(API_URL, BALANCER_ID))
data = r.json()
current_its_version = data['current_version']

# Пушим обновлённые веса в ITS
r = session.post('{}/{}/weights/its_value/'.format(API_URL, BALANCER_ID), json={
    'current_version': current_its_version,
    'target_version': current_db_version,
})
data = r.json()
current_its_version = data['current_version']

# Проверяем, что всё хорошо
assert current_db_version == current_its_version

# Удаляем секцию
r = session.delete('{}/{}/weights/sections/{}/'.format(API_URL, BALANCER_ID, SECTION_ID),
                   headers={'If-Match': etag})
assert r.status_code == 204
```
