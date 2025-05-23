# S3Lib.lua

Библиотека интеграции S3 и nginx.
Позволяет nginx выдергивать из входящих запросов имя бакета,
ограничивать частоту запросов с помощью YARL, проверять возможность публичного доступа к бакету и т.п.

В представлении автора в эту библиотеку должен постепенно съехать весь имеющий отношение к S3 inline-код
из nginx-конфигов. Такой подход убивает сразу несколько зайцев:
* кодовая база собирается в одном месте, в nginx остаются только несколько точек входа: вызов
  одной-двух функций и из *_by_lua_block и всё.
* можно пользоваться IDE для работы с кодом (подсветка синтаксиса, suggest'ы,
  автоматическое обнаружение явных ляпов и т.п.).
* можно тестировать изменения в коде в изолированной среде: docker-контейнер, подключение
  lua-библиотеки в тестовую конфигурацию nginx'а и выполнение запросов.

## Структура кода
Большая часть кода внутри S3Lib откомментирована. Предполагается, что этого достаточно для понимания назначения
каждого из компонентов кода, а так же смысла их появления, однако есть вещи которые сложно отразить в коде даже в
виде комментариев.

Вот список модулей и их основное назначение, которое может быть неочевидным из самого кода:

* `lib.lua` - основная точка входа в библиотеку. Как правило, все использования S3Lib в nginx - это прямые вызовы
  методов из файла `lib.lua`, т.е. в nginx всегда достаточно сделать
  `S3Lib = require 's3.lib'; S3Lib.init(); S3Lib.<some action>()`.
  Единственный модуль в библиотеке, функции которого самостоятельно принимают решения о немедленном ответе клиенту
  или как-то мутируют ответ (выставляют заголовки).
  > Например, функция проверки публичного доступа к бакету не вернёт значение "можно-нельзя", она прям оборвет обработку
  и сама вернёт клиенту 403 в случае запрета.
  >
  > Функции остальных модулей не должны мутировать ответ,
  они возвращают какое-то значение в коде и не прерывают поток обработки.
  Например, та же функция проверки публичного доступа к бакету в модуле `open_buckets` просто вернёт `true` или `false`,
  никак не влияя на ответ клиенту.
* `open_buckets.lua` - весь код про контроль публичного доступа к бакетам: синхронизация настроек в shared-memory,
  периодическое их кеширование в локальной памяти worker'а, проверка возможности доступа и т.п.
* `private-api.lua` - простенький клиент к S3 Private API для nginx'а. Позволяет работать с API даже вне контекста
  запроса (без subrequest'ов). Потребовалось для `open_buckets.lua`.
* `values.lua` - интерфейсы для доступа к разным шаренным переменным и параметрам. Например, к данным о запросе и
  переменным, заданным в конфиге nginx'а.
* `internal.lua` - всякие внутренние функции-helper'ы. То, что не нужно "экспортировать" в nginx.
  > Предполагается, что этот модуль никогда не подключается напрямую в конфиге nginx и вызовы всех функций в нём
  происходят только из других модулей S3Lib. 
  >
  > `internal.lua` не импортирует никакие другие модули S3Lib кроме "стандартной библиотеки" - штук, 
  > которые ну совсем уж общие и вообще не имеют отношения конкретно к S3.
  >
  > Это гарантирует, что любой другой модуль S3Lib может импортировать `internal.lua` и не впороться 
  > в циклические зависимости.
* `lock.lua` - убогенькая реализация локов nginx между worker'ами через shared memory. "Убогенькая" потому, что
  полностью гонки не исключает и с ней всё-равно возможно споткнуться. Залетное место помечено большим комментом внутри
  библиотеки. Не поленись и ознакомься с ним (или поправь эту доку, если кто-то нашёл способ исправить гонку).
* `log.lua` - обертки для логирования событий в библиотеке.
  > Можно считать это куском той самой "стандартной библиотеки", которая упомянута выше.
* `files.lua` - честно краденый код из примеров документации к lua о работе с файлами.
  Чуть-чуть адаптированный и причёсанный.
  > Можно считать это куском той самой "стандартной библиотеки", которая упомянута выше.
  > По-хорошему её надо выкинуть из S3Lib куда-то в сторону `signal.lua`

## Дополнительные файлы
* `values.conf` - переменные, через которые nginx может "общаться" с `values.lua`. Файл должен быть подключен в
  `server {`, в котором использется S3Lib
* `shared_dicts.conf` - dict'ы, через которые worker'ы общаются между собой.
  Локи, настройки открытых бакетов, "вотэтовсё". Они не используются напрямую в конфиге nginx, но lua не может
  объявить их сам. Для объявления dict'ов файл должен быть подключен в `http {` (!НЕ server!), сайты которого
  используют S3Lib.
* `private-api.json` - конфигурационный файл клиента к S3 Private API. Читается клиентом напрямую с ФС, подключать его
  никуда не нужно.
* `dev` - набор кофигураций и разработческой магии для локального тестирования S3Lib. Подробности в README внутри.


## Как тестировать библиотеку

Всё для локального тестирования лежит в `./dev`. Подробности в README внутри.

## open_buckets.lua - синхронизация настроек открытых бакетов.

Основные концепции:
* настройки публичного доступа хранятся в lua shared dict
* каждый worker может обновить данные из S3 private и сохранить их в shared dict 
* для исключения гонок и одновременного обновления данных (чтобы не насиловать зря s3-private) процесс синхронизации должен запускаться под локами (это делет `lib.lua`)

`OpenBuckets.refresh()` должен периодически запускаться каким-то внешним процессом. Он ходит в S3 Private API, получает оттуда список публичных бакетов и их настройки, сохраняет это всё в shared memory. Кроме того модуль кеширует настройки бакетов в файл на диске, чтобы восстановиться, если после рестарта nginx вдруг окажется недоступен S3 Private API.

Частота синхронизации и ttl записей в shared dict задаётся в `lib.lua` в момент инициализации воркера.

После каждой успешной синхронизации shared memory чистится от старых записей:
* Старые записи для обычных бакетов не удаляются напрямую, это присходит за счёт истечения времени жизни записи (стандартные механизмы lua shared dict). 
* Старые записи для regex-правил доступа удаляются из shared memory явно.

Для того, чтобы видеть, что синхронизация работает, достаточно следить за возрастом файла с кешом настроек публичного доступа к бакетам. У нас есть на это мониторинг.
