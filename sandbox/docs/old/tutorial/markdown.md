В задаче `HELLO_%LOGIN%` создаётся ресурс с Markdown-файлом. В дальнейших разделах руководства вам предстоит сгенерировать из него HTML-файл несколькими разными способами. Получившийся файл нужно добавить в ресурс: вместо одного файла он должен хранить директорию с `.md` и `.html` файлами.

# Ресурс с директорией { #directory_resource }

В первую очередь, задачу надо переписать так, чтобы создаваемый ресурс хранил директорию, а не файл:
```python
def on_execute(self):
    ...
    resource = Greeting(
        task=self,
        description="Created by Sandbox task #{}".format(self.id),
        path="./greetings"  # директория с файлами ресурса
    )
    resource_data = sdk2.ResourceData(resource)
    resource_data.path.mkdir()  # создать директорию `greetings`

    text = ...
    with (resource_data.path / "hello.md").open("w") as f:
        f.write(text)
```


# Работа с Markdown { #markdown }

Для конвертации будем использовать [CommonMark](https://commonmark.org): стандартизированный диалект Markdown. В частности, именно его использует Arcanum для рендеринга `.md` файлов.

Для работы с ним существует Python библиотека-commonmark, представленная как в [PyPI](https://pypi.org/project/commonmark), так и в Аркадии ([contrib/python/commonmark](https://a.yandex-team.ru/arc/trunk/arcadia/contrib/python/commonmark)):

```python
import commonmark
text = "# Hello %username%!"
html = commonmark.commonmark(text)  # -> '<h1>Hello %username%!</h1>\n'
```

Кроме этого, пакет предоставляет консольную утилиту `cmark`:
```bash
$ cmark hello.md -o hello.html
```

В Аркадии её можно статически собрать бинарном виде:

```bash
arcadia$ ya make sandbox/projects/tutorial/common/cmark
Ok

arcadia$ sandbox/projects/tutorial/common/cmark/cmark --help
usage: cmark [-h] [-o [O]] [-a] [-aj] [infile]
```

Один из этих способов нужно будет использовать в задаче, если в ней выставлен соответствующий параметр:
```python
def on_execute(self):
    ...
    if self.Parameters.create_html:
        html = ...  # md -> html
        with (resource_data.path / "hello.html").open("w") as f:
            f.write(html)
```

В следующих разделах мы разберём, как именно можно доставить и использовать commonmark в коде задачи.
