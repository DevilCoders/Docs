# Генерация файлов зон

Файл зоны ([Zone file](https://en.wikipedia.org/wiki/Zone_file)) - классический вариант представления DNS зоны, который представляет из себя текстовый файл со списком всех записей.
На этой странице приведена релевантная информация к этому процессу.

## Описание процесса

Файлы зон генерируются раз в полчаса и сохраняются в виде ресурсов типа `DNS_ZONE_FILE` в Sandbox.
Для этого запущен [шедулер](https://sandbox.yandex-team.ru/scheduler/44765/view) в Sandbox.
Каждый запуск задачи генерирует файлы для всех известных зон.
Внутри задачи запускается тулза [generate_zonefiles](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns/tools/generate_zonefiles),
именно она выполняет работу по выкачиванию данных из YP и составлению файлов.

## Особенности процесса и тудушки

На момент написания статьи известны следующие недостатки процесса:

- Список зон, для которых нужно сгенерировать файлы, берется из [вкомпилированного](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns/tools/generate_zonefiles/lib/config_loader.cpp?rev=r9455095#L51) json-конфига в тулзу и обновляется только в случае пересборки тулзы.
- Также нет поддержки [динамических зон](../yp_dns_api/api.md#create-zone).
- В файл зоны [добавляются](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns/tools/generate_zonefiles/lib/zone.cpp?rev=r9455095#L78-85) `SOA` и `NS` записи, сгенерированные по конфигу зоны, даже если записи этих типов явно присутствуют в YP.
- В [статической](../yp_dns_api/api.md#zone-config) `SOA` записи `serial number` [всегда 0](https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns/tools/generate_zonefiles/lib/zone.cpp?rev=r9455095#L79-80).

## Ссылки

- Шедулер в Sandbox: <https://sandbox.yandex-team.ru/scheduler/44765/view>.
- Тикет на создание процесса: <https://st.yandex-team.ru/YP-3145>.
- Код тулзы: <https://a.yandex-team.ru/arc/trunk/arcadia/infra/yp_dns/tools/generate_zonefiles>.
