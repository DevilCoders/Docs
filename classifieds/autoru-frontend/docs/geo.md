# Как пользоваться гео-данными

Приоритет определения гео:

1. Параметр `geo_id` в урле
2. Регион за слешем (`https://auto.ru/moskva/`)
3. Кука `gids`
4. Автоопределение по IP-адресу

**ВАЖНО: пустой `geo_id` (например, `?geo_id=`) и отсутствие `geo_id` - это РАЗНЫЕ ЗНАЧЕНИЯ. Первый означает - любой регион**

Исследовать геобазу можно в веб-интерфейсе [geoadmin.yandex-team.ru/](https://geoadmin.yandex-team.ru/) или с помощью [API](https://doc.yandex-team.ru/lib/libgeobase5/concepts/interfaces-nodejs.xml).

## request

**Вычисленный регион** (в т.ч. сессионный). В большинстве случаев используется именно он:
* **`req.geoIds`** - `{number[]}` массив ID регионов пользователя, определенный согласно нашим правилам
* **`req.geoIdsInfo`** - объект `{rid: <geobase.getRegionById(rid)>}` с информацией про регион.
* **`req.geoIdsParents`** -  объект `{rid: [parents]}` для регионов `req.geoIds`.

**Сохраненный регион** (без учета сессии):
* **`req.geoReqIds`** - `{number[]}` массив ID регионов пользователя, определенный из запроса без учета региона в урле (кука или IP). Т.о. это постоянный регион пользователя, а не сессионный.
* **`req.geoReqIdsParents`** -  объект `{rid: [parents]}` для регионов `req.geoReqIds`.

Информация о **IP пользователя**:
* **`req.regionByIp`** - результат работы [`geobase.regionByIp()`](https://doc.yandex-team.ru/lib/libgeobase5/concepts/interfaces-nodejs.xml#meth-region_by_ip) от IP-адреса входящего запроса (`req.env.clientIp`).
  Это означает, что в контроллерах не надо вручную дергать гео-метод `regionByIp`, все данные уже есть
* **`req.regionByIpParents`** - `{number[]}` результат работы [`geobase.parents()`](https://doc.yandex-team.ru/lib/libgeobase5/concepts/interfaces-nodejs.xml#meth-parents) от `req.regionByIp`


Вспомогательные поля:

* **`req.geoOverride`** - гео переопределен, т.е. сохраненный регион пользователя (кука `geo_id`) и регион в урле (параметры или за слешом) не совпадают.
Используется последний как более приоритетный.
* **`req.geoSource`** - источник данных о гео пользователя (`cookies`, `ip`, `location`, `path`, `query`)
* **`req.isInternalNetwork`** - запрос сделан из внутренней сети Яндекса. Доступен так же в priv, как `data.isInternalNetwork`
