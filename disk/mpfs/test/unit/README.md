### Добавление юнит тестов

#### 0. Располагаем новый тест

Выбирая место для нового теста следует придерживаться структуры production кода. Так при добавлении теста для методов DiskDataIndexer из модуля `mpfs/core/filesystem/indexer.py`, стоит расположить тесты в директории `test/unit/mpfs/core/filesystem/indexer`.

#### 1. Наследуем базовый тестовый класс

Базовым тестовым классом для юнит тестов является `NoDBTestCase` (из модуля `test.unit.base`). Этот тестовый класс изолирует MPFS от БД, замещая контроллер взаимодействия с ней dummy-версией такого контроллера.

```python
from test.unit.base import NoDBTestCase

class IsAllowedAudioTestCase(NoDBTestCase):
```

*Примечание*:

В коде MPFS есть много участков, исполняющихся на уровне модуля, поэтому импортировать из `mpfs` стоит внутри класса (когда, БД уже замещена):

```python
class IsAllowedAudioTestCase(NoDBTestCase):
    def setup_method(self, method):
        # Делаем импорт из mpfs
        from mpfs.core.filesystem import indexer
```

#### 2. Подготавливаем окружение для тестов

Действия по настройке окружения следует делать в [xunit-стиле pytest](http://pytest.org/latest/xunit_setup.html).

Так для теста метода `is_allowed_audio` нам нужен будет только объект класса `DiskDataIndexer`:

```python
    def setup_method(self, method):
       from mpfs.core.filesystem import indexer

       self.indexer = indexer.DiskDataIndexer()
```

#### 3. Добавляем собственно тесты

В тестах стоит располагать только проверки. При этом если для теста нужны небольшие тестовые данные, то для большей описательности теста можно располагать такие данные внутри тестового метода.

В итоге тесты метода `is_allowed_audio` могут выглядеть следующим образом:

```python
from hamcrest import assert_that, equal_to

from test.unit.base import NoDBTestCase


class IsAllowedAudioTestCase(NoDBTestCase):
    def test_not_a_file(self):
        item = {'type': "dir"}

        assert_that(self.indexer.is_allowed_audio(item), equal_to(False))

    def test_media_type_audio(self):
        item = {
            'type': "file",
            'media_type': "audio"
        }

        assert_that(self.indexer.is_allowed_audio(item), equal_to(True))

    def setup_method(self, method):
        from mpfs.core.filesystem import indexer

        self.indexer = indexer.DiskDataIndexer()
```
