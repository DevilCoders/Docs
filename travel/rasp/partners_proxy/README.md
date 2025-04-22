partners-proxy
==============

Прокcи (3proxy) до партнеров через ipv4

Сделан аналогчно прокси Авиа https://wiki.yandex-team.ru/avia/dev/services-table/partner-proxy/

#### Сборка:

Нужно увеличить версию в pkg.json и запушить новый образ в docker-registry выполнив комманду:

```
ya package pkg.json --docker --docker-repository=rasp --docker-push
```

#### Деплой:

Указать новую версию образа в файле deploy_stage_rasp_partners_proxy.yaml.
Начать деплой командой:

```
ya tool dctl put stage deploy_stage_rasp_partners_proxy.yml
```

Проверить работоспособность можно так(должен вернуться ipv4 адрес прокси):

```
wget -e use_proxy=on -e http_proxy=http://<user>:<pass>@<host>:80 -qO- http://api.ipify.org && echo ""
```
