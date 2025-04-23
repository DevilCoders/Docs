# Нацеливание баннера на себя
[Описание и как воспользоваться](https://yandex.ru/support/direct/impressions/view-ad.html)

## Как это работает

Нацеливание — ручка [banner_aiming/set_cookie](https://a.yandex-team.ru/arc/trunk/arcadia/direct/web/src/main/java/ru/yandex/direct/web/entity/cookie/banneraiming/controller/BannerAimingController.java?rev=5435964#L59) в java-web.
Она выставляет контейнерную [yp cookie](https://wiki.yandex-team.ru/cookies/y/#yp) c названием adoc.
Кука выставляется ручкой морды [/portal/set/any/](https://wiki.yandex-team.ru/morda/handlers/#/portal/set/any/) 

### Описание параметров ручки /portal/set/any/
- sk: секретный ключ генерируется для авторизованных пользователей по uid [алгоритм](https://wiki.yandex-team.ru/morda/sk/)
- yp_подкука = <i>adoc</i>
- формат значения куки: **expire.bannerid_timestamp_sign**
- retpath — страница, куда надо сделать редирект после выставления куки, передается с фронтэнда

### Описание формата куки
- expire — timestamp протухания куки, now + ttl
- bannerid — номер баннера в БК
- timestamp — время выставления куки
- sign — подпись, расшифровывается на стороне БК и adfox


### Алгоритм шифрования подписи
Строка <i>**expire:timestamp:yandexUid:bannerId**</i> шифруется с помощью алгоритма HmacSHA1, а затем кодируется в base64.
Ключ для подписи хранится в [секрете](https://yav.yandex-team.ru/secret/sec-01cscy8trk2gvtvqhg6bvt5682/explore/versions).<br>
Формат секрета
```json
[{"t": 1599154527, "d": "secret", "f": 1599068127},...]
```

- t — время начала действия секрета
- f — время окончания
- d — секрет

Секрет генерируется джобой в sandbox [BANNER_USER_CHOICE_GENERATE_KEY](https://sandbox.yandex-team.ru/task/758094125/view),
код джобы можно посмотреть [тут](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/yabs/BannerUserChoice/GenerateKey/__init__.py?rev=7265104#L16).
Кладется в файл `/etc/direct-tokens/bs_banner_aiming_key.txt`
