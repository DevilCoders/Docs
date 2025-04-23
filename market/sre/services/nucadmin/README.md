# Nucadmin

## Get started
1. Поднимаем базу `docker-compose -f deployments/docker-compose.develop.yaml up`
2. Создаем необходимые таблицы в базе `docker-compose -f deployments/docker-compose.develop.yaml exec database psql` и вручную вкидываем SQL команды из скрипта миграции методом обычной копипасты
3. Собираем фронт `cd website && npm run build && cd -`
4. Собираем бэк `ya make`
5. Запускаем сервер ./nucadmin runserver --config configs/develop.yaml

## Configs
Конфиги хранятся в [секретнице](https://yav.yandex-team.ru/?search=nucadmin).

### config.yaml
Конфиг самого приложения.
* `server`: секция конфига http сервера приложения
* `storage`: секция подключения приложения к базе
* `clientPath`: указываем бэку, куда положили файлы скомпилированного фронта, ибо он их сервит
* `swagger`: секция конфигов свагера
* `tvmtoolclient`: клиент TVM демона
  * `url`: куда делать запросы
  * `src`: свой ID
  * `authtoken`: токен, который передали TVM демону при запуске
* `idm`: секция конфигов IDM
* `testmode`: секция конфига для запуска в режиме локальной отладки. <span style="color:red">****Ни в коем случае не использовать на проде!!****</span>
  * `fakeUID`: UID, который будет присваиваться всем запросам
  * `fakeIDMAuth`: _true_, если нужно подергать IDM ручки без токена
  * `fakeBBAuth`: _true_, если нужно подергать API ручки без куки Session_id от имени _fakeUID_

### tvmticket
Строка с ключем TVM, должна совпадать со строкой _tvmtoolclient.authtoken_ из **config.yaml**.
Подробности, зачем она нужна, читать в [описании tvm-daemon](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#kakzapustitprocess).

### tvmtoolconfig.json
[Конфиг TVM демона](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#konfig).

## Структура проекта

* `api`:
    * `swagger.yaml`: swagger описание предоставляемого api
* `build`:
    * `package.json`: описание сборки пакета
* `cmd`: директория с командами, которые будут доступны для вызова из итогового бинаря
* `configs`: здесь лежат примеры конфигов приложения, которые можно использовать для локальной отладки
* `deployments`: здесь лежат файлы, необходимые для развертывания приложения
* `main.go`: точка входа
* `scripts`:
    * `migrations`: скрипты миграции базы данных
    * `manual_local_tests`: заготовки для ручного тестирования
* `internal`:
    * `commands`: реализация команд из `cmd`
        * `context.go`: расширение контекста доп. полями для типизированного использования в `actions`
    * `core`: основная логика
        * `actions`: функции, выполняющие какие-то действия и возвращающие результат. Не завязаны на веб-сервер, можно вызвать из любого места. Зависят по входным данным только от кастомного контекста.
        * `entities`: сущности, в частности представление таблиц из базы в коде
        * `config.go`: структура конфига и функция парсинга
        * `payloads`: сущности клиентского ввода, используются для того что бы распарсить JSON в теле или параметры запроса, валидировать и на их основе составить слайс опций для вызова action
    * `server`: релизация web-сервера
        * `handlers`: функции, обрабатывающие запрос. На вход - http-request, на выходе запись ответа. Вызывают `actions` (см. выше) для формирования ответа
        * `app.go`: оболочка к http-серверу
        * `context.go`: адаптор, преобразующий контекст к кастомному контексту, чтобы не кастить в каждом `handler`'е
        * `middlewares.go`: локальные `middlewares`
        * `router.go`: сопоставление путей и `handler`'ов
    * `storage`: работа с хранилищами данных
    * `botclient`: клиент к ятимовскому боту
    * `idm`: модуль для работы с idm
    * `tvmtoolclient`: модуль для работы с TVM
* `website`: тут лежит фронтенд и все, что с ним связано

## Runtime
Сервис запускается в nanny:
- тестовый инстанс во [VLA](https://nanny.yandex-team.ru/ui/#/services/catalog/testing_market_nucadmin_vla/);
- продовые в [SAS](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_nucadmin_sas/) и во [VLA](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_nucadmin_vla/);

Для работы используется СУБД Postgres MDB в YC: [тест](https://yc.yandex-team.ru/folders/fooeehq0fj9a6o9c6fe1/managed-postgresql/cluster/mdbg6es4lt8p617gj7qc?section=overview) и [прод](https://yc.yandex-team.ru/folders/fooeehq0fj9a6o9c6fe1/managed-postgresql/cluster/mdbg6es4lt8p617gj7qc?section=overview)

## Deploy
Катится через пайплайн [ЦУМ](https://tsum.yandex-team.ru/pipe/projects/sre/delivery-dashboard/nucadmin)

## Integrations

### CUPS
Все принтера, имеющиеся в nucadmin, с прописанным или автосгенерированным именем попадат в соотвествующие CUPS.
Для этого на стороне nucadmin реализована ручка [/api/other/printer/cups](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/services/nucadmin/internal/server/router.go?rev=r8820620#L436).
Ручка принимает GET параметром warehouse_id и отдаёт только те принтеры, которые относятся к складу с указанным id.
Можно запросить сразу несколько складов, например https://nucadmin.market.yandex-team.ru/api/other/printer/cups?warehouse_id=1&warehouse_id=12warehouse_id=45.
На стороне сервера с cups работает по крону тулза [cups-nucadmin-sync](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/tools/cups-tools/cmd/cups-nucadmin-sync), которая синхронизирует имеющие в CUPS принтера в соотвествии с тем, как задано в ёё конфиге.
Дефолтный [конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/tools/cups-tools/static/etc/yandex/cups-tools.toml) снабжен годными комментариями. Путь к конфигу захардкожен на /etc/yandex/cups-tools.toml

### WMS
Работает аналогично предыдущей синхронизации. Ручка [/api/other/printer/wms](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/services/nucadmin/internal/server/router.go?rev=r8820620#L441).
GET параметры аналогичные. Тулза [wms-nucadmin-sync](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/tools/cups-tools/cmd/wms-nucadmin-sync). Использует тот же файл конфига.

### DNS
На стороне nucadmin реализована ручка [/api/other/dns/wh](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/services/nucadmin/internal/server/router.go?rev=r8820620#L451)
Со стороны DNS в неё ходит [тулза](https://st.yandex-team.ru/DNS-600) и забирает адреса. Ручка намеренно фильтрует адреса и отдаёт только сущности, которые относятся к .wh.market.yandex.net

### Conductor
Для каждого склада в nucadmin задано значение *conductor_group_id* (вручную при заведении склада).
При заведении новой станции nucadmin заводит её же в Conductor, попутно, сохраняя id станции в кондукторе в поле *conductor_host_id*.
При редактировании станции nucadmin сообщает об изменениях в Conductor, а при удалении соотвественно удаляет станцию из conductor.

## Explanation

### AAA
Для аутентификации сервис требует проставленную [ятимовским паспортом](https://passport.yandex-team.ru) куку Session_id
Отдельно обрабатываются кейсы, когда в сервис ходят АРМы самостоятельно.

Для авторизации используется [IDM](https://idm.yandex-team.ru/system/nucadmin/roles#f-status=all,f-role=nucadmin,sort-by=-updated)

#### Роли
В системе предусмотрены следующие роли:
* `global_wh_writer` - роль дает право добавлять/удалять склады, а так же редактировать их параметры
* `global_params_writer` - роль дает право добавлять/удалять/редактировать модели устройств, типы рабочих станций, рабочие страницы
* `wh_%d_adder` - роль дает право добавлять/редактировать/удалять оборудование на складе с id `%d` (подставить вместо %d id склада - для каждого склада отдельная роль)
* `wh_%d_adder` - роль дает право выпускать сертификаты и редактировать work_pages на складе с id `%d`
