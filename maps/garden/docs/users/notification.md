# Оповещения из тасок

Огородные таски поддерживают рассылку оповещений через [JNS](https://jns.yandex-team.ru/).

Для рассылки необходимо:
1. Завести свой [проект](https://docs.yandex-team.ru/jns/sources) в JNS.
2. Настроить [канал](https://docs.yandex-team.ru/jns/channels) для оповещений.
3. Сформировать настройки для рассылки оповещений вида:

```python
from maps.garden.libs.jns_client.client import JnsConfig, JnsTarget

JNS_CONFIG = JnsConfig(
    # для отправки сообщений из контура datatesting
    datatesting=[
        JnsTarget(
            project=<target-project>,
            channel=<target-channel>
        ),
        JnsTarget(
            ...
        ),
        ...
    ],
    # Для отправки из стабильного контура:
    stable=[
        JnsTarget(
            ...
        ),
        ...
    ]
)
```

4. В методе `Task.__call__()` отправить оповещение:
```python
def __call__(self, ...):
    ...

    self.notify(JNS_CONFIG, "your message")
```

В данный момент поддержаны следующие типы каналов:
1. Email
2. Telegram
3. Slack
4. YaChats

Так же, некоторые стандартные таски могут сами отправлять оповещения об успешном окончании работы. Для отправки сообщений необходимо передать настройки оповещений в конструктор таски:
```python
graph_builder.task(
    ecstatic.ActivateTask(
        ....
        jns_config=JNS_CONFIG,
    )
).creates(
    ...
).demands(
    ...
)
```

Пока поддерживает отправку сообщений таска `ecstatic.ActivateTask`.
