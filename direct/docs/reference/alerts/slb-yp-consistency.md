# slb-yp_consistency

[Примеры проверок](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Ddirect.prod%26service%3Dslb-yp_consistency).

## Oписание { #description }
L3 балансер работает с IP адресами реалов, а не FQDN. В момент выкладки конфигурации, происходит преобразование имён ман в IPv4/IPv6 адрес. Поэтому когда контейнер(реал) переезжает, балансер теряет с ним связь и требуется обновить конфигурацию.

{% note info %}

В этом месте ожидаемо нет автоматики со стороны балансера, такова политика NOC.  
Должна быть автоматика со стороны риалов (и мы её получим при переходе на awacs), поэтому сами не делаем (возможно пока).

{% endnote %}

## Диагностика { #diagnostics }
Идем на ppcback01f/01e/01i сервер и смотрим лог `/var/log/dt-l3-yp/dt-l3-yp.py.log`. 

Скрипт `dt-l3-yp.py` отвечает за сверку ip адресов, полученных из Nanny/Conductor и API L3 балансера. Пример расхождения:
```text
2020-07-31 04:01:24,774 slb id:3505[vs: 2537352](fqdn: api.direct.yandex.com,api.direct.yandex.ru port 443),nanny: Ok, no diff
2020-07-31 04:01:24,775 slb id:3505[vs: 2537352](fqdn: api.direct.yandex.com,api.direct.yandex.ru port 443),conductor groups: ['direct_soap']: Ok, no diff
2020-07-31 04:01:24,775 Hosts diff: 
2020-07-31 04:01:24,775 --- slb id:3505[vs: 2537352](fqdn: api.direct.yandex.com,api.direct.yandex.ru port 443)
2020-07-31 04:01:24,775 +++ Resolved conductor groups: ['direct_soap']
2020-07-31 04:01:24,775 - 2a02:6b8:c1d:2091:0:648:18d9:0
2020-07-31 04:01:24,775 + 2a02:6b8:c1f:d94:0:648:15fb:0
2020-07-31 04:01:24,775 ------------------------------
```

Удобная команда получения списка ссылок на L3 Manager для балансеров, требующих внимания по логу за сегодня:
```sh
grep `date +"%Y-%m-%d"` /var/log/dt-l3-yp/dt-l3-yp.py.log | grep '++ Resolved conductor groups' -B1 | perl -ne '/slb id:(\d+)/ && print "https://l3.tt.yandex-team.ru/service/$1\n";' | sort | uniq
```

## Решение { #solution }
Обновляем список реалов в L3 Manager.

1. Идем в веб [L3 Manager](https://l3.tt.yandex-team.ru/service) и ищем указанный сервис.
   Альтернативный способ: подставить `slb id` в URL `https://l3.tt.yandex-team.ru/service/<slb id>`
1. Находим **Active** правило и заходим в него (щелкнуть по нему)
1. Вверху справа будет кнопка **Update RS Groups**: **Update RS Groups** → **Save changes**, затем **Deploy**
1. Ждем несколько минут пока выложится. Если все прошло успешно, то в **Active** будет отображаться полный список реалов (например, `RS states 80/80`).


## Полезное { #tips }
Для ускорения позеленения мониторинга обноление которого происходит редко, можно воспользоваться следующим заклинанием c ppcback-а:
```bash
sudo -u ppc -i
OAUTH=$(cat /etc/direct-tokens/l3api_oauth_robot-direct-admin) switchman -c /etc/directadmin-switchman.conf -g ppcback --lockname slb-consistency --delay 6 -- dt-l3-yp.py -vv
```
