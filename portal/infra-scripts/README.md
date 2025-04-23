# Скрипты для безопасной очистки s3

Скрипты позволяют чистить s3 от ненужных файлов с учётом времени модификации и доступа к файлу. В этом состоит отличие от родного механизма s3, который использует только время модификации файла.

## Рекомендуемый способ использования

Настраиваем автоматическую чистку в бакете **xyz** файлов, которые:
- последний раз модифицировались не позднее **EXISTENCE_DAYS** дней назад,
- не находятся в access логах последних **NO_ACCESS_DAYS** дней,
- перед удалением перемещаются в специальную папку **to-delete** и лежат там ещё  **IDLE_DAYS** после чего удаляются безвозвратно.

Для правильной работы скрипта нужно, чтобы в env были следующие секреты: `YQL_TOKEN`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`.
Помимо этого требуется, чтобы запросы за файлами попадали в логи [logs/l7-balancer-yastatic-access-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/l7-balancer-yastatic-access-log/1d)

1. для настройки потребуется [установить aws-cli и получить нужные секреты ](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#awscommandlineinterface)
2. настраиваем политику удаления в папке **to-delete**:
 - получаем существующую политику (обязательно нужно получить существующую, т.к. установка политики перепишет существующую)
 `aws --endpoint-url=http://s3.mds.yandex.net s3api get-bucket-lifecycle-configuration --bucket xyz`
 - убеждаемся что в нужном бакете _нет ничего ценного_ в папке **to-delete**
 `aws --endpoint-url=http://s3.mds.yandex.net s3 ls xyz/to-delete/`
 - устанавливаем политику с новым правилом для папки **to-delete**:
 ```
 aws --endpoint-url=http://s3.mds.yandex.net s3api put-bucket-lifecycle-configuration --bucket xyz --lifecycle-policy {
     "Rules": [
         !!здесь указать все существующие правила из первого пункта!!
         ,
         {
            "Expiration": {
                "Days": IDLE_DAYS
            },
            "ID": "Remove in IDLE_DAYS days",
            "Filter": {
                "Prefix": "to-delete/"
            },
            "Status": "Enabled"
         }
      ]
    }
 ```
3. настраиваем шедулер в [сандбоксе](https://sandbox.yandex-team.ru)
 - справа-сверху нужно нажать "Create scheduler" и выбрать `TRENDBOX_CI_JOB`
 - в Job configuration указать следующий конфиг (подставив в нужных местах свои значения):
 ```json
 {
    "debugShell": true,
    "language": "node_js",
    "env": {
        "node_js": 12,
        "SCHEDULER": "cleanup-s3", // это менять не надо
        "S3_PREFIX": "smth/", // здесь указать префикс, если требуется чистка только определённого префикса
        "DEST_PREFIX": "to-delete",
        "S3_BUCKET": "xyz",
        "EXISTENCE_DAYS": EXISTENCE_DAYS,
        "NO_ACCESS_DAYS": NO_ACCESS_DAYS
    },
    "lifecycle": {
        "prepare": [
            "nvm install $node_js",
            "trendbox checkout -c $checkout_config --dir sources",
            "cd sources; hash -r"
        ],
        "before_install": [
            "npm ci"
        ],
        "install": [
            "npm run scheduler:install"
        ],
        "script": [
            "npm run scheduler:start"
        ]
    },
    "checkout": {
        "type": "git",
        "url": "https://github.yandex-team.ru/morda/infra-scripts.git",
        "branch": "master"
    }
}
```
 - настроить остальные параметры шедулера
 - [пример конфигурации](https://sandbox.yandex-team.ru/scheduler/24844/view)

## Как срочно почистить бакет

`AWS_ACCESS_KEY_ID=... AWS_SECRET_ACCESS_KEY=... S3_BUCKET=zyx ./bin/rm-by-prefix.js --dry-run to-delete/smth`
Префикс здесь от корня бакета. Скрипт откажется удалять папку из корня бакета чтобы минимизироват ущерб от кривых рук.
Дейстует быстро, но не моментально. Вычистка сотни гигабайт затянется на десятки минут.

## Как узнать, сколько занимает папка в бакете

`AWS_ACCESS_KEY_ID=... AWS_SECRET_ACCESS_KEY=... S3_BUCKET=zyx ./bin/rm-by-prefix.js --dry-run prefix`
Отличается от предыдущего пункта параметром --dry-run.
