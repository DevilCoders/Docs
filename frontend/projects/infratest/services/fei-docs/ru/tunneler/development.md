# Tunneler. Документация разработчика

## Общая схема работы Tunneler

В настоящее время доступны две версии:

- **v1 (tunneler-ws)** – инсталляция для поднятия туннелей на рабочих станциях разработчиков.
- **v2 (tun)** – инсталляция для поднятия туннелей в CI.

Обе версии поддерживаются в актуальной версии клиента. Различия заключаются в способе балансировки трафика и "привязки" туннелей к серверам ssh-фермы.

Вместо тысячи слов:
![](./images/components.png)

### Балансер

{% note info "Ссылки" %}

- [Сервис в awacs](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/show/)
- [Панели мониторингов](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/monitoring/common/)
- [Алерты в juggler](https://juggler.yandex-team.ru/project/awacs.tun/dashboard?project=awacs.tun)

{% endnote %}


Почти обычный awacs-балансер. Конфигурируется в апстримах:

- [tunnels](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/upstreams/list/tunnels/show/) для ci-фермы
- [tunnels-ws1](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/upstreams/list/tunnels-ws1/), [tunnels-ws2](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/upstreams/list/tunnels-ws2/), [tunnels-ws3](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/upstreams/list/tunnels-ws3/) для ws-ферм

#### Как грепать логи балансера

Логи удобнее грепать через [sky run](https://doc.yandex-team.ru/Search/skynet-dg/concepts/sky-run.html)

```
sky run --stream 'grep <username> /logs/current-access_log-balancer-443' yp@rtc_balancer_tun_man yp@rtc_balancer_tun_sas yp@rtc_balancer_tun_vla
```

или [executer](https://wiki.yandex-team.ru/executer)

```
p_exec n:rtc_balancer_tun_sas,n:rtc_balancer_tun_vla,n:rtc_balancer_tun_man grep '<username>' /logs/current-access_log-balancer-443
```

#### Как найти sandbox-таску по логам балансера

В запросе, который вас волнует, можно увидеть, на какой под tun был спроксирован запрос:

```
[2a02:6b8:c01:b73:0:522:c938:9104]:41910 2021-08-18T20:00:52.576932+0300 "GET /static/web/app.js HTTP/1.1" 0.121404s "https://man-o7o74sm7m2lvml5g-24980-yp.tun2.yandex.ru/chat" "man-o7o74sm7m2lvml5g-24980-yp.tun2.yandex.ru" [report u:service_total [cookie_policy u:service_total [regexp default [log_headers <::X-Forwarded-For:2a02:6b8:c01:b73:0:522:c938:9104::> <::X-Req-Id:1629306052576932-7026138019633667709::> [regexp default [regexp_host tun2-testing [regexp tunnels [proxy o7o74sm7m2lvml5g.man.yp-c.yandex.net:24980 0.121026s/0.121179s 0/240 succ 304]]]]]]]]
```

Часть `proxy o7o74sm7m2lvml5g.man.yp-c.yandex.net:24980` здесь указывает на то, в какой хост и порт Tunneler был сделан запрос. Теперь нужно выяснить, с какого IP было инициировано поднятие туннеля.

Для этого идем в [логи tun](https://deploy.yandex-team.ru/stages/tun/logs) и ищем там следующее:

```
pod=o7o74sm7m2lvml5g; context.bindPort=24980; message="tunnel_open"
```

Кликнув на интересующую вас запись в логе, вы увидите расширенный json-лог, в котором будет такое:

```
"context": {
  "bindPort": 20059,
  "connectionId": "01FDDCNXMAYSETXR1Q1RBZPR9A",
  "clientIp": "2a02:6b8:c01:685:0:522:4bd5:631a",
  "pid": 11
}
```

Здесь `clientIp` — это ip sandbox-агента. Осталось выяснить, какая задача на нём выполнялась в это время. В этом нам поможет sandbox audit:

```
curl 'https://sandbox.yandex-team.ru/api/v1.0/task/audit?since=2021-08-18T16:00:00.000Z&to=2021-08-18T19:00:00.000Z&remote_ip=2a02:6b8:c01:685:0:522:4bd5:631a'
```

В `since` и `to` поставьте дату, которая вас интересует, а в `remoteIp` — `clientIp` из логов tun. В ответе вы увидите задачи, выполнявшиеся в это время на этом поде.

### tunneler-ws

{% note info "Ссылки" %}

- [Сервис в Deploy](https://deploy.yandex-team.ru/stages/tunneler-ws)
- [Панель мониторингов](https://deploy.yandex-team.ru/stages/tunneler-ws/monitoring)
- [Исходный код](https://github.yandex-team.ru/search-interfaces/tunneler-legacy)

{% endnote %}

Клиент использует один из доступных API серверов для получения адреса сервера SSH:

```
curl https://ws{1,2,3}-tunnelerapi.tunneler-si.yandex-team.ru/api/v1/instances
```

По умолчанию сервер выбирается на основе логина пользователя, а в случае недоступности используется следующий по хэшрингу.

Через выбранный инстанс поднимается туннель на случайном или явно указанном порту. После поднятия туннеля можно ходить по url вида `{login}-{tunnel-port}-ws{1,2,3}.tunneler-si.yandex.ru`, запросы будут проксироваться в туннель.

{% note warning "Внимание!" %}

Номер инстанса изменять нельзя. В url он должен соответствовать инстансу, на котором поднимался туннель.

{% endnote %}

#### Детали реализации и ограничения

- Примечание выше накладывает существенные ограничения на масштабирование инсталляции, так как балансер должен знать о каждом инстансе ssh-сервера.

- Дополнительно ситуация усугубляется тем, что за одним инстансом должен стоять ровно один под, на котором поднято SSH соединение.

- Для "красивых" url с логином приходится использовать двойной reverse proxying – сначала на L7 балансере, затем на самом SSH сервере, для возможности определения соединения по логину из url. В итоге HTTP запрос проходит следующий путь:

```
tunnel endpoint > L7 balancer > tunneler [ HTTP proxy > unix socket > SSH tcp-forward channel ] > tunnel endpoint
```

### tun

{% note info "Ссылки" %}

- [Сервис в Deploy](https://deploy.yandex-team.ru/stages/tun)
- [Панель мониторингов](https://deploy.yandex-team.ru/stages/tun/monitoring)
- [Алерты в juggler](https://juggler.yandex-team.ru/project/fei.tun/dashboard?project=fei.tun)
- [Исходный код](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/tun)

{% endnote %}

Клиент получает доступные инстансы из API:

```
curl https://tun.si.yandex-team.ru/api/v2/instances
```

Затем на случайно выбранном и доступном поде клиент поднимает туннель на случайном порту. После поднятия туннеля можно ходить на url вида `{dc}-{ident}-{tunnel-port}-yp.tun.si.yandex.ru`, запросы будут проксироваться в туннель. Клиент выбирает `dc` и `ident` на основе ответа API ручки. На стороне балансера hostname будет транслирован в service discovery FQDN пода в YP и проксироваться прямо в туннель.

## Исходный код

- [Сервер (tun)](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/services/tun)
- [Сервер (tunneler-ws)](https://github.yandex-team.ru/search-interfaces/tunneler-legacy)
- [Клиент](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/tunneler)
- [Archon-компонент](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/archon-tunneler)

## Docker образы

- `registry.yandex.net/search-interfaces/tun`
- `registry.yandex.net/search-interfaces/tunneler-legacy`

## Секреты

- [Приватный ключ хоста](https://yav.yandex-team.ru/secret/sec-01dvrcbg8bzdc6n5q6e1hvkt7c). Требуется для поднятия SSH сервера.

## Мониторинги и алерты

{% note info "Мониторинги" %}

- [Панели балансера](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tun/monitoring/common/)
- [Панель tun](https://deploy.yandex-team.ru/stages/tun/monitoring)
- [Панель tunneler-ws](https://deploy.yandex-team.ru/stages/tunneler-ws/monitoring)

{% endnote %}

{% note info "Алерты" %}

- [Все алерты в yasm](https://yasm.yandex-team.ru/template/panel/fei-alerts/abc=tun/)
- [Алерты балансера в juggler](https://juggler.yandex-team.ru/project/awacs.tun/dashboard?project=awacs.tun)
- [Алерты tun в juggler](https://juggler.yandex-team.ru/project/fei.tun/dashboard?project=fei.tun)

{% endnote %}

### Достаточное количество живых подов tun

Этот алерт загорается, когда число живых инстансов [tun](https://deploy.yandex-team.ru/stages/tun) уменьшается.

Алерт может загораться при учениях, регламентных работах (об этом оповещают заранее) и авариях в ДЦ (искать major события [в infra](https://infra.yandex-team.ru/timeline?preset=all&status=all&types=major_issue)). Тогда это нормальная деградация.
Если алерт загорается без видимых проблем в ДЦ, надо посмотреть, почему инстансы ушли, какая доля, и восстановились ли они.
