Более полная документация по счётчикам на wiki: https://wiki.yandex-team.ru/search-interfaces/multimedia/counters/

## Blockstat

Добавить новый счетчик можно [здесь](https://stat.yandex-team.ru/DictionaryEditor/blockstat), для этого необходимо запросить права [здесь](https://idm.yandex-team.ru/#rf-role=yfdbccte#stat/groups/blockStatEditor;;;,rf-expanded=yfdbccte,rf=1). После этого необходимо обновить `blockstat.dict.json` — `bin/updateBlockstat`.

Если необходимо пробросить счётчик на клиент — обращайтесь к @yurich. Или попробуйте посмотреть на `bin/updateCounters`.

**Общая схема при добавлении нового счетчика (или, если у вас не расшифровывается числовое значение)**

1) Убедиться, что счетчик есть в списке https://stat.yandex-team.ru/DictionaryEditor/blockstat. Если нет - добавить.

2) Убедиться, что счетчик есть в [blockstat.dict.json](blockstat.dict.json). Если нет - запустить скрипт `bin/updateBlockstat`

3) Если счетчик нужен на клиенте, то его необходимо добавить в словарь для клиента. Словари разбиты по платформам/сервисам. Например, для touch в images [images/blocks-touch/counter/counter.priv.js](images/blocks-touch/counter/counter.priv.js). Ищите подходящий вам словарь.

4) Если вы выполняли пункт 3, то надо запустить `bin/updateCounters`, указав первым аргументом путь к платформе (например, `bin/updateCounters images/blocks-touch`)

5) Все готово, коммитим, наслаждаемся
