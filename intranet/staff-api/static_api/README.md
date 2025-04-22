static-api
==========
django-app для организации readonly api в mongo.


required django settings
========================
`PAGE_SIZE` — (`int`) размер страницы с данными по умолчанию

`UPDATE_LIMIT` — (`int`) максимально количество сообщений, обрабатываемых за раз

`PROCESS_LOCK_TIMEOUT` — (`int`) таймаут для лока таски в секундах

`API_DEFAULT_RETRY_COUNTDOWN` — (`int`) число ретраев, которые делают таски

`STATIC_API_ENTITY_COLLECTIONS`  - (`list`) имена коллекций для сущностей

`STATIC_API_META_COLLECTIONS` - (`list`) имена служебных коллекций

`STATIC_API_MESSAGES_COLLECTION` - (`str`) имя коллекции для сообщений

`SERVICE_NAME` — (`str`) имя сервиса для документации

`API_VERSION` — (`str`) версия апи для документации

`API_HOSTNAME_PRODUCTION` — (`str`) хост апи в продакшне

`API_HOSTNAME_TESTING` — (`str`) хост апи в тестинге


Графики и мониторинг
====================
С помощью management-команды `apimasterdeltas` можно получить json с текущими
значениями отставания данных в api от master базы данных.

Ключи:

  * `delta_ids` разница между id последнего сообщения
  * `delta_time` задержка в секундах; -1 если задержка есть,
  но посчитать её нельзя (как во время самого первого init)


Можно вывести эти значения на график, прописав в настройку
`STATIC_API_GRAPHITE_METRIC_PREFIX` префикс вида `"one_sec.example_api"`,
и добавив таску `static_api.tasks.graphite` в celery beat на выполнение
раз в несколько секунд.
