# solomon-push-client

Пакет для пуша отдельных сигналов в [Solomon].
Может быть использован для сбора метрик и настройки мониторингов
на несильно нагруженные сервисы, где частота отправки метрик не должна превышать 5000 RPS.
Сделано на основе [Solomon Push API][push-API].

## Установка

```shell
npm i @yandex-int/solomon-push-client --registry=https://npm.yandex-team.ru
```

## Использование

Для использования необходимо передать [Solomon OAuth токен][OAuth-токен] в переменной окружения `SOLOMON_OAUTH_TOKEN`.
Timestamp отправленной метрики проставляется, как текущий timestamp запроса.

1. `SolomonCounterClient` –– класс-счётчик для отправки монотонно возрастающего значения во времени какой-либо метрики.
По умолчанию `value` инкрементируется на единицу, а [тип сенсора][sensor-type] сенсора ⟶ `COUNTER`.

    ```ts
    import { SolomonCounterClient } from '@yandex-int/solomon-push-client';

    const httpNotFoundRequestsCounter = new SolomonCounterClient({
        project: 'fixture_project_name',
        cluster: 'fixture_cluster_name',
        service: 'fixture_service_name',
        labels: {
            // имя метрики
            name: 'http.requests_total',
            // метка и её значение: https://wiki.yandex-team.ru/solomon/userguide/datamodel/#types
            status: 404,
        }
    });

    async function main() {
        await httpNotFoundRequestsCounter.increment();
    }

    main();
    ```

2. `SolomonPushClient` –– базовый класс, поддерживающий отправку произвольного типа метрик (в отличие от `SolomonCounterClient`).
Для пуша метрики необходимо воспользоваться методом `push`:

    ```ts
    import { SolomonPushClient, SolomonMetricType } from '@yandex-int/solomon-push-client';

    const personTemperature = new SolomonPushClient({
        project: 'fixture_project_name',
        cluster: 'fixture_cluster_name',
        service: 'fixture_service_name',
        labels: {
            // имя метрики
            name: 'temperature_of_body',
        }
    }, SolomonMetricType.DGAUGE);

    async function main() {
        await personTemperature.push(36.6);
    }

    main();
    ```

[Solomon]: https://wiki.yandex-team.ru/solomon/
[push-API]: https://wiki.yandex-team.ru/solomon/api/push/
[OAuth-токен]: https://wiki.yandex-team.ru/solomon/api/v2/#authentication
[sensor-type]: https://wiki.yandex-team.ru/solomon/userguide/datamodel/#types
