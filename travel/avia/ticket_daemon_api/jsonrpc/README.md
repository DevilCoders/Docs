## HTTP интерфейс к тикетдемону.
https://daemon.avia.yandex.net/jsonrpc/

### Сценарий использования:

1. Инициализация поиска
    * Метод search.init
    * Передаём:
        - point_from
        - point_to
        - national
        - date_forward
        - service
        - date_backward=None
        - klass
        - lang
        - adults=1
        - children=0
        - infants=0
        - ignore_cache=True|False
    * В ответе получаем словарь с ключами:
        - 'qid':  идентификатор поиска
        - 'partners':  ['code1', ...]

2. Ходить на ручку получения результатов поиска
    * Метод search.results
    * Передаём
        - qid
        - lang
        - skip_partners
        - resultpages
    * В ответе получаем словарь с ключами:
        - 'variants':  собственно, варианты. У вариантов
          есть тэги.
        - 'reference':  словарь с объектами, на которые
          ссылаются аттрибуты из вариантов
        - 'status':  статусы опроса партнёров в виде
          словаря {'<partner_code>': 'querying|done|empty|fail' | число}
          если передали число, то его нужно передать с
          тем же ключём в следующем запросе к этой ручке
          в параметре 'resultpages'
        - expired_date

3. Получить подробности для выбранных вариантов из ручки
    * Метод search.order_data
    * Передаём параметры:
        - qid
        - vtags (предпочтительнее) или tags
            * vtags: {'<partner_code>': '<tag>', ...}
            * tags: ['<tag>', ...]
        - lang
    * Получаем тот же формат что и search.results с
      расширенной информацией в вариантах в том числе,
      order_data

4. Получить ссылку (или ссылку и post-данные) на переход к партнёру
    * Метод search.redirect_data
    * Передаём:
        - qid
        - order_data
        - user_info

Подробности с описанием отражены в интеграционном тесте.
Можно взять как пример.
* https://github.yandex-team.ru/avia/td-integration-tests/blob/master/tests/test_search_redirect_data.py

Есть ещё ручки для расписаний. Они выполнены специально
adhoc, и их не нужно больше нигде использовать.


### Пример клиента:

#### python
```python
# jsonrpc-requests==0.3
from jsonrpc_requests import Server

# Параметры пробрасываются в requests.post
server = Server('https://{}/jsonrpc'.format(HOST), timeout=7, verify=False)

answer = server.search.init({
    'point_from': 'MOW',
    'point_to': 'SVX',
    'national': 'ru',
    'date_forward': '2016-11-11',
    'date_backward': None,
    'service': 'ticket',
    'klass': 'economy'
    'adults': 2,
    'children': 1,
    'infants': 1,
    't_code': 'plane',
    # 'ignore_cache': True,
})

assert answer['status'] == 'success'
qid = answer['data']['qid']
partners = answer['data']['partners']  # Партнёры, которых будет опрашивать
```

#### Из консоли
```shell
curl -i -X POST \
    -H "Content-Type: application/json; indent=4" \
    -d '{
    "jsonrpc": "2.0",
    "method": "search.results",
    "params": {
        "qid": "160814-173922-176:ticket:c213_c54_2016-11-11_None_economy_1_0_0_ru",
        "lang": "ru",
        "t_code": "plane"
    },
    "id": "1"
}' "http://jsonrpc-daemon.seiv.cloud.dev.rasp.yandex.net/jsonrpc"
```
