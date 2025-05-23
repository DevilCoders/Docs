# Экспорт метрик в формате Prometheus
Чтобы выгрузить метрики в формате {{ prometheus-name }}, воспользуйтесь методом [prometheusMetrics](../../api-ref/MetricsData/prometheusMetrics.md). Для загрузки метрик в {{ prometheus-name }} необходимо предварительно настроить сбор метрик в {{ prometheus-name }}.

Пример настройки сбора метрик из {{ monitoring-name }} в {{ prometheus-name }}:
1. Выберите каталог, с которого вы хотите собирать данные.
1. Выберите сервис из следующего списка:
   - `application-load-balancer` — {{ alb-name }}.
   - `audit-trails` — {{ at-name }}.
   - `certificate-manager` — {{ certificate-manager-name }}.
   - `compute` — {{ compute-name }}.
   - `container-registry` — {{ container-registry-name }}.
   {% if product == "yandex-cloud" %}- `data-proc` — {{ dataproc-name }}.{% endif %}
   {% if product == "yandex-cloud" %}- `data-streams` — {{ yds-name }}.{% endif %}
   - `data-transfer` — {{ data-transfer-name }}.
   - `iam` — {{ iam-name }}.
   {% if product == "yandex-cloud" %}- `interconnect` — {{ interconnect-name }}.{% endif %}
   - `kms` — {{ kms-name }}.
   {% if product == "yandex-cloud" %}- `logging` — {{ cloud-logging-name }}.{% endif %}
   - `managed-clickhouse` — {{ mch-name }}.
   {% if product == "yandex-cloud" %}- `managed-elasticsearch` — {{ mes-name }}.{% endif %}
   {% if product == "yandex-cloud" %} `managed-greenplum` — {{ mgp-name }}.{% endif %}
   - `managed-kafka` — {{ mkf-name }}.
   - `managed-kubernetes` — {{ managed-k8s-name }}.
   {% if product == "yandex-cloud" %}- `managed-mongodb` — {{ mmg-name }}.{% endif %}
   - `managed-mysql` — {{ mmy-name }}.
   - `managed-postgresql` — {{ mpg-name }}.
   {% if product == "yandex-cloud" %}- `managed-redis` — {{ mrd-name }}.{% endif %}
   {% if product == "yandex-cloud" %}- `managed-sqlserver` — {{ mms-name }}.{% endif %}
   - `message-queue` — {{ message-queue-name }}.
   - `monitoring` — {{ monitoring-name }}.
   - `network-load-balancer` — {{ network-load-balancer-name }}.
   {% if product == "yandex-cloud" %}- `serverless-apigateway` — {{ api-gw-name }}.{% endif %}
   {% if product == "yandex-cloud" %}- `serverless-containers` — {{ serverless-containers-name }}.{% endif %}
   {% if product == "yandex-cloud" %}- `serverless-functions` — {{ sf-name }}.{% endif %}
   {% if product == "yandex-cloud" %}- `speechkit` — {{ speechkit-name }}.{% endif %}
   - `storage` — {{ objstorage-name }}.
   {% if product == "yandex-cloud" %}- `translate` — {{ translate-name }}.{% endif %}
   {% if product == "yandex-cloud" %}- `vision` — {{ vision-name }}.{% endif %}
   {% if product == "yandex-cloud" %}- `ydb` — {{ ydb-name }}.{% endif %}
1. Создайте статичный [API-ключ](../../../iam/operations/api-key/create.md) для [сервисного аккаунта](../../../iam/concepts/users/service-accounts).
1. [Назначьте сервисному аккаунту роль](../../../iam/operations/roles/grant#access-to-sa) `{{ roles-monitoring-viewer }}` на выбранный каталог.
1. В [конфигурацию Prometheus](https://prometheus.io/docs/prometheus/latest/configuration/configuration) в секцию для сбора данных добавьте еще одну задачу (`job`):
   ```yaml
   ...
   scrape_configs:
     ...
     - job_name: 'yc-monitoring-export'
       metrics_path: '/monitoring/v2/prometheusMetrics'
       params:
         folderId:
         - '<folderId>' # например, aoeng2krmasimogorn5m
         service:
         - '<service>' # например, managed-mongodb
       bearer_token: '<api_key>'
       # Или через файл (рекомендуется):
       # bearer_token_file: '<имя файла с api_key>'
       static_configs:
       - targets: ['monitoring.{{ api-host }}']
         labels:
           folderId: '<folderId>'
           service: '<serviceId>'
   ```
1. Перезапустите {{ prometheus-name }}.
1. Проверьте сбор данных в пользовательском интерфейсе {{ prometheus-name }}: `http://localhost:9090/targets` (замените `localhost` именем хоста, на котором установлен {{ prometheus-name }}).
1. При необходимости изменения имен меток воспользуйтесь механизмом [relabeling](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#relabel_config).

{% note tip %}

Если у вас много метрик, увеличьте таймаут на сбор данных (`scrape_timeout`) до 60s.

{% endnote %}
