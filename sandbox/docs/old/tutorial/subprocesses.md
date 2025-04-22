Внешние утилиты и скрипты в Sandbox-задачах рекомендуется запускать с помощью `sdk2.helpers.subprocess`. Это дополнительно пропатченный бэкпорт стандартной библиотеки [subprocess](https://docs.python.org/3.2/library/subprocess.html) из Python 3.

В [прошлом разделе](./sync-resources.md) мы скачали в задачу ресурс с утилитой cmark. Её запуск для конвертации Markdown в HTML может выглядеть так:
```python
from sandbox import sdk2

def execute(self):
    ...
    with sdk2.helpers.ProcessLog(self, logger="cmark") as pl:
        sdk2.helpers.subprocess.check_call(
            [
                # cmark hello.md -o hello.html
                str(cmark_data.path),
                str(resource_data.path / "hello.md"),
                "-o",
                str(resource_data.path / "hello.html"),
            ],
            stdout=pl.stdout, stderr=pl.stderr,
        )
```

Контекстный менеджер `ProcessLog` сохраняет stdout/stderr подпроцесса в файлы cmark.out и cmark.err соответственно в директорию с логами. Без него логи работы процесса не сохранятся, что не позволит диагностировать проблему, если процесс вдруг упадёт с ненулевым кодом возврата. В качестве `logger` можно передать полноценные объекты логгеров из библиотеки [logging](https://docs.python.org/2/library/logging.html).
