# Фронтенд vertis-partner.yandex.ru

## Основная информация

| Service | URL |
|---|---|
| TeamCity | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Fvertis-partner-www&id=vertis-partner-www |
| Deploy | https://admin.vertis.yandex-team.ru/services/vertis-front-partner |
| Logs | https://grafana.vertis.yandex-team.ru/explore?orgId=1&left=%5B%22now-1h%22,%22now%22,%22vertis-logs%22,%7B%22expr%22:%22service%3Dvertis-front-partner%22,%22fields%22:%5B%22thread%22,%22context%22,%22message%22,%22rest%22%5D,%22limit%22:100%7D%5D |
| Графики | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?orgId=1&var-datasource=Prometheus&var-job=vertis-front-partner&var-allocation_id=All&var-rate=2m |
| Секреты | https://yav.yandex-team.ru/?tags=vertis-partner |

## Хосты

| Environment | URL |
|---|---|
| Testing | https://partner.realty.test.vertis.yandex.ru <br> https://branch-${branch}.partner.realty.test.vertis.yandex.ru <br> https://partner.rabota.test.vertis.yandex.ru <br> https://branch-${branch}.partner.rabota.test.vertis.yandex.ru |
| Production | https://partner.realty.yandex.ru <br> https://partner.rabota.yandex.ru |

## Быстрый старт

1. Разрабатываться можно только на дев виртуалке. [Как заказать](https://wiki.yandex-team.ru/vertis-admin/dev-containers/).
1. Для проброса ssh-агента добавляем в ~/.ssh/config. Поменяй логин на свой!
```
Host yandex_vertis
    HostName fresk-01-dev.sas.yp-c.yandex.net
    User fresk
    ForwardAgent yes
    IdentityFile ~/.ssh/id_rsa
    SendEnv LANG LC_*
```
1. Настраиваем виртуалку
```bash
ssh yandex_vertis
apt-get install nodejs-14=14.18.1-1 nginx yandex-vertis-nodejs-init apt-transport-https
mkdir www
```
1. Генерируем сертификат на [crt](https://crt.yandex-team.ru/certificates/?cr-form=1).
Вбиваем следующие хосты:
```
partner.realty.vp-<login>.<login>.dev.vertis.yandex.ru,
partner.rabota.vp-<login>.<login>.dev.vertis.yandex.ru
```
Качаем `.pem` сертификат и кладем в `/etc/nginx/keys/cert.pem`
```
exit
scp ~/Downloads/partner.realty.vp-fresk.fresk.dev.vertis.yandex.ru.pem yandex_vertis:/tmp
ssh yandex_vertis
sudo mkdir /etc/nginx/keys
sudo mv /tmp/partner.realty.vp-fresk.fresk.dev.vertis.yandex.ru.pem /etc/nginx/keys/cert.pem
```
1. Клонируем репозиторий и запускаем проект
```
cd www
git clone git@github.com:YandexClassifieds/vertis-partner-www.git vp
cd vp
make npm.get
SECRETS_ENV_PATH=.env.secrets /opt/nodejs/14/bin/node node_modules/.bin/secrets-to-dotenv
make
sudo systemctl restart nginx
```

nodejs запустился в фоновом режиме. Теперь можно открыть в браузере `https://partner.realty.vp-<login>.<login>.dev.vertis.yandex.ru`

### Аккаунты для тестирования
```
Admin  uid:292685114 auto:28026029 tours:28026030 drvr01:drvr02
Agency uid:306541088 auto:28026031 tours:28026032 drvr02:drvr03
Client uid:306541137 auto:28026033 tours:28026034 drvr03:drvr04
```

## Пересборка рабочей копии

### Что делать, если я добавил/удалил/поправил файл в node.js-коде
Как правило ничего.
В крайнем случае `make restart`.

### Что делать, если я добавил/удалил файл или поправил `deps.js` в `blocks-*`
`make enb-make`

### Что делать, если я отредактировал существующий файл в `blocks-*`
 * `priv.js` — `make privs` быстро
 * `bemhtml` — `make enb-make` медленно :(
 * `*.css`/`*.js` — ничего :)
