---
title: Поставка логов awacs
---

## Описание
Логи awacs балансеров по дефолту никуда не поставляются. Можно только сделать поставку в YT по [инструкции](https://wiki.yandex-team.ru/awacs/logs/#gdechitatlogi).  
Для балансеров Travel настроена постака логов в YT и ClickHouse по [инструкции](https://wiki.yandex-team.ru/users/nikshel/awacs-balancer-logs/).
1) С инстансов балансеров логи поставляются в топики Logbroker
2) Из топиков логи поставляются в YT и ClickHouse
3) Логи в ClickHouse можно смотреть через ClickHouse Viewer и YQL

После настройки поставки в Logbroker логи автоматически будут выгружаться в ClickHouse.  
TTL записей в ClickHouse - 168 часов(неделя).  
Примеры:
 - [ClickHouse Viewer](https://travel-production-awacs-access-log.chv.yandex-team.ru/dashboard?componentSettings=%7B%22charts%22%3A%7B%22autoRefresh%22%3Atrue%2C%22columns%22%3A%5B%22chart_rps%22%5D%7D%7D&filter=domain%20%3D%3D%20api.rasp.yandex.net%20AND%20status%20%3D%3D%20200%20AND%20upstream%20%3D%3D%20rasp-api-public-production.upstream&period=hour)   
 - [YQL](https://yql.yandex-team.ru/Operations/YP_gQ9K3DCAg1LYIb1XIv6VlNumjuDQ3ObvwrGzC-WY=)

## Окружения компонентов поставки
* Logbroker:
   - [testing](https://logbroker.yandex-team.ru/logbroker/accounts/rasp/travel-testing-awacs-access-logs)
   - [production](https://logbroker.yandex-team.ru/logbroker/accounts/rasp/travel-production-awacs-access-logs)
* YT:
   - [testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/travel-testing-awacs-access-logs)
   - [production](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/travel-production-awacs-access-logs)
* ClickHouse:
   - [testing](https://yc.yandex-team.ru/folders/fooeiqn5ocka08hvboii/managed-clickhouse/cluster/mdbbgsdqsq6knc6l5hf5)
   - [production](https://yc.yandex-team.ru/folders/fooeiqn5ocka08hvboii/managed-clickhouse/cluster/mdbtpao1rek4kjilc5q9)
* ClickHouse Viewer:
   - [testing](https://travel-testing-awacs-access-log.chv.yandex-team.ru)
   - [production](https://travel-production-awacs-access-log.chv.yandex-team.ru)
* YQL:
   - [testing](https://yql.yandex-team.ru/Operations/YP_Yp9K3DCAg1KR0tOFS_ZsZHJB2OG3ZPyrtPtFCD48=)
   - [production](https://yql.yandex-team.ru/Operations/YP_gQ9K3DCAg1LYIb1XIv6VlNumjuDQ3ObvwrGzC-WY=)



## Подключение
Для подключения новых балансеров к поставке необходимо настроить поставку логов балансеров в топики Logbroker.  
[Пример настроенного балансера в Nanny](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_travel-rasp-testing_man/)
- Добавляем в конфиг балансера заголовки и куки, которые нужно логировать:
```
- copy: {source: X-Req-Id, target: X-Request-Id, keep_existing: true}
- create: {target: X-Request-Id, func: reqid, keep_existing: true}
- log: {target_re: X-Request-Id|User-Agent, cookie_fields: [yandexuid]}
```
- Создаем TVM-приложение, запрашиваем права на запись в топик для tvm_id
- Для каждого Nanny-сервиса балансера (соответствует пунктам 3-9 в [оригинальной инструкции](https://wiki.yandex-team.ru/users/nikshel/awacs-balancer-logs/#otpravkalogovvlogbroker)):
    - Находим последнюю стабильную версию [push client](https://sandbox.yandex-team.ru/tasks/?children=true&release=stable&type=BUILD_STATBOX_PUSHCLIENT&limit=20), копируем id ресурса
    - На вкладке `Files`  в `Sandbox files`  добавляем `push-client`, в форму вставляем id ресурса  
        ![awacs_push_client](_assets/awacs_push_client.png =800x120)
    - В секции `Static files`  добавляем файл `push-client_real.conf` и подставляем в него tvm_id  
        ![awacs_push_client_conf](_assets/awacs_push_client_conf.png =800x300)
    
      {% cut "push-client_real.conf для testing" %}
        ```
        watcher:
            state: /logs/pushclient
            drop_on_error: 1
        network:
            master-addr: "logbroker.yandex.net"
            proto: pq
            transport: ipv6
            tvm-client-id: <tvm_id>
            tvm-server-id: 2001059
            tvm-secret-file: pushclient-secrets/client_secret
        logger:
            file: /logs/current-pushclient
            remote: 0
            telemetry_interval: -1
            level: 6
        topic: /rasp/travel-testing-awacs-access-logs
        files:
          - name: /logs/current-access_log-balancer-80
            sid: [host, name, lines: 1]
            send_delay: 5
          - name: /logs/current-access_log-balancer-443
            sid: [host, name, lines: 1]
            send_delay: 5
        ```
      {% endcut %}

      {% cut "push-client_real.conf для production" %}
        ```
        watcher:
            state: /logs/pushclient
            drop_on_error: 1
        network:
            master-addr: "logbroker.yandex.net"
            proto: pq
            transport: ipv6
            tvm-client-id: <tvm_id>
            tvm-server-id: 2001059
            tvm-secret-file: pushclient-secrets/client_secret
        logger:
            file: /logs/current-pushclient
            remote: 0
            telemetry_interval: -1
            level: 6
        topic: /rasp/travel-production-awacs-access-logs
        files:
          - name: /logs/current-access_log-balancer-80
            sid: [host, name, lines: 1]
            send_delay: 5
          - name: /logs/current-access_log-balancer-443
            sid: [host, name, lines: 1]
            send_delay: 5
        ```
      {% endcut %}
    - На вкладке `Instance spec`  в `Instance data volumes`  добавляем `volume` с именем `pushclient-secrets`, в котором значение берётся из yav-секрета для TVM-приложения (id TVM приложения из `tvm-client-id` в `push-client_real.conf`)
        ![awacs_push_client_secret](_assets/awacs_push_client_secret.png =800x300)
    - Сохраняем снапшот: Save  -> Submit
    - На экране балансера в UI awacs нажимаем кнопку `Enable pushclient`:
        ![awacs_push_client_enable](_assets/awacs_push_client_enable.png =800x140)
    - Ждем, когда awacs активирует внесённое изменение (созданный им снапшот в Nanny-сервисе станет Active)
    - Проверяем, что логи начали поставляться в Logbroker. Если этого не происходит, заходим на машинку балансера и читаем pushclient.err
    - Настраиваем Juggler-проверки:
        - Добавляем ресурс с бандлом проверок как [juggler-check-bundle-push-client.tar.gz](https://sandbox.yandex-team.ru/resource/1653085111/view) , ставим галку `ISS properties` -> `Is juggler bundle`  и деплоим
        - Идем на вкладку `Monitoring settings`, жмем `Add passive check`, выбираем хост, в качестве сервиса пишем `push-client-last-commit`, в `Args ` добавляем `push-client_real.conf`. В `Notifications` -> `on_status_change` выбираем, куда отправлять уведомления
        
После настройки поставки в Logbroker данные начнут поставляться в YT (через LogFeller) и ClickHouse (через Transfer Manager).  
[Логи должны появиться в соответствующих окружениях](../../ops/tools/awacs_logs#okruzheniya-komponentov-postavki)  

## Документация
[Описание полей лога](https://wiki.yandex-team.ru/users/nikshel/awacs-balancer-logs/#parserlogov)  
[ClickHouse в YQL](https://yql.yandex-team.ru/docs/clickhouse#bazovoe-ispolzovanie)
