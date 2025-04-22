## Описание

Данная библиотека подключается opt-in к библиотеке tms-core-quartz2.

Здесь добавляется функциональность по отправке времени выполнения задач в соломон.
Каждое выполнение tms-задачи (как успешное, так и неуспешное) будет инициировать событие отправки
асинхронного запроса в solomon-push-api.

### Включение tms-quartz-solomon

#### Шаг 0 - добавление зависимости
Добавьте в свой ya.make файл в раздел PEERDIR зависимость:
```
    market/jlibrary/tms-quartz-solomon
```

#### Шаг 1 - настройка контекста
Для работы библиотеки необходимо добавить в свой tms-контекст бины:
 ``SolomonPusher``, ``SolomonJobRunTimeReporterProperties`` и ``SolomonJobRunTimeReporter``.
Пример инициализации необходимых бинов в своём контексте:
```
@Bean
public SolomonJobRunTimeReporterProperties solomonJobRunTimeReporterProperties() {
    return new SolomonJobRunTimeReporterProperties();
}

@Bean
public SolomonPusher solomonPusher(SolomonJobRunTimeReporterProperties properties,
                            @Value("${your-project.solomon.oauth.token}") String oauthToken) {
    return SolomonPusher
        .ownHttpClient(AsyncHttpClientUtils.newAsyncHttpClient("Solomon-Reporter"))
        .pushTo(properties.getStand())
        .oauthToken(oauthToken)
        .debugNon200()
        .build();
}

@Bean
public SolomonJobRunTimeReporter solomonReporter(SolomonJobRunTimeReporterProperties properties,
                                       SolomonPusher solomonPusher) {
    return new SolomonJobRunTimeReporter(properties, solomonPusher);
}
```

#### Шаг 2 - properties файл
Для корректной работы SolomonPusher-a, необходимо задать следующие настройки в properties-файле:
```
market.tms-quartz-solomon.enabled=true
market.tms-quartz-solomon.stand=PRESTABLE
market.tms-quartz-solomon.project=your-project
market.tms-quartz-solomon.cluster=your-project.cluster
market.tms-quartz-solomon.service=your-project.service
market.tms-quartz-solomon.sensor=job_execution_time
```
Для окружения testing и production необходимо использовать
```
market.tms-quartz-solomon.stand=PRODUCTION
```
Остальные настройки можно использовать одинаковыми для всех окружений (development, testing, production).
Но скорее всего значения `solomon.cluster` и `solomon.service` для testing и production у вас будут различными.

#### Использование
После выполнения шагов выше, все tms-задачи, которые есть у вас в контексте (бины, отмеченные аннотацией @CronTrigger),
при каждом выполнении будут отправлять push запрос в solomon-api .
В запросе общей будет информация, перечисленная в свойствах: `solomon-project,
solomon-cluster, solomon-service, solomon-sensor`.
Различным будет `label` c названием `job_name` (свой для каждой задачи),
и собственно время выполнения задачи.
Таким образом, в solomon будет возможность получить график времени выполнения в
разрезе каждой задачи, фильтруя точки по `job_name`.

