# olap2-tableau-scripts
## sync_users.py
Синхронизация лицензий юзеров с сотоянием в БД olap2-etl (лицензии управляются через https://wiki.yandex-team.ru/market/projects/marketstat/olap2etl/dostupy/#dobavlenienovojjlicenzii).

Этот скрипт сейчас "поставлен" руками на `cubes01h:/usr/local/bin/sync_users.py` и запускается по крону раз в 5 минут под рутом. Скрипт запускается в venv `/root/venv`. В этом venv стоит либа tableauserverclient, **которой не рекомендуется пользоваться**. Вместо неё лучше ходить в tableau rest API через requests, или даже курлом из баша.

2019.10.21 табло перешло на https, поэтому пришлось подсунуть наш внутренний сертификат allCAs.pem в питон. Для это пришось в venv поставить пакет `source /root/venv/bin/activate && /root/venv/bin/pip install urllib3[secure]`, и перед каждым запуском скрипта устанавливать переменную `export REQUESTS_CA_BUNDLE=/etc/nginx/keys/allCAs.pem`. Я прописал этот экспорт в `/root/.bashrc`.

Конфиг крона выглядит так:
```
*/5 * * * * export REQUESTS_CA_BUNDLE=/etc/nginx/keys/allCAs.pem; /root/venv/bin/python /usr/local/bin/sync_users.py 2>&1 | tee -a /var/log/yandex/tableau_sync_users.log
```


## load
Скрипты для переливки юзеров, групп и расписаний из одного табло в другое.



## market-tableau-scripts
Скрипты мониторинга и бекапа табло, которые запаковываются в deb-пакет и ставятся на главную ноду табло.



https://wiki.yandex-team.ru/Market/projects/marketstat/support/tableau/
