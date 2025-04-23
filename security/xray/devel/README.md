# Разворачиваем X-Ray в QYP

X-Ray не самый приятный сервис для разворачивания, т.к. требует множества подвижных частей.
Необходимые зависимости:
  - nginx
  - [smug](https://github.com/ivaaaan/smug)
  - [porto](https://wiki.yandex-team.ru/porto/)
  - [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/)
  - [dev секретики](https://yav.yandex-team.ru/secret/sec-01fshbkcr7rgsdn6m86616qbrs)
  - QYP виртуалка в сети `_SECURITY_MTN_NETS_`

1. Для начала, создадим папочку со всем нужным барахлом и слинкуем туда конфиги:
```
$ sudo mkdir -p /srv/xray
$ sudo chown $USER /srv/xray
$ ln -sf $(pwd)/configs /srv/xray
```
2. Копируем `./configs/.env.example` -> `/srv/xray/.env`, добавив значения секретиков из [yav](https://yav.yandex-team.ru/secret/sec-01fshbkcr7rgsdn6m86616qbrs)
3. Сохраняем сертификат из [yav](https://yav.yandex-team.ru/secret/sec-01fshbkcr7rgsdn6m86616qbrs) в `/srv/xray/certs/www.pem`
4. Соберем все бинарники запуском `make`
5. Линкуем конфиг для smug и стартуем все наше безобразие:
```
$ mkdir -p ~/.config/smug
$ ln -sf $(pwd)/smug.yml ~/.config/smug/xray.yml
$ smug start xray --attach
```

Если все прошло норм и все стартануло - то фуф!

Теперь на клиенте правим `/etc/hosts`, добавив туда запись для `xray-dev.sec.yandex-team.ru` и можно пользоваться :)
Например, зашедулим проверку стейджа `kirby-stage`:
```
$ export XRAY_TOKEN=<любой oauth-token>
$ /srv/xray/bin/xray-cli stage schedule --force --id kirby-stage --latest --wait --addr localhost:3000 --insecure
```
