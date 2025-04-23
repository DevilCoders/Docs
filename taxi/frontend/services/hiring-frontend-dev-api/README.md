# Сервис автоматизации монорепы

## Хосты

* NGINX - [hiring-frontend-dev-api](/services/hiring-frontend-dev-api/etc/nginx/sites-available/hiring-frontend-dev-api.conf)
* testing - [frontend-dev-api.taxi.tst.yandex.net](http://frontend-dev-api.taxi.tst.yandex.net/)
* stable - [frontend-dev-api.taxi.yandex.net](http://frontend-dev-api.taxi.yandex.net/)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing. 

## Установка 

- `cd services/hiring-frontend-dev-api/`
- `npm run install`
- `npm run run:server:watch`

## Релиз 

[Как собирать и катитить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/)

## Дырки

[Дырки, необходмые для сервиса можно посмотреть здесь](https://puncher.yandex-team.ru?create_sources=_C_SRV_QLOUD_ROOT_&create_sources=_C_TAXI_DEV_BUILDAGENT_XENIAL_&create_sources=_GENCFG_MAN_QLOUD_MONGO_&create_sources=_GITHUBNETS_&create_sources=_STARTREK_API_PRODUCTION_NETS_&create_destinations=frontend-dev-api.taxi.yandex.net&create_protocol=tcp&create_ports=80&create_ports=443&create_comment=Перевезли%20сервис%20из%20клауда%20в%20ртц,%20нужно%20дырки%20пробить%20такие%20же:%20https://st.yandex-team.ru/INFRANAIM-5084#5f045d6b550c2255ae07c226)


## Логи 

* [Prod](https://kibana.taxi.yandex-team.ru/goto/f19cd1ff31fd79beaa1295587c75b555)
* [Testing](https://kibana.taxi.tst.yandex-team.ru/goto/36f58499d4fa6e44dc9de16247b64a6e)

## Секреты

Для старта сервера [секреты](https://yav.yandex-team.ru/secret/sec-01fbq8xgj21tew7w355zjnbwmr).
