# Conserva
Система создания бэкапов для S3


{% note alert "Как восстановить бэкап" %}

<br>Для выполнения действий необходимо входить в состав [abc:maps-core-conserva](https://abc.yandex-team.ru/services/maps-core-conserva)
<br>Возьмите [шаблон](https://sandbox.yandex-team.ru/template/RestoreS3Backup/view), нажмите "Create new task", затем в секции tasklet_input поставьте значения yt_dir(откуда восстанавливаем) и s3_bucket(куда восстанавливаем) и запустите его.
<br>[Тут](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/conserva) можно посмотреть список доступных yt_dir.
<br>Необходимо, чтобы [access и secret](https://wiki.yandex-team.ru/mds/s3-api/authorization/#upravlenieaccesskeys) ключи были прописаны [в секрете](https://yav.yandex-team.ru/secret/sec-01f6p883xe46d86wc17bjkhpqm). (для pano-src, maps-sat-source и maps-sat-rgb-source уже прописаны)
<br><br>Например, для pano-src:
```json
{
    "config": {
        "yt_dir": "pano-src",
        "s3_bucket": "pano-src",
        "command": "RESTORE",
        "operations_count": 5,
        "jobs_count": 100
    },
    "context": {
        "secret_uid": "sec-01f6p883xe46d86wc17bjkhpqm"
    }
}
```

{% endnote %}


{% note warning %}

По всем вопросам обращаться в [чат поддержки](../contacts.md).

{% endnote %}

Регулярно запускаются задачи создания и валидации бэкапов:
- [backup: pano-src](https://sandbox.yandex-team.ru/scheduler/86672/view)
- [backup: maps-sat-rgb-source](https://sandbox.yandex-team.ru/scheduler/90727/view)
- [backup: maps-sat-source](https://sandbox.yandex-team.ru/scheduler/90728/view)
- [md5: pano-src](https://sandbox.yandex-team.ru/scheduler/105616/view)
- [md5: maps-sat-rgb-source](https://sandbox.yandex-team.ru/scheduler/105883/view)
- [md5: maps-sat-source](https://sandbox.yandex-team.ru/scheduler/105617/view)

