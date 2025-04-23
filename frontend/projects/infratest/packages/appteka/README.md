# Appteka

Утилита, позволяющая сохранять входные дампы вершин AppHost и применять их на нужные вершины для дебага проблем.

## Подключение

Для работы с апптекой можно воспользоваться [yatool](https://wiki.yandex-team.ru/yatool/distrib/).

После установки `yatool` выполнить команду `ya tool appteka --help`.

Appteka работает на OS Linux и macOS.

Чтобы необходимые дампы сохранялись, нужно [Включить сохранение дампов для вершины в графе](#vklyuchitь-sohranenie-dampov-dlya-vershiny-v-grafe).


## Команды

### Отправить дампы (apply)

1. `ya tool appteka apply <Address> --reqid <ReqId> [--node Node] [--edit]`

2. `ya tool appteka apply <Address> --file <Path to file> [--edit]`

Пример использования:

1. `ya tool appteka apply grpc://localhost:33743 --reqid 1642778863647369-10905014385527642476-vla1-4643-vla-l7-balancer-8080-BAL --node .PRE_SEARCH_TEMPLATE_DATA_SETUP`
2. `ya tool appteka apply grpc://localhost:33743 --file ./src/__fixtures__/.PRE_SEARCH_TEMPLATE_DATA_SETUP.json`

Appteka может отправлять дампы либо взятые с SeTrace (в это случае должен быть обязательно указан `ReqId` и опционально `Node`), либо взятые из файла, хранящегося у пользователя (в данном случае должен быть обязательно указан параметр `File`). Опции `--file` и `--reqid|--node` являются взаимоисключающими, но одну из них необходимо указать. 

Если будет указан `ReqId` без указания `Node`, то по указанному адресу (`<Address>`) будут отправлены **все** имеющиеся для `ReqId` дампы apphost. Посмотреть список всех имеющихся `Node` для конкретного `ReqId` можно командой [list](#pokazatь-vse-vershiny-s-dampami-list).

Если указать опцию `--edit`, то перед отправкой дамп будет открыт в текстовом редакторе (берется из переменных окружения $VISUAL и $ENVIRONMENT) для внесения изменения, после чего измененный дамп будет отправлен по указанному адресу.

Appteka умеет работать с протоколами `neh` и `grpc`, протокол определяется автоматически из полученных данных, которые затем отправляются в нужном формате в вершину по этому же протоколу. Адрес нужно указать в формате `post://localhost:3000` для `neh` протокола и `grpc://localhost:3000` для `grpc` проткола.

Форматы дампов: [neh](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/appteka/src/__fixtures__/.WEB_SEARCH.WEB1.NOAPACHE_ADJUSTER.json), [grpc](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/appteka/src/__fixtures__/.PRE_SEARCH_TEMPLATE_DATA_SETUP.json)

### Сохранить дампы (save)

`ya tool appteka save --reqid <ReqId> [--node Node]`

Пример использования:

`ya tool appteka save --reqid 1642778863647369-10905014385527642476-vla1-4643-vla-l7-balancer-8080-BAL --node .PRE_SEARCH_TEMPLATE_DATA_SETUP`

Команда сохраняет указанные дампы в директорию, из которой была вызвана, и выводит в терминал пути к ним. Если будет указан `ReqId` без указания `Node`, то будут сохранены **все** имеющиеся по указанному `ReqId` дампы apphost. Посмотреть список всех имеющихся `Node` для конкретного `ReqId` можно командой [list](#pokazatь-vse-vershiny-s-dampami-list).

Форматы дампов: [neh](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/appteka/src/__fixtures__/.WEB_SEARCH.WEB1.NOAPACHE_ADJUSTER.json), [grpc](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/appteka/src/__fixtures__/.PRE_SEARCH_TEMPLATE_DATA_SETUP.json)

### Показать все вершины с дампами (list)

`ya tool appteka list --reqid <ReqId>`

Пример использования:

`ya tool appteka list --reqid 1642778863647369-10905014385527642476-vla1-4643-vla-l7-balancer-8080-BAL`


Команда list выводит для указанного `ReqId` в терминал список всех `Node`, у которых есть дампы `Apphost`.
Идентификаторы вершины выводятся в формате `<ПУТЬ_ДО_ВЕРШИНЫ>` из опции [json_dump_requests](https://docs.yandex-team.ru/apphost/pages/cgi#json_dump_requests).

Если по указанному `ReqId` не найдено ни одной вершины с дампами, возможно, они не сохраняются (см. пункт [Включить сохранение дампов для вершины](##vklyuchitь-sohranenie-dampov-dlya-vershiny-v-grafe)).

### Опции

* Address  - адрес вершины аппхоста, куда нужно отправить дамп, обязательный параметр, должен иметь формат `post://localhost:3000` для `neh` протокола и `grpc://localhost:3000` для `grpc` проткола.
* ReqId (-r)  - request id, уникальный идентификатор запроса пользователя, обязательный параметр для `save` и `list`, необязательный параметр для `apply`
* Node (-n)  - идентификатор вершины, поведение аналогично опции [json_dump_requests](https://docs.yandex-team.ru/apphost/pages/cgi#json_dump_requests), необязательный параметр
* File (-f) - адрес к дампу, хранящемуся локально, необязательный параметр
* Edit (-e) - если опция указана, то перед отправкой дамп будет открыт в текстовом редакторе для внесения изменения, необязательный параметр для `apply`

## Включить сохранение дампов для вершины в графе

Чтобы Appteka могла получать необходимые дампы, нужно указать в конфиге графа [dump_error_requests=true](https://docs.yandex-team.ru/apphost/pages/node_params#logging_config), в этом случае AppHost всегда логирует `TSourceRequest` , если запрос завершился **с ошибкой**.

Чтобы AppHost логировал `TSourceRequest` при **удачных** запросах тоже, нужно установить в конфиге графа опцию [dump_request_probability=1](https://docs.yandex-team.ru/apphost/pages/node_params#logging_config).

Пример можно посмотреть в графе [renderer_pcode](https://horizon.z.yandex-team.ru/backends/json/RENDERER_PCODE/9049009/trunk).

Эти ошибки не логируются:
* «connection refused».
* «connection timed out».
* HTTP 503 с текстом «too many requests in progress».
* HTTP 503 c текстом «service suspended».

## Откуда appteka берет дампы

Appteka берет данные из параметра `TSourceRequest`, который логируется `AppHost`. Данные хранятся в SeTrace и достаются оттуда по `ReqId`, поэтому на использование апптеки действуют такие же ограничения, как и на использование `SeTrace` - если данные по `ReqId` не были запрошены в течении нескольких часов после исследуемого запроса, то они удаляются и получить их становится невозможно. Если `ReqId` был запрошен и вернул данные, то они будут доступны в SeTrace (а значит и в Апптеке) еще 2 месяца.

## Куда appteka отправляет дампы

В команде `apply` в опции `<Address>` можно указывать как продовые вершины, так и поднятые локально. 

Дампы с протоколом [neh](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/appteka/src/__fixtures__/.WEB_SEARCH.WEB1.NOAPACHE_ADJUSTER.json) совместимы с утилитой [servant_client](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/tools/servant_client).

Дампы с протоколом [grpc](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/appteka/src/__fixtures__/.PRE_SEARCH_TEMPLATE_DATA_SETUP.json) совместимы с утилитой [grpc_client](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/tools/grpc_client).

Принцип работы `servant_client` и `grpc_client` описан в [документации аппхоста](https://docs.yandex-team.ru/apphost/pages/manual_requests). Appteka использует для отправки биндинги к этим утилитам. 

## Поднять вершину локально

Для того, чтобы получить поведение аналогичное продовому у себя локально, нам нужно запустить report renderer с нужным шаблоном.

Есть 2 способа это сделать:

1) Многие сервисы предоставляют возможность запуститься локально. Например, [web4](https://a.yandex-team.ru/arcadia/frontend/projects/web4). Локальный запуск сервиса, использвующего рендерер, в любом случае запускает рендерер, и в логах появится порт, который нужно затем использовать в `--address`. Минус этого решения в том, что запускается последняя версия и для дебага старых проблем это может не подойти - код мог успеть поменяться и начать вести себя по-другому.

2) Чтобы поднять точно такую же вершину, как была в проде в момент фейла, можно скачать ресурс с Sandbox, определив дату по времени фейла. Далее запускаем рендерер с помощью команд:
```
mkdir test-pcode
cd ./test-pcode
wget http://s3.mds.yandex.net/sandbox-3069/2745712661/pcode-templates.tar.gz
tar -xpf pcode-templates.tar.gz
ya tool renderer --templates-package routes.json -p 3000 --apphost-service
```
Название папки и архив взяты для примера, вместо файла `routes.json` также может быть `routes.js`.
В другом терминале открываем логи (папка `logs` появится сразу после запуска рендерера в месте запуска):

```
cd logs
tail -f *
```

## Инструкция для разработчика appteka

Для внесения изменений в код апптеки можно воспользоваться [инструкцией](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/appteka/DEV.md).

## Возможные ошибки, с которыми может столкнуться пользователь при использовании appteka
### Не получается сделать запрос к SeTrace
Возможно, нет доступа. Нужно его запросить для вашей вертикали в [Puncher](https://puncher.yandex-team.ru/?create_destinations=setrace.yandex-team.ru&create_locations=vpn,office&create_ports=80%2C%20443&create_protocol=tcp&create_sources=%40srv_svc_reportrenderer%40&create_until=persistent) (заменить `reportrenderer` на нужный ABC сервис).

### Дамп для указанной пользователем Node не найден
Нужно вывести все пути вершин apphost, для которых сохранен TSourceRequest по этому `ReqId` c помощью команды `appteka list -r`.
