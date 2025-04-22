# Auto Navi Tollroads

Сервис для покупки билетов на проезд по ЦКАД в Навигаторе.

Предоставляет API для мобильного приложения Навигатора.
Ещё здесь настроен VPN-клиент для хождения в API партнёров
("СВП Свободный поток", где СВП = Система взимания платы; они же &mdash; ЦКАД).

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Михаил Крутяков (mkrutyakov@yandex-team.ru) <br> Михаил Куприянов (kupriyanov-m@yandex-team.ru) |
| Отвественные SRE | Михаил Крутяков (mkrutyakov@yandex-team.ru), <br/> Михаил Куприянов (kupriyanov-m@yandex-team.ru) |
| Исходники | [maps/automotive/tollroads](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tollroads) |
| Сервис в ABC | [maps-auto-navi-toll-roads](https://abc.yandex-team.ru/services/maps-auto-navi-toll-roads/)|
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_AUTO_NAVI_TOLLROADS |
| Документация | [API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tollroads/docs/README.md)<br/>[DB Schema](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tollroads/docs/db.sql)|


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Prestable | [maps_auto_navi_tollroads_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_prestable/) | [ auto-navi-tollroads.prestable ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-tollroads-prestable-panel-main/) | [ maps_auto_navi_tollroads_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_tollroads_prestable) |
| Stable | [maps_auto_navi_tollroads_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_stable/) | [ auto-navi-tollroads.stable ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-tollroads-stable-panel-main/) | [ maps_auto_navi_tollroads_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_tollroads_stable) |
| Testing | [maps_auto_navi_tollroads_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_testing/) | [ auto-navi-tollroads.testing ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-tollroads-testing-panel-main/) | [ maps_auto_navi_tollroads_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_tollroads_testing) |
| Stress | [maps_auto_navi_tollroads_stress](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_stress/) | [ auto-navi-tollroads.stress ](https://yasm.yandex-team.ru/template/panel/maps-auto-navi-tollroads-stress-panel-main/) | [ maps_auto_navi_tollroads_stress ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_auto_navi_tollroads_stress) |


[Monitorings all (tag=a_prj_maps-auto-navi-tollroads)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-auto-navi-tollroads)

| Staging | Ratelimiter | PostgreSQL |
| ------- | ----------- | ---------- |
| *       | [RPS and Quotas](https://yasm.yandex-team.ru/template/panel/maps_auto_navi_tollroads-ratelimiter2-panel/)| - |
| Testing |  - | [maps-auto-navi-tollroads-testing](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb5uu3t2ujog6unpabr) |
| Stable | - | [maps-auto-navi-tollroads-stable](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=mdb72e52vq9karnjsa64) |

Сервис использует общий S3 Навигатора для хранения данных по РВП:
- [Репозиторий](https://bb.yandex-team.ru/projects/NAVI/repos/navi_s3/browse)
- Testing Bucket: yandexnavi-testing, [toll_road_checkpoints.json](https://yandexnavi-testing.s3.yandex.net/toll_road_checkpoints/test/toll_road_checkpoints.json)
- Stable Bucket: yandexnavi, [toll_road_checkpoints.json](https://yandexnavi-testing.s3.yandex.net/toll_road_checkpoints/prod/toll_road_checkpoints.json)

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable | Default | [auto-navi-tollroads.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-navi-tollroads.maps.yandex.net/) | [auto-navi-tollroads.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-navi-tollroads.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=auto-navi-tollroads-maps;signal=service_total) | [rtc_balancer_auto-navi-tollroads_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-tollroads_maps_yandex_net_man)<br>[rtc_balancer_auto-navi-tollroads_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-tollroads_maps_yandex_net_sas)<br>[rtc_balancer_auto-navi-tollroads_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-tollroads_maps_yandex_net_vla) |
| Testing | Default | [auto-navi-tollroads.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/auto-navi-tollroads.testing.maps.yandex.net/) | [auto-navi-tollroads.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=auto-navi-tollroads.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=sas,vla,man;prj=auto-navi-tollroads-testing-maps;signal=service_total) | [rtc_balancer_auto-navi-tollroads_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-tollroads_testing_maps_yandex_net_man)<br>[rtc_balancer_auto-navi-tollroads_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-tollroads_testing_maps_yandex_net_sas)<br>[rtc_balancer_auto-navi-tollroads_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_auto-navi-tollroads_testing_maps_yandex_net_vla) |


## What happens when service is down

Пользователи больше не могут оплачивать проезд по ЦКАД из Навигатора

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/auto-tollroads/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'auto-navi-tollroads.maps.yandex.net' limit 1; |
| OpenVPN | /var/log/openvpn/* |

## OpenVPN

### Общие сведения про конфигурацию VPN

Для работы с API ЦКАД у нас настроен клиент OpenVPN.
- Конфиг лежит в [/etc/openvpn/client/ya-sft.ovpn](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tollroads/docker/install/etc/template_generator/templates/etc/openvpn/client/ya-sft.ovpn).
- Ключи и пароли хранятся в Vault, секрет [maps-auto-navi-tollroads-openvpn](https://yav.yandex-team.ru/secret/sec-01enqx42z8ntkn1zhb237s7d89/explore/versions).
  Кладутся в директорию /etc/openvpn/keys.
- OpenVPN запускается при помощи supervisorctl: [/etc/supervisor/conf-available/openvpn.conf](https://a.yandex-team.ru/arc_vcs/maps/automotive/tollroads/docker/install/etc/supervisor/conf-available/openvpn.conf)

Для подключения используем NAT64, выставляем префикс `64:ff9b::185.68.23.1`, где `185.68.23.1` &mdash; IP-адрес
VPN-сервера ЦКАД. Порт `1194`.

Нам выдано 10 ключей: ya-sft (без номера), ya-sft-1, ..., ya-sft-9. Ключи распределены по машинкам с помощью bash-скрипта:
[/etc/runner/run.d/20_openvpn_certificates.sh](https://a.yandex-team.ru/arc_vcs/maps/automotive/tollroads/docker/install/etc/runner/run.d/20_openvpn_certificates.sh)
По факту каждая машинка (всего их 9) использует свой ключ.

У партнёров включен режим `duplicate-cn`, так что использование одного ключа на нескольких машинках
в принципе допустимо, хоть и не является чем-то желательным. Также у них работает DHCP, рассчитанный
как минимум на 9 подключений (36 адресов, по 4 адреса на подключение, почему так читай тут:
[/30 subnet in TUN mode](https://community.openvpn.net/openvpn/wiki/273-qifconfig-poolq-option-use-a-30-subnet-4-private-ip-addresses-per-client-when-used-in-tun-mode) и
[Topology net30](https://community.openvpn.net/openvpn/wiki/Topology#Topologynet30)
). Возможно, получится подключить и больше, но никто не пробовал. И договаривались мы только про 9.

В последний раз нам выдавали IP-адреса из следующих подсетей:

- 172.25.209.4/30
- 172.25.209.8/29
- 172.25.209.16/29
- 172.25.209.60/30
- 172.25.209.64/29
- 172.25.209.72/30

От их VPN-сервера нам приходят (через PUSH-сообщение OpenVPN):
- Выданные через DHCP адреса (2 шт., например 172.25.209.5 и 172.25.209.6)
- DNS (77.88.7.3, 8.8.8.8)
- IPv4 маршруты до их сетей (10.20.12.0/24, 10.20.20.0/24)

Мы игнорируем настройки DNS и приходящие маршруты. Маршруты прописываются с помощью нашего же скрипта
[/etc/openvpn/setuproute.sh](https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/tollroads/docker/install/etc/template_generator/templates/etc/openvpn/setuproute.sh).
Делаем это из соображений безопасности и надёжности (чтобы нам не прислали странного).

Нормальная картина для маршрутов такая
(здесь 172.25.209.10 - выданный нам адрес, будет отличаться на разных машинках):
```
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
10.20.12.0      172.25.209.10   255.255.255.0   UG    0      0        0 tun0
10.20.20.0      172.25.209.10   255.255.255.0   UG    0      0        0 tun0
172.16.0.0      172.25.209.10   255.240.0.0     UG    0      0        0 tun0
172.25.209.10   0.0.0.0         255.255.255.255 UH    0      0        0 tun0
```

### Как чинить VPN

Как проверить, что VPN работает (и отлаживать, если не работает):
- Выполнить `ifconfig` и посмотреть, есть ли интерфейс tun0.
- `ping 10.20.20.10` или `traceroute 10.20.20.10`, чтобы проверить корректность настроек маршрутизации
- Проверить, запущен ли OpenVPN с помощью `supervisorctl status openvpn`
- Посмотреть логи OpenVPN в /var/log/openvpn/openvpn.log
- Проверить, прописались ли ключи с помощью:
  ```
  ls -l /etc/openvpn/keys/chosen*
  lrwxrwxrwx 1 root root 135 Nov 23 17:49 /etc/openvpn/keys/chosen-tollroads-client.crt -> /place/db/iss3/instances/maps-auto-navi-tollroads-testing-1_maps_auto_navi_tollroads_testing_rDH5UappyjG/secrets/tollroads-client-1.crt
  lrwxrwxrwx 1 root root 135 Nov 23 17:49 /etc/openvpn/keys/chosen-tollroads-client.key -> /place/db/iss3/instances/maps-auto-navi-tollroads-testing-1_maps_auto_navi_tollroads_testing_rDH5UappyjG/secrets/tollroads-client-1.key
  lrwxrwxrwx 1 root root 130 Nov 23 17:49 /etc/openvpn/keys/chosen-tollroads-client-password.txt -> /place/db/iss3/instances/maps-auto-navi-tollroads-testing-1_maps_auto_navi_tollroads_testing_rDH5UappyjG/secrets/ya-password-1.txt
  ```
  Должно быть три симлинка: chosen-tollroads-client.crt, chosen-tollroads-client.key, chosen-tollroads-client-password.txt.
  Если не прописались, можно проставит их вручную на любой ключ из /etc/openvpn/keys
  (главное, чтобы номер у сертификата, ключа и пароля совпадал). Примерно вот так:
  ```bash
  ln -sf $SWD/secrets/tollroads-client-1.crt /etc/openvpn/keys/chosen-tollroads-client.crt
  ln -sf $SWD/secrets/tollroads-client-1.key /etc/openvpn/keys/chosen-tollroads-client.key
  ln -sf $SWD/secrets/ya-password-1.txt /etc/openvpn/keys/chosen-tollroads-client-password.txt
  ```
- Если VPN не работает, можно попробовать выполнить `supervisorctl restart openvpn`
- Если VPN отваливается с ошибкой `AUTH: Received control message: AUTH_FAILED`, вероятно проблема
  в том, что у DHCP ЦКАД закончились IP-адреса. Либо на нашей стороне запущено больше 9 машинок,
  либо они поменяли конфигурацию на своей стороне. Проблему необходимо решать совместно с сетевыми
  инженерами ЦКАД.
- Проверить, есть ли интерфейс tun на машинке: `ls /dev/net`. Если нет, надо переаллоцировать поды,
  включив в разделе "Advanced settings" настройку "/dev/net/tun device in pod" в положение "Enable".
- Вручную можно запускать так (для отладки, например):
  ```
  openvpn --config /etc/openvpn/client/ya-sft.ovpn
  ```

## How to fix common problems

- [What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)
- **openvpn-ping**, **openvpn-running**, **openvpn-connected** &mdash; про отладку проблем с OpenVPN
  см. соответствующий [раздел](#как-чинить-vpn) этого Readme.
- **hanged-orders** &mdash; заказ долгое время висит в неоплаченном состоянии.
  Скорее всего, требует изучения со стороны разработчиков сервиса (или людей из Оплаты).
- **tskad-api** &mdash; что-то пошло не так в API партнёров. Может починиться "само".
  Если не починилось, надо связываться с ними, контакты есть у разработчиков сервиса.
- **orders-handle-failure** &mdash; не удалось обработать заказ, надо смотреть логи.
- **orders-payment-api-failure** &mdash; скорее всего, ошибка API Оплат.
  Надо смотреть логи + стучаться в их поддержку.
- **orders-active-ticket-failure** &mdash; оплата завершилась с ошибкой после получения билета на проезд в ЦКАД.
  Так быть не должно. Надо смотреть логи и просить товарищей из Оплат помочь.
- **orders-completed-cancel**, **orders-completed-failure** &mdash; наш флоу не предполагает
  ни отмен, ни провалов заказов. Если что-то такое произошло, это требует дальшейших разбирательств.
- **datasync-save-failure** &mdash; не удалось сохранить заказ в Datasync.
  Можно подождать пару минут, возможно починится само.
  Если не починилось, надо читать логи/звать разработчиков/писать в поддержку Datasync.

Контакты:
- [ABC Оплат](https://abc.yandex-team.ru/services/pay) (есть ссылка на Telegram-чатик поддержки)
- [Дежурства Оплат](https://wiki.yandex-team.ru/mail/swat/#anchor-duty)
- [Чат поддержки Оплат](https://t.me/joinchat/AA90WB0o6d2Ua4m4CJcYrw)
- [Чат поддержки Datasync](https://t.me/joinchat/Dd--B0fE9-g9XFl7BVMnLQ)

## Documentation

- [Дизайн-ревью](https://wiki.yandex-team.ru/automotive/serverdevelopment/toll-roads-navi/design-review/)

## Known clients
- Приложение Навигатора (виджет оплаты ЦКАД)

## SLA

[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/????) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/???.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log

## YP pods

| Staging | YP Pod |
| ------- | ------ |
| Prestable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_prestable/yp_pods/ |
| Stable | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_stable/yp_pods/ |
| Testing | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_testing/yp_pods/ |
| Stress | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_auto_navi_tollroads_stress/yp_pods/ |


## Firewall macroses

| staging | URL |
|---|---|
| stable | [ \_MAPS_AUTO_NAVI_TOLLROADS_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_NAVI_TOLLROADS_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_AUTO_NAVI_TOLLROADS_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_AUTO_NAVI_TOLLROADS_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/YCARBACKEND?service=maps-auto-navi-tollroads
    * Sandbox (line): https://sandbox.yandex-team.ru/scheduler/43200
    * Sandbox (const): https://sandbox.yandex-team.ru/scheduler/43201
    * Тикет: https://st.yandex-team.ru/YCARBACKEND-642
