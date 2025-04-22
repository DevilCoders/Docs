### Блокировка пользователей по IP

После переезда на [сервисный балансер](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps.slb.maps.yandex.net/show/) AWACS, появилась возможность блокировать пользователей по IP адресу на балансере. Для этого надо сделать следующие шаги:

1. В upstream [ban_by_ip](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps.slb.maps.yandex.net/upstreams/list/ban_by_ip/show/) добавить следующую секцию:

```
  - match_fsm:
      header:
          # <PUT REASON HERE>
          name: X-Forwarded-For-Y
          value: <PUT IPv4 or IPv6 HERE>
```

2. Убедиться что все [секции](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-maps.slb.maps.yandex.net/upstreams/list/) провалидировалсь и доехала до прода. Статус `Active` у всех равен `true`
3. Зайти на [БЯК](https://yandex.ru/maps) и убедиться, что он открывается
