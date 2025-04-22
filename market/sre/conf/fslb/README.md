# config-market-fslb
Market config for L7 balancer

[Naming Conventions](https://github.yandex-team.ru/cs-admin/config-market-fslb/blob/master/src/balancer/values-available/README.md)

# conductor tickets
https://c.yandex-team.ru/packages/config-market-fslb/tickets

# сборка происходит автоматически по коммитам через tsum CD
https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/config-market-fslb-stages

# Создание конфига для сервиса
https://wiki.yandex-team.ru/market/administration/fslb/createbalancerfslb/
https://wiki.yandex-team.ru/market/administration/checklist/createfslb/

1. Добавить конфиг для сервиса в values-available
    * Бэкслэши в servername_regexp должны быть экранированы: "market\\.yandex\\.ru" (почему?)
2. Прописать IP-адреса балансеров сервиса из racktables в файл 00-ip-service-map.yaml
    (куда прописывать порты?)


# Формат конфига

    main:
        ips:
            vs: ip
        default_cert: 'cert'
    vs:
        servers:
            default|testing|production:
                main:
                    - name:
                      port:
                      http_port:
                      plain_http_backend: bool
                      timeout:
                      weight:

                alternative:
                    - name:
                      ...
        context:
            default|testing|production:
                antirobot: bool
                antirobot_service_name | default("market")
                attempts | default(1) | default(3)
                balancing_method = "hashing"|"rr"|"active"
                cert
                disable_https: bool
                exp_getter
                fallback_pool
                health_check | default("request")
                paths
                plain_http
                port_shift
                priority
                priority
                proxy_host
                rewrite_regexp | default(".*")
                rewrite_url
                servername_regexp
                service_name = string|"captcha"
                service_type = ""|"redirect"|"proxy"
                special = bool
                testid_from_host
                uaas_service_name | default("market")
                vs
                alternative_backends: bool | default(none)
                alt_headers:
                - alt_name:   'google_bot'
                  alt_header: 'User-Agent'
                  alt_regexp: 'Google Bot'
                - alt_name:   'yandex_bot'
                  alt_header: 'User-Agent'
                  alt_regexp: 'Yandex Bot'

- Секция `default` обязательна.

Некоторые Параметры секции `context` описаны ниже. Дополняйте, если знаете детальное значение других опций:

- `antirobot` - включить или выключить отправку входящих запросов в антиробот, который распознает робота и при необходимости скажет yandex-balancer-у показать капчу или просто 403 кода ответа.
- `antirobot_service_name` - маркер (на самом деле заголовок), по которому антиробот понимает, от какого сервиса пришел запрос на валидацию и соответственно применяет какие-то определенные настроенные правила, заданные на этот маркет
- `attempts` - кол-во повторных попыток. В каких случаях - см. конфиги и допиши сюда.
- `balancing_method` - метод балансировки трафика между бекендами, но для трафика, летящего на lo интерфейс в haproxy разница между ними не совсем понятна.
- `exp_getter` - включить эксперименты в yandex-balancer-е. В этом случае yandex-balancer будет ходить в uaas, чтобы получать заголовки про эксперименты и прокидывать их дальше в сервис.
- `servername_regexp` - регулярное выражение, предназначенное для матчинга приходящих запросов по заголовку `Host` и отправляющее нужные данные в правильные бекенды.
- `service_type` - для различных типов сервиса используется разная конфигурация, например для конфигов-редиректов. В шаблоне они разворачиваются в отдельном цикле `for`.
- `testid_from_host` - превращать testid значение, указанное в заголовке `Host` в заголовок `X-Testid`, который может использоваться в бекендах и возможно, в uaas.
- `uaas_service_name` - аналогично маркету для антиробота, мы делаем маркер для запросов, отправляемых в uaas, который возвращает список экспериментов и обогащает запрос перед отправкой его бекенду.
- `alternative_backends` - включить альтернативные бекенды. Работает только для сортировки запросов по заголовкам. При использовании этого параметра нужно обязательно указывать список из словарей с ключами `alt_name`, `alt_header` и `alt_regexp`, а также дополнительный блок бекендов в `servers` под названием `alternative`.
- `alt_name`   - Часть, которая будет добавлена к имени секции, начинающейся с `alternative_backend_` и заканчивающейся значением `alt_name`. Использовать только цифры, буквы латинского алфавита и символ подчеркивания (underscore). 
- `alt_header` - Имя заголовка, по которому планируется матчить запросы.
- `alt_regexp` - Регулярное выражение для содержимого заголовков.


# Деплой конфигов

0. Сконфигурировать IP-адреса на fslb (как?)
1. Запустить пайплайн "Выкладка config-market-fslb".
2. Включить конфиг нового сервера на балансерах

    ln -s  values-available/10-service.yaml values-enabled/10-service.yaml;

3. Сгенерировать конфиги и перезагрузить балансеры

    balancer_regenerate
    balancer_reload

