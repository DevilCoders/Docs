### SecretSearch. Cython binding

Cython биндинг к SecretSearch, имеет очень аскетичный интерфейс:
```py
class Secret(object):
    __slots__ = ('secret', 'message', 'line_no', 'validated', 'additional')

class Searcher(object):
    def __init__(self, validate=False, valid_only=False, excludes=[], max_file_size=3<<20):
    """
    :param validate: производить ли валидацию найденного секрета
    :param valid_only: возвращать _только_ валидные секреты
    :param excludes: список исключений при итерации по директории (сейчас не используется)
    :param max_file_size: максимальный размер файла (актуально для .check_path)
    """

    def check_blob(self, content):
    """
    Поискать секретики. НЕ потокобезопасен.

    :param content: бинарная строка с контентом для поиска
    :return: генератор секретов
    """

    def check_path(self, path):
    """
    Поискать секретики в файле/папке. НЕ потокобезопасен.

    :param path: путь к файлу или директории
    :return: генератор секретов, возвращающий (path, secrets[])
    """
```

Пример использования: [junk/buglloc/secret-search/__main__.py](https://a.yandex-team.ru/arc/trunk/arcadia/junk/buglloc/secret-search/__main__.py)
