# Routines в SandBox

Env | Конфиг файл | Список шедулеров | Мониторинги
--- | --- | --- | ---
Testing | [Конфиг файл](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/etc/sandbox-tasks-testing.json) | [Список шедулеров](https://sandbox.yandex-team.ru/schedulers?task_type=MARKET_RUN_UNIVERSAL_BUNDLE&tags=TESTING) |  [Мониторинги](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmi-datacamp-united-testing%26service%3Droutines-*-status)
Production | [Конфиг файл](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/etc/sandbox-tasks-production.json) | [Список шедулеров](https://sandbox.yandex-team.ru/schedulers?task_type=MARKET_RUN_UNIVERSAL_BUNDLE&tags=PRODUCTION) | [Мониторинги](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmi-datacamp-united%26service%3Droutines-*-status) 

## Логи отработавшей таски
Открываем в sandbox страницу задачу, логи которой хотим почитать. Нас на этой странице интересует ссылка `log1`, а в нем файл `market_task.err.log`.

## Горит мониторинг routines-*-status
По окончании работы sandbox отправляет в juggler сигнал со своим статусом. В случае упавшей задачи отправляется статус CRIT и ссылка на неудачный запуск. В этом случае надо посмотреть логи задачи по инструкции выше.

Если в течение `juggler.ttl` juggler не получит сигнал от sandbox, то мониторинг зажжется со статусом `NO_DATA`. В этом случае надо открыть шедулер через UI Sandbox и изучить историю запусков. Как вариант шедулер могли остановить руками, либо же таска выполняется дольше `juggler.ttl` и следует поднять пороги/ускорить таску.   

## Остановка шедулера
В случае проблем с какой-то из тасок, можно остановить его запуск через UI Sandbox.
![pic](../../_images/sb_scheduler_stop.png)

## Хотфиксом обновить параметры запуска таски
Например надо увеличить timeout таски, либо докинуть диска 
1. Коммитим в конфиги шедулеров свой патч
2. Копируем последний запуск таски [GEN_IDX_UNIVERSAL_SCHEDULERS](https://sandbox.yandex-team.ru/tasks?children=true&author=robot-market-infra&type=GEN_IDX_UNIVERSAL_SCHEDULERS&limit=20&created=14_days&input_parameters=%7B%22environment%22%3A%22production%22%7D)
3. Запускаем таску

## Запуск новой задачи через рутины

Чтобы переместить рутину в сандбокс нужно:
- Дописать в конфиг [тестинга](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/etc/sandbox-tasks-testing.json) и [прода](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/etc/sandbox-tasks-production.json) необходимую таску.
- Добавить таску в [список тасок](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/routines/bin/main.py?rev=r8566967#L63), которые запускаются через sandbox.
- Ждать релиза Datacamp Routines

### Конфиги

Для рутин используется упрощенный конфиг:
```
{
  "tasks": {
    "routines-<имя рутины в lower_case>": {
      "type": "ROUTINES_TASK",
      "sandbox": {
        "task_name": "<имя рутины как в TASKS в бинаре рутин>",
        "interval": <интервал в секундах>,
        "sequential_run": true,
        "kill_timout": <интервал в секундах>
      },
      "juggler": {
        "ttl": <время в секундах через которое загорится мониторинг, примерно 1.5 * interval>
      }
    }, 
    ...
  }
}
```

Если нужно сделать аналогичную процедуру, но не для рутин, то придется писать полное описание шедулера из [API sandbox](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/scheduler/scheduler_list_post):
```
{
  "tasks": {
    "<имя таски>": {
      "sandbox": {
        "task_type": "MARKET_RUN_UNIVERSAL_BUNDLE",
        "data": {
          "owner": "owner",
          "author": "author",
          "task": {
            "owner": "owner",
            "tags": ["любые","теги"],
            "kill_timeout": <интервал в секундах>,
              "custom_fields": [
                {"name": "task_name", "value": "<имя таски>"},
                {"name": "bundle_name", "value": "<имя бандла>"},
                {
                  "name": "cmd",
                  "value": [
                    "аргументы",
                    "камандной",
                    "строки",
                  ],
                },
              {"name": "environment", "value": "production"},
            ],
          },
        },
      },
      "juggler": {"ttl": <интервал в секундах>},
    },
    ...
  }
}
```

Если запускается не `MARKET_RUN_UNIVERSAL_BUNDLE`, то `custom_fields` составляется для соответствующей задачи.

Для корректного запуска `MARKET_RUN_UNIVERSAL_BUNDLE` необходимо, чтобы ресурс, указанный в `bundle_name`, был собран и зарелизен. Вот [пример](https://sandbox.yandex-team.ru/task/1038293087/view).


## Детали реализации
### Запуск задачи шедулером
1. В sandbox находится ресурс с типом `MARKET_RUN_UNIVERSAL_BUNDLE`, атрибутом `bundle_name=routines-sandbox` и зарелиженный в нужный stage
2. Подхватываются необходимые секреты из секретницы
3. Опционально подхватываются ITS и дополнительные ресурсы(например геттер)
4. sandbox запускает вашу команду из входных параметров 

### Метрики
1. Собираются метрики времени подготовки/выполненния таски, скачивания/распаковки ресурсов. На графики можно посмотреть [тут](https://monitoring.yandex-team.ru/projects/market.datacamp/dashboards/mond3evb61302ianc787?from=now-1h&to=now&refresh=60000&p.cluster=testing&p.task=OffersCopier)
2. Можно самому писать метрики для отправки. Для этого нужно положить в окружение таски файлик `app-metrics.json` формата 
```
{
  "sensor1": 100, 
  "sensor2": 200,
}
```

### Релизы
1. В ЦУМ собирается дополнительный пакет рутин для запуска в sandbox
2. После сборки пакета запускается кубик генерации шедулеров в stage. **Сейчас конфиг генератора берется из транка, а не из ревизии релиза: ждем https://st.yandex-team.ru/MARKETINFRA-10261**
3. Дополнительно генерируются проверки в juggler
4. Шедулеры начинают работать в sandbox

## Дебагинг и разработка
### GEN_IDX_UNIVERSAL_SCHEDULERS
Это таска, которая запускается из релизного пайплайна ЦУМ, и на основе конфигов в аркадии создает шедулеры и мониторинги. Код таски лежит в
[sandbox/projects/market/idx/GenIdxUniversalSchedulers](https://a.yandex-team.ru/arc_vcs/sandbox/projects/market/idx/GenIdxUniversalSchedulers) и катается с помощью яндексового CI.

#### Выкатка таски
Для GEN_IDX_UNIVERSAL_SCHEDULERS существует релизный пайплайн с автоматической выкаткой релиза в тестинг, выкладка в стэйбл происходит вручную:
1. Сборка релиза запускается автоматически, страница [релизного пайплайна](https://a.yandex-team.ru/projects/datacamp/ci/releases/timeline?dir=sandbox%2Fprojects%2Fmarket%2Fidx%2FGenIdxUniversalSchedulers&id=release_gen_idx_universal_schedulers)
2. Релиз выкатывается в тестинг автоматически
3. Нужно удостовериться в том, что новые таски успешно запускаются с новым релизом, [история запусков таски](https://sandbox.yandex-team.ru/tasks?children=true&type=GEN_IDX_UNIVERSAL_SCHEDULERS&created=14_days&input_parameters=%7B%22binary_executor_release_type%22%3A%22testing_or_upper%22%7D).
4. По истечению некоторого времени, когда таск отработает достаточное количество раз без происшествий, выкатываем таск в стэйбл.
5. Аналогично проверяем, что продовые шедулеры генерируются: [история запусков таски](https://sandbox.yandex-team.ru/tasks?children=true&type=GEN_IDX_UNIVERSAL_SCHEDULERS&created=14_days&input_parameters=%7B%22binary_executor_release_type%22%3A%22stable%22%7D)

### MARKET_RUN_UNIVERSAL_BUNDLE
Таска-обертка, которая отвечает за подготовку окружения и запуск бинарника рутин. Код лежит в
[sandbox/projects/market/idx/MarketRunUniversalBundle](https://a.yandex-team.ru/arc_vcs/sandbox/projects/market/idx/MarketRunUniversalBundle/__init__.py) и катается с помощью яндексового CI.

#### Выкатка таски
Для MARKET_RUN_UNIVERSAL_BUNDLE существует релизный пайплайн с автоматической выкаткой релиза в тестинг, выкладка в стэйбл происходит вручную:
1. Сборка релиза запускается автоматически, страница [релизного пайплайна](https://a.yandex-team.ru/projects/datacamp/ci/releases/timeline?dir=sandbox%2Fprojects%2Fmarket%2Fidx%2FRunUniversalTask&id=release_market_run_universal_bundle)
2. Релиз выкатывается в тестинг автоматически
3. Нужно удостовериться в том, что новые таски успешно запускаются с новым релизом, [история запусков таски](https://sandbox.yandex-team.ru/tasks?children=true&type=MARKET_RUN_UNIVERSAL_BUNDLE&created=14_days&input_parameters=%7B%22binary_executor_release_type%22%3A%22testing_or_upper%22%7D).
4. По истечению некоторого времени, когда таск отработает достаточное количество раз без происшествий, выкатываем таск в стэйбл.
5. Аналогично проверяем, что таски протекают успешно: [история запусков таски](https://sandbox.yandex-team.ru/tasks?children=true&type=MARKET_RUN_UNIVERSAL_BUNDLE&created=14_days&input_parameters=%7B%22binary_executor_release_type%22%3A%22stable%22%7D)

### Запуск таски не по расписанию
На странице шедулера жмем кнопку `Run once`
![pic](../../_images/sb_scheduler_run_once.png)

### Запуск таски с подменой релиза
Допустим хочется запустить таску со своим кодом и проверить, её выхлоп. В таком случае:
1. `cd ~/arcadia/market/idx/datacamp/routines`
2. Собираем пакет `ya package pkg-sandbox.json`
3. Загружаем его в sandbox `ya upload -T=MARKET_IDX_UNIVERSAL_BUNDLE <pkg.tar.gz>`
4. Копируем задачу, которая запускалась шедулером.
5. При необходимости правим команду запуска бинарника
6. В параметрах задачи меняет `override_basic_params=True` и прописываем id ресурса из предыдущего шага в `overridden_bundle_resource`
7. Запускаем задачу

### Быстрофикс
Если пришло осознание, что в выложенном пакете что-то не так и нужно срочно его заменить, а релиз не хочется трогать, то можно выкатить свой ресурс, который перекроет тот, что лежит в проде/тестинге.
1. `cd ~/arcadia/market/idx/datacamp/routines`
2. Собираем пакет `ya package pkg-sandbox.json`
3. Загружаем его в sandbox `ya upload -T=MARKET_IDX_UNIVERSAL_BUNDLE <pkg.tar.gz> -A resource_name=routines-sandbox  --release <testing/stable>`

Теперь все новые задачки из-под шедулеров будут использовать новый ресурс. До тех пор пока его не перекроет другой, например выложенный релизом.

### Ссылки
* [Документация по sandbox](https://docs.yandex-team.ru/sandbox/)
* [Документация по бинарным задачам sandbox](https://docs.yandex-team.ru/sandbox/dev/binary-task)
* [Релизный пайплайн универсального запускатора бинарников MARKET_RUN_UNIVERSAL_TASK](https://a.yandex-team.ru/projects/datacamp/ci/releases/timeline?dir=sandbox%2Fprojects%2Fmarket%2Fidx%2FRunUniversalTask&id=release_market_run_universal_bundle)
* [Релизный пайплайн генератора шедулеров GEN_IDX_UNIVERSAL_SCHEDULERS](https://a.yandex-team.ru/projects/datacamp/ci/releases/timeline?dir=sandbox%2Fprojects%2Fmarket%2Fidx%2FGenIdxUniversalSchedulers&id=release_gen_idx_universal_schedulers)
