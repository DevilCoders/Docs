proxy
========

Модуль для работы с прокси (3proxy)

Пример использования http-прокси через request:

```python
import requests

pool = YpProxyPool(user='rasp', password='pwd', yd_entry_point='rasp-proxy')
proxy = pool.get_http_proxies()[0]
result = requests.get('https://api.ipify.org', proxies=proxy, verify=False)
```


Пример ftp прокси через wget:
```python
from subprocess import Popen

pool = YpProxyPool('rasp', 'pwd', 'rasp-proxy')
proxy = pool.get_ftp_proxies('ftp://test.ftp.example.com:21')[0]

wget = Popen(['wget', proxy.url, '--user={}'.format(proxy.user), '--password={}'.format(proxy.password)])
```
