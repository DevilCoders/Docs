# Core ST monitor

Инструмент, повышающий прозрачность процесса дежурств

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Вадим Мазаев (vmazaev@yandex-team.ru) <br> Иван Селезнев (imseleznev@yandex-team.ru) |
| Отвественные SRE | Вадим Мазаев (vmazaev@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/st_monitor |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-st-monitor/ |
| CI (TestEnv) - Покоммитный | https://beta-testenv.yandex-team.ru/project/maps_tests/job/BUILD_DOCKER_MAPS_CORE_ST_MONITOR/history?limit=12 |

## Service infrastructure

### Instances

| Stage | Deploy project |
| ------- | ------------- |
| Stable | [maps-core-st-monitor-stable](https://deploy.yandex-team.ru/project/maps-core-st-monitor-stable) |

### Balancers

| Staging | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | -------------- | -------------- | ----------------------- |
| Stable | [core-st-monitor.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-st-monitor.maps.yandex.net/) | [core-st-monitor.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-st-monitor.maps.yandex.net;itype=balancer;ctype=prod;metaprj=balancer;prj=core-st-monitor-maps;signal=service_total) | [rtc_balancer_core-st-monitor_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-st-monitor_maps_yandex_net_vla)<br>[rtc_balancer_core-st-monitor_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-st-monitor_maps_yandex_net_vla) |

## What happens when service is down

Дежурные не получают ссылки на тикеты по сработавшим мониторингам, не могут поставить даунтайм через тикет и т.п.

## Logs
| Name | URL/path |
|---|---|
| stdout (access-log) | ./st-monitor-workload_stdout.portolog |
| stderr (error-log) | ./st-monitor-workload_stderr.portolog<br>st_monitor.log |
| YT (access-log) | https://yql.yandex-team.ru<br>```USE arnold; SELECT * FROM `logs/deploy-mvp-test-log/1d/` WHERE stage = "maps-core-st-monitor-stable";``` |

## Documentation

### Как собрать докер-образ локально
0. Настроить докер на машине, где будет производиться сборка (например, по [этой интрукции](https://wiki.yandex-team.ru/users/vmazaev/docker-v-QYP/))
1. Из директории с докер-образом выполнить: `ya package pkg.json --docker --docker-push --docker-repository maps [--custom-version <version-name>]`

### Как запустить бота в дебаг-режиме
0. Собрать бинарник
1. Запустить со следующими ключами:
    - `--debug` - запускать бота в поллинг-режиме коннекта к телеграму: будет отзываться на кнопки в телеграме, но
      события от стартрека все еще нужно отправлять curl'ом (по-умолчанию в этом режиме на 5000-й порт)
    - `--oauth-token` - токен для походов в startrek, juggler, staff (подойдет токен от sedem'а)
    - `--telegram-token` - телеграм-токен от бота, добавленного в чаты, на которых планируется тестирование. Не используйте телеграм-токен прода.
    - `--slack-token` - Slack-токен от бота, добавленного в чаты, на которых планируется тестирование. Не используйте Slack-токен прода.
    - `--sign-key test` - "соль" для подписи кнопок в телеграме, бот будет отвечать только на те кнопки, которые подписаны с данной "солью"
    - `--no-proxy` - (опционально) не проксировать события в Подрика (фронтендовский бот для мониторинга)
    - `--no-gc` - (опционально) не запускать бэкграунд тред, автоматически снимающий даунтаймы c мониторингов, у которых закрыли тикет

```
./st_monitor --debug --no-proxy --no-gc --oauth-token XXX --telegram-token XXX --sign-key test
```

## Known clients

Дежурные бэкенда и фронтенда Карт

## Firewall macros
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_ST_MONITOR_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_ST_MONITOR_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_ST_MONITOR_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_ST_MONITOR_TESTING_RTC_NETS_ ) |

## Production secrets

**N.B. Не используйте продакшн-токены при тестировании**

[Telegram token](https://yav.yandex-team.ru/secret/sec-01dkvdrcatst3qfm8d4e82mh8h)

[Slack token](https://yav.yandex-team.ru/secret/sec-01f0ewxqdn0mrarww4sjf6tw0h)
