# Horizontal Pod Autoscaler

{% note info %}

Развитие сервиса  Horizontal Pod Autoscaler приостановленно

{% endnote %}


Автоматическое масштабирование `replica_set` - изменение количества подов - в зависимости от загрузки CPU.

Каждые 10 секунд Horizontal Pod Autoscaler:

- получает `current_metric` - среднее значение утилизации CPU за последние 5 минут (сигнал "CPU usage of cpu limit avg" со страницы мониторингов);
- если `current_metric` вышел за указанный пользователем интервал:
- высчитывается целевое количество подов `desired_replicas := ceil(current_metric / target_metric * current_replicas)`, где `target_metric` - середина целевого интервала;
- `desired_replicas` "режется" до указанного пользователем допустимого интервала: `desired_replicas := clip(desired_replicas, min_replicas, max_replicas)`;
- если предыдущий upscale/downscale был достаточно давно (период настраивается пользователем):
- обновляется `replica_set.pod_count := desired_replicas`.

Все аллокации/деаллокации производятся в рамках пользовательской квоты, указанной в `replica_set`.
Реализация гибких политик квотирования обсуждается в https://st.yandex-team.ru/DEPLOY-2309.

Horizontal Pod Autoscaler реализован в виде YP объекта `horizontal_pod_autoscaler` и контроллера. Объект `horizontal_pod_autoscaler` описывает поведение контроллера.
Контроллер периодически корректирует количество реплик `replica_set` для соответствия желаемой загрузки CPU, указанной пользователем.

## Требования к пользовательскому сервису {#service_requirements}

Прямая корреляция между (cpu) метрикой и кол-вом подов.

Новые поды должны активироваться быстрее, чем за `[upscale_delay](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/horizontal_pod_autoscaler.proto?rev=r8477255#L170) [default: 30 min]` для избежания осциляций. Читай подробнее в разделе [Алгоритм Replica Set Scale](#replica_set).

Для сервисов с большими контейнерами (>30cpu) не стоит пользоваться (настраивать) auto downscale ниже дневного бейзлайна.
Так как поиск места для контейнера в YP может занять продолжительное время, потраченное на дефрагментацию (часы).

**Хороший кандидат** для autoscaler - сервис stateless бекендов под балансером.
**Плохой кандидат** - сервис из трех реплик в master-slave парадигме.

## Временные пререквизиты {#prerequisites}
1) Редактирование autoscaler через UI пока недоступно:  https://st.yandex-team.ru/DEPLOY-2058
1) Включение autoscaler через UI пока недоступно: https://st.yandex-team.ru/DEPLOY-2058
Можно включить/редактировать autoscaler через dctl. [Пример.](#dctl_example)
1) Autoscaler над MYT/IVA смотрит на один и тот же аггрегат (geo=msk, как будто поды живут в одном кластере). https://st.yandex-team.ru/DEPLOY-2503
1) MultiClusterReplicaSet (пока) не поддерживается.
Приоритет низкий, так как MCRS не переживает YP XDC downtime.
Это ведет к тому, что autoscale не будет работать во время YP XDC downtime, что чревато инцидентами.

## Мотивация к использованию autoscaler {#motivation}
1) Защита от cpu (RPS) burst - upscale в случае резкого (или плавного) роста внешних запросов, включая сценарий отключения ДЦ.
Для безопасности можно запретить downscale ниже константы `min_replicas`.
Скорость реакции системы: 10 минут + время старта пода (загрузки ресурсов / старта процессов).
1) Автоскейл на фоне естественного роста/падения трафика в масштабах месяца/квартала.
Условно: "за последнюю неделю cpu avg поднялся выше 50%, добавлю-ка я один под".
Чтобы один раз задать "хочу запас cpu x2" и забыть.
1) Повышение утилизации ресурсов ночью.
Количество подов будет автоматически уменьшаться вечером и увеличиваться утром.
На освободившихся ресурсах ночью можно, например, запускать offline расчеты.

## Алгоритм Replica Set Scale {#replica_set}
В Деплое представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/horizontal_pod_autoscaler.proto?rev=8477255):

Кастомные метрики будут поддержаны в рамках:
https://st.yandex-team.ru/DEPLOY-2178
https://st.yandex-team.ru/DEPLOY-2505

## Dry run (RO) запуск autoscale над активным сервисом {#dry_run}

Для тестирование политики/поведения autoscale можно запустить его в dry run (RO) режиме.
Можно создать сразу несколько dry run автоскейлеров с разными конфигурациями.

Как это работает:
Autoscaler обновляет `replica_set` только при наличии в `replica_set` разрешающего лейбла.
Поэтому для dry run достаточно создать объект `horizontal_pod_autoscaler` (и не трогать `stage` / `replica_set`). 

Для этого:

1) Создайте объект `horizontal_pod_autoscaler` над вашим `replica_set` в том же кластере
Создайте файл hpa.yaml с описанием `horizontal_pod_autoscaler`:

а) Cpu utilization метрика (см. [proto](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/horizontal_pod_autoscaler.proto?rev=r8477255#L52)):

```yaml
meta:
  id: yanddmi-test-hpa # hpa-name
  replica_set_id: yanddmi-test-cpu-load.DeployUnit1 # stage-name.du
spec:
  replica_set:
    cpu_utilization:
      lower_bound_percent: 40
      upper_bound_percent: 60
    max_replicas: 3
    min_replicas: 1
    upscale_delay: 
      seconds: 1800
    downscale_delay: 
      seconds: 1800
```
б) Произвольная метрика из golovan (см. [proto](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/horizontal_pod_autoscaler.proto?rev=r8477255#L70)):

```yaml
meta:
  id: danibw-test-hpa
  replica_set_id: danibw-test-cpu-load.DeployUnit1
spec:
  replica_set:
    custom:
      golovan_signal:
        signal: "havg(portoinst-cpu_limit_usage_perc_hgram)"
        tags:
          itype: "deploy"
          deploy_unit: "DeployUnit1"
          stage: "danibw-test-cpu-load"
        set_local_geo_tag: true
        host: "ASEARCH"
      lower_bound: 4.0
      upper_bound: 6.0
    max_replicas: 2
    min_replicas: 1
```
в) Произвольная метрика из solomon (см. [proto](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/horizontal_pod_autoscaler.proto?rev=r8477255#L100)):

```yaml
meta:
  id: danibw-test-hpa
  replica_set_id: danibw-test-cpu-load.DeployUnit1
spec:
  replica_set:
    custom:
      solomon_signal:
        project: "horizontal_pod_autoscaler_controller"
        cluster: "sas_yp"
        service: "sas_yp"
        host: "cluster"
        sensor: "horizontal_pod_autoscaler_controller.hpa_ctl.danibw-test.metric_value"
        aggregation: "avg"
      lower_bound: 4.0
      upper_bound: 6.0
    max_replicas: 2
    min_replicas: 1
```
Запишите объект через dctl в тот же кластер, что `replica_set`:

```bash
yanddmi@yanddmi-dev[~]:ya tool dctl put hpa -c sas hpa.yaml 
Put horizontal_pod_autoscaler: yanddmi-test-hpa
```
2) Подберите корректную конфигурацию на основе расчетных/прогнозируемых числа подов и загрузки cpu
В dry mode autoscaler:

- вычисляет:
- `current_replicas` - расчетное/прогнозируемое количество подов после "мнимых" рескейлов
- `metric_value := real_metric_value * (real_replicas / current_replicas)` - расчетное/прогнозируемое значение cpu метрики
- считает, что `replica_set` меняет кол-во подов мгновенно.

Статус и графики autoscaler описаны [в следующей секции](#diagnostics).
Понаблюдайте за графиками в течение суток/недели и подберите корректную конфигурацию.

2) Удалите созданный объект `horizontal_pod_autoscaler`

```bash
yanddmi@yanddmi-dev[~]:ya tool dctl remove hpa yanddmi-test-hpa -c sas
Removed horizontal pod autoscaler: yanddmi-test-hpa
```

## Пример включения через dctl {#dctl_example}

1) Указать секцию `autoscale` вместо константы `pod_count` в спеке stage(deploy_unit):

```yaml
...
spec:
  deploy_units:
    DeployUnit1:
      replica_set:
        per_cluster_settings:
          sas:
            autoscale:
              cpu_utilization:
                lower_bound_percent: 40
                upper_bound_percent: 60
              max_replicas: 100
              min_replicas: 1
              upscale_delay:
                seconds: 1800
              downscale_delay:
                seconds: 180
...
```
2) Обновить stage: `ya tool dctl put stage deploy.yaml`
3) Следить за статусом выкатки в UI

Подробный статус объекта `horizontal_pod_autoscaler` можно узнать через dctl:

```bash
yanddmi@yanddmi-dev[~]:ya tool dctl status hpa -c sas yanddmi-test.DeployUnit1
+------------+------------------+---------------------+---------------------+------------------------------------+
|  Replicas  |   MetricValue    |   LastUpscaleTime   |  LastDownscaleTime  |               Status               |
+------------+------------------+---------------------+---------------------+------------------------------------+
| 3 ∈ [1, 3] |  52 ∈ [40, 80]   | 2020-03-18 17:58:40 | 2020-03-18 18:06:21 | Successful update of replica_count |
+------------+------------------+---------------------+---------------------+------------------------------------+
```

Выключить autoscaler можно откатив секцию `autoscaler` назад к `pod_count`.

##  Мониторинг и диагностика {#diagnostics}

### Чтение статуса через dctl {#dctl_status}
```bash
yanddmi@yanddmi-dev[~]:ya tool dctl status hpa -c sas yanddmi-test.DeployUnit1
+------------+------------------+---------------------+---------------------+------------------------------------+
|  Replicas  |   MetricValue    |   LastUpscaleTime   |  LastDownscaleTime  |               Status               |
+------------+------------------+---------------------+---------------------+------------------------------------+
| 3 ∈ [1, 3] |  52 ∈ [40, 80]   | 2020-03-18 17:58:40 | 2020-03-18 18:06:21 | Successful update of replica_count |
+------------+------------------+---------------------+---------------------+------------------------------------+
```

### Графики в Solomon {#sensors}

Контроллер генерирует solomon сенсоры для каждого пользовательского hpa: [https://solomon.yandex-team.ru/?project=horizontal_pod_autoscaler_controller&cluster=sas_test_yp&service=sas_test_yp&sensor=horizontal_pod_autoscaler_controller.hpa_ctl.yanddmi-test-cpu-load.DeployUnit1](https://solomon.yandex-team.ru/?project=horizontal_pod_autoscaler_controller&cluster=sas_test_yp&service=sas_test_yp&sensor=horizontal_pod_autoscaler_controller.hpa_ctl.yanddmi-test-cpu-load.DeployUnit1.*&graph=auto&stack=false)

Замените cluster на ваш кластер и `yanddmi-test-cpu-load.DeployUnit1` на id вашего hpa.
