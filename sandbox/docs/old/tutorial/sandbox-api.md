Управлять и получать информацию обо всех объектах Sandbox можно через его [REST API](https://wiki.yandex-team.ru/sandbox/api/). Обычно его используют во внешних сервисах для автоматизации запуска задач. Но и в коде задач прямые вызовы в API могут быть полезны.

API рекомендуется использовать через специальный HTTP-клиент [sandbox/common/rest](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/rest) (см. [документацию и примеры](https://sandbox.yandex-team.ru/docs/html/common.rest.html#common.rest.Client)). В классе задачи его объект уже инициализирован в свойстве `self.server`.

Узнаем из API, как давно была создана последняя задача типа `HELLO_%LOGIN%`, завершившаяся в статусе SUCCESS. Для этого подойдёт метод [GET /task](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/task/task_list_get). Полный запроса будет выглядеть так:

```
GET /api/v1.0/task?type=HELLO_%LOGIN%&limit=1&status=SUCCESS&fields=time&order=-id HTTP/1.1
Host: sandbox.yandex-team.ru
```


В API-клиенте ему соответствует следующий код:

```python
from sandbox.common import rest

client = rest.Client()
resp = client.task.read(
    type="HELLO_%LOGIN%", limit=1, status="SUCCESS", fields="time", order="-id"
)
```

При переносе вызова в код задачи текущий тип можно взять напрямую из объекта, а разницу во времени перевести в человекочитаемый вид с помощью функции из [sandbox/common/format](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/common/format):

```python
import datetime as dt
from sandbox.common import format

def on_execute(self):
    resp = self.server.task.read(type=self.type.name, limit=1, status="SUCCESS", fields="time", order="-id")
    if resp["items"]:
        task = resp["items"][0]

        from dateutil import parser
        created = parser.parse(task["time"]["created"]).replace(tzinfo=None)

        delta = format.td2str(dt.datetime.utcnow() - created)
        self.set_info("Last successfull task was created {} ago".format(delta))
    ...
```

Не забудьте подключить соответствующие библиотеки в PEERDIR. Результат должен отображаться на странице задачи:

![task result](https://wiki.yandex-team.ru/users/mkznts/sandbox-tutorial/14-sandbox-api/.files/screenshot2019-11-08at17.58.43.png)
