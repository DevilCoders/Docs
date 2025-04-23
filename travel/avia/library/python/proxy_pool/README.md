# Пул партнерских прокси

Описание партнерского прокcи: https://wiki.yandex-team.ru/avia/dev/services-table/partner-proxy/

Пример использования для FTP:

```python
import ftplib

from travel.avia.library.python.proxy_pool.deploy_proxy_pool import DeployProxyPool

pool = DeployProxyPool(
    environment='production',
    datacenter='sas',
    login='avia',
    password='XXX',
)
proxy = pool.get_proxy()
ftp = ftplib.FTP(timeout=10,)
ftp.connect(proxy.get_ftp_host(), proxy.FTP_PORT)
ftp.login(proxy.get_ftp_user('ftp-user', 'ftp-host'), 'ftp-password')
```
