# ~~In~~sane requests
Небольшой враппер для простого создания сессий с дефолтными таймаутами и
включёнными ретраями, вдохновение черпалось из https://findwork.dev/blog/advanced-usage-python-requests-timeouts-retries-hooks/

Дефолтные таймауты: 60 ms connect timeout, 30 sec read timeout
Дефолтные паузы между попытками (секунды): 0.5, 1, 2, 4, 8, 16, 32, 64, 120, 120

Несколько примеров:

```python
from saas.library.python.sane_requests import get_session

my_session = get_session()  # type: requests.Session
response = my_session.get('https://example.com/')
other_response = my_session.get('https://example.com/fast', timeout=(0.02, 0.3))  # override default timeouts for request with 20ms connect, 300ms read
```

Кастомизация таймаутов
```python
from saas.library.python.sane_requests import get_session
from saas.library.python.sane_requests.timeout_http_adapter import TimeoutHTTPAdapter

my_session = get_session(adapter=TimeoutHTTPAdapter(timeout=(3.05, 900)))  # type: requests.Session
response = my_session.get('https://example.com/')  # use connect timeout 3.05 sec and read timeout 900 sec
```

Кастомизация ретраев
```python
from saas.library.python.sane_requests import get_session
from saas.library.python.sane_requests.exponential_retry_strategy import get_retry_strategy

my_retry_strategy = get_retry_strategy(
    total=300,  # total retries; default=10
    connect=3,  # connect retries; ! values > total not working! default=5
    # retries only performed if request method in method_whitelist AND response code in status_forcelist
    method_whitelist=['HEAD', 'GET'],  # default: {'HEAD', 'TRACE', 'GET', 'OPTIONS', 'DELETE'}
    status_forcelist=[400, 429, 500], # default: {503, 504, 529, 598, 408, 429}
    backoff_factor=0.1,  # sleep before next try calculated as {backoff_factor} * (2 ** ({made_tries} - 1)), so for 0.1 sleeps would be 0.2s, 0.4s, 0.6s, ...
    respect_retry_after_header=True  # if the response contains Retry-After header, the next retry will wait for Retry-After seconds
)

my_session = get_session(retry_strategy=my_retry_strategy)  # type: requests.Session
response = my_session.get('https://example.com/')
```
