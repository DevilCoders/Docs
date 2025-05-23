Альтернативный способ сконвертировать HTML в Markdown — запустить в задаче утилиту cmark. Доставить в задачу её можно с помощью Sandbox-ресурса.

Ресурс [1110614779](https://sandbox.yandex-team.ru/resource/1110614779/view) типа [COMMONMARK_BINARY](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/tutorial/common/__init__.py?rev=5897843#L14-20) уже содержит нужный нам статически собранный бинарь cmark. Можно скачать его в задачу напрямую по ID:

```python
def on_execute(self):
    ...
    cmark = sdk2.Resource[1110614779]  # Вернёт объект `CommonmarkBinary` заданного ресурса
    cmark_data = sdk2.ResourceData(resource)
    cmark_data.path  # -> объект типа `pathlib2.Path`, указывающий на файл или директорию ресурса
```

Ресурс скачивается (*синхронизируется*) на хост в момент создания объекта `sdk2.ResourceData`. Свойство `.path` указывает на скачанный файл или директорию ресурса (в данном случае — на исполняемый файл cmark).

{% note "Доступ на запись" %}
Файлы ресурсов будут доступны только на чтение и, возможно, на исполнение. Если вы хотите в них записывать — скопируйте файлы в директорию своей задачи.
{% endnote %}

Указывать ID ресурсов в коде задач — плохая практика. Как минимум, их будет сложнее обновить. Удобнее динамически находить самый свежий ресурс по заданному типу и набору критериев. Типичный паттерн поиска ресурса выглядит так:

```python
def on_execute(self):
    # Вернёт объект `CommonmarkBinary`
    # наиболее свежего релизнутого ресурса, либо `None`
    cmark = sdk2.Resource.find(
        type="COMMONMARK_BINARY",
        attrs={"released": "stable"}
    ).order(-sdk2.Resource.id).first()

    if not cmark:
        raise errors.TaskFailure("Could not find cmark")

    cmark.id  # -> 1110614779 (или другой, более свежий)
```

Если вместо `sdk2.Resource` использовать конкретный класс ресурса, аргумент `type` можно опустить:

```python
from sandbox.projects.tutorial import common
cmark = common.CommonmarkBinary.find(attrs={...}).first()
```

Добавьте в задачу `HELLO_%LOGIN%` динамический поиск ресурса COMMONMARK_BINARY и его скачивание. С помощью логирования убедитесь, что файл действительно находится по указанному в `ResourceData` пути.

Рекомендации при динамическом поиске ресурсов:

* Писать `order(-sdk2.Resource.id)` не обязательно — такая сортировка используется по умолчанию.
* Ресурс по заданным критериям может не найтись; эту ситуацию всегда нужно обрабатывать.
* Требование атрибута `"released"` говорит о том, что мы рассматриваем лишь вручную релизнутые, т.е. вручную «одобренные» ресурсы. В некоторых ситуациях это может быть не актуально.
* В production-задачах рекомендуется также добавлять аргумент `owner=self.owner`, чтобы пользователи за пределами вашей Sandbox-группы не могли случайно «подсунуть» в задачу посторонний ресурс.
* Аргументы `.find()` соответствуют query-параметрам метода [GET /resource](https://sandbox.yandex-team.ru/media/swagger-ui/index.html#/) в [Sandbox API](./sandbox-api.md).