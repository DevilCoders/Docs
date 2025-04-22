Installation:
```python
pip install svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/noc/rtapi
```

Usage:

```python
import rtapi
api = rtapi.RTAPI()
object_id = api.call.findObjectByName('sas1-s100')
```

Async API usage:

```python
import aiortapi


async def no_authentication():
    """Call rtapi without authentication via raw TCP socket."""
    with aiortapi.RTAPI() as rt:
        res = await rt.call.findObjectByName("myt-s15")
        print(res)


async def ssh_authentication():
    """Call rtapi with SSH pub key auth via SSL socket."""
    with aiortapi.RTAPI(auth_try_ssh=True) as rt:
        res = await rt.call.getTagByName("тестовый свитч")
        print(res)


async def read_write():
    """Call rtapi in read-write mode."""
    with aiortapi.RTAPI(rw=True, auth_try_ssh=True) as rt:
        object_id = await rt.call.findObjectByName("myt-s15")
        downtime_objects = [int(object_id)]
        downtime_hours = 1
        await rt.call.setDowntime(downtime_objects, downtime_hours)
```

Обновление пакета в локальном пипе:
```
python setup.py sdist upload -r yandex
```
В конфиге ~/.pypirc должны быть явки для yandex. Если их нет то идем сюда https://wiki.yandex-team.ru/pypi/#zagruzkapaketov


Обновление пакетов на dist.yandex.net/noc:

1. Поправить мейнтейнера в stdeb.cfg (чтобы пакет можно было подписать)
2. При необходимости бампнуть Debian-Version там же (версия апстрима берется из setup.py)
3. Выполнить:
```
docker build --tag rtapi_builder .
docker run --rm -v`pwd`:/docker rtapi_builder
```

Пакеты будут собраны в ./deb_dist. Подписать и загрузить на dist:
```
sudo chown -R `whoami` deb_dist
cd deb_dist
debsign rtapi_0.9-2_amd64.changes
dupload rtapi_0.9-2_amd64.changes
```

В ~/.dupload.conf должен быть конфиг для dist/noc:

```
package config;
$default_host = "noc";
$cfg{'noc'} = {
    fqdn => "noc.dist.yandex.ru",
    method => "scpb",
    incoming => "/repo/noc/mini-dinstall/incoming/",
    dinstall_runs => 0,
    login => <ваш_логин>
};
```

Пакеты должны оказаться в:
```
deb http://dist.yandex.ru/noc stable/all/
```
