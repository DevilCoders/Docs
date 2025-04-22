## Ротация дежурных в правилах нотификации в соотвествии с графиком дежурств ABC
### Добавление правила в ротацию:
Добавить словарь в ```ROTATOR_CONFIGS``` в [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/mail/monitoring/juggler/notifications/config.py):
```
    {
        "abc_id": <id сервиса в ABC с графиком дежурств>,
        "namespace": "<имя неймспейса>",
        "notify_rule_id": "<id правила нотификации>"
    }

```

[Шедуллер в ABC](https://sandbox.yandex-team.ru/scheduler/19980/view)

Шедулер запускается каждый час.

**Для того, чтобы у джобы хватило прав поменять порядок дежурных нужно добавить робота ```robot-gerrit``` во владельцы неймспейса Juggler.**
