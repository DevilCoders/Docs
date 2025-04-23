https://wiki.yandex-team.ru/intranet/idm/dev/

## Установка
```shell
export LDFLAGS="-I/usr/local/opt/openssl/include -L/usr/local/opt/openssl/lib" # для установки psycopg2
pip install -i https://pypi.yandex-team.ru/simple/ -r requirements/python/requirements.txt
pip install -r requirements/python/dev-requirements.txt
```