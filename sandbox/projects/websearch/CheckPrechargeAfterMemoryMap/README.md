### Описание
Тест предназначен для нахождения мест, где поисковая компонента на старте отображает файл в память,
но не считывает его с диска (вызов [TMemoryMap::Map](https://a.yandex-team.ru/arc/trunk/arcadia/util/system/filemap.h?rev=4037684#L81) без флага oPrecharge).
Подобное поведение может привести к тому, что на первые запросы компонента будет отвечать сильно дольше или вовсе отдавать пятисотку, если очередь запросов переполнится.

Сделано в рамках [NOAPACHE-50](https://st.yandex-team.ru/NOAPACHE-50) по мотивам [SPI-1240](https://st.yandex-team.ru/SPI-1240), [SPI-4253](https://st.yandex-team.ru/SPI-4253).

### Как добавить новую компоненту
1. В поддиректории [components](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/CheckPrechargeAfterMemoryMap/components) надо создать файл с классом компоненты,
отнаследовать его от Component из [component.py](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/CheckPrechargeAfterMemoryMap/component.py) и переопределить методы.
2. Записать имя файла в [PY_SRCS](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/CheckPrechargeAfterMemoryMap/components/ya.make).
2. Добавить в [`__init__.py`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/websearch/CheckPrechargeAfterMemoryMap/__init__.py) в словарь COMPONENTS новую компоненту.

### Примечание
- Бинарь компоненты должен быть собран в debug-сборке.
