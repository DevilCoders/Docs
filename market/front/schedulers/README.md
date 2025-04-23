## Шедулеры фронта

Набор шедулеров фронта Яндекс.Маркета.


### Как запускать

1. Создать шедулер таски `TASKLET_RUN_COMMAND` в Sandbox по [ссылке](https://sandbox.yandex-team.ru/schedulers?task_type=TASKLET_RUN_COMMAND).

Шаблон поля  `__tasklet_input__`:

```json
{
    "config": {
        "environment_variables": [
            {
                "value": "market/front/schedulers",
                "key": "repo_path"
            },
            {
                "value": "12",
                "key": "node_js"
            },
            {
                "value": "15000",
                "key": "STARTREK_TIMEOUT_MS"
            },
            {
                "value": "68430",
                "key": "TRACKER_FILTER"
            },
            {
                "value": "debug",
                "key": "LOG_LEVEL"
            }
        ],
        "secret_environment_variables": [
            {
                "secret_spec": {
                    "key": "robot-metatron-st-token"
                },
                "key": "STARTREK_TOKEN"
            }
        ],
        "cmd_line": "source /etc/trendbox \n nvm install $node_js \n cd $repo_path \n npm install \n npm run start:crime-scene-cleaner",
        "arc_mount_config": {
            "revision_hash": "trunk",
            "enabled": true
        }
    },
    "context": {
        "secret_uid": "sec-01cv39yy683mvszy5yt550amgq"
    }
}
``` 

Если шедулеру необходимые секретные токены:

// TODO описать как это работает


### Запущенные шедулеры

1. https://sandbox.yandex-team.ru/scheduler/707613/view – удаляет комментарии-дубликаты из тикетов MARKETFRONT MARKETPARTNER
2. https://sandbox.yandex-team.ru/scheduler/706936/view – удаляет комментарии-дубликаты из тикетов MARKETAFFILIATE
3. https://sandbox.yandex-team.ru/scheduler/707053/view – аггрегирует комментарии роботов в описание MARKETAFFILIATE
4. https://sandbox.yandex-team.ru/scheduler/707056/view – аггрегирует комментарии роботов в описание MARKETFRONT MARKETPARTNER
5. https://sandbox.yandex-team.ru/scheduler/707058/view – удаляет комментарии-дубликаты из тикетов MARKETFRONT (? Но это не точно, непонятно что это и зачем)

