# А что делать с миграциями
Когда ты добавил новую вурсию конфига, надо произвести несколько миграций

Первая - миграция статический файлов в тестсьютах клиентских сервисов (сейчас это yagr, yaga, yaga-metrolog, internal-trackstory) для того, чтобы сервис смог подняться и рабоать (если миграцию не произвести, то сервис, поддерживающий схему версии n будет получать схему версии n - 1, которую скорее всего не сможет распарсить).

Вторая - миграция в базе данных. При переходе на новую версию control-plane будет брать из базы данных конфиги новой версии. Если миграцию не прозвести, то конфигов не будет и сервисы будут получать пустой список конфигов.

## Как писать код
Для миграций нужно реализовать функцию, котоая будет изменять конфиг соответствубщим бразом. Эту функцию надо ркализовать по следующему шаблону:

В файле `services/geo-pipeline-control-plane/scripts/migration/migration_tools/to_{new_version}.py` надо написать следующий класс-мигратор по шаблону

```(python)
import json
from . import i_migrator
from typing import Dict


class Migrator(i_migrator.Migrator):
    @staticmethod
    def get_version() -> int:
        return # new version

    @staticmethod
    def migrate(config) -> Dict:
        # your code here...
        return config

```

Этот класс будет цепляться из скриптов для миграций

## Тесты
Нужны тесты.

Во-перых это нужно вам, чтобы не поломать случайно миграцию, во-вторых наличие тестов будет обязательно проверяться при запуске миграций (по крайней мере для базы данных)

Все, что нужно это написать два файла -

`services/geo-pipeline-control-plane/scripts/migration/tests/input_{new_version}.py`

и

`services/geo-pipeline-control-plane/scripts/migration/tests/expected_{new_version}.py`

С конфигами того, что было и что должно быть, соответственно.

## Запуск скриптов
- `python3 scripts/migration/run_tests.py` - запуск тестов
- `python3 scripts/migration/migrate_static_files.py --version-to-migrate={new_version}` -  запуск миграций статическийх файлов тестсьюта сервисов
- ***TODO*** - запуск миграции бд
