## Жизненный цикл
 * [Render](#render)
 * [Validation](#validation)
 * [Conflicts resolving](#conflicts-resolving)
 * [Throttling](#throttling)
 * [Execution](#execution)
   * Revision -> Job
   * Job -> Task
 * [Reporting](#reporting)

### Render [(source)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/manager/renderer.go)
Язык выражений, доступные функции и переменные описаны в [CONTEXT.md](./CONTEXT.md).

### Validation [(source)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/manager/validator.go)
### Conflicts resolving [(source)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/manager/conflicts_resolver.go)
В ситуации, когда 2 юнита на хосте не могут поделить один ресурс (два юнита хотят поставить один пакет / поменеджить один файл) могут происходить плохие вещи (e.g. пакеты будут переустанавливаться при каждом запуске hostctl). Для избежания такого придуман механизм conflicts resolving.

#### Про то как он работает:
1. Перед каждым запуском hostctl мы имеем слоты с current и removed ревизиями
2. При запуске могут придти новые конфигурации юнитов
3.  На основе этих конфигураций формируются новые ревизии (старая CURRENT становится REMOVED, по новой конфигурации формируется новая CURRENT).
4. Все ревизии после применения новых конфигураций разбиваются на таски (для CURRENT -> install/manage/run_porto, для REMOVED -> uninstall/remove/destroy_porto)
5. Для разрешения конфликтов зовем [CheckConflicts](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/tasks/conflicts.go) попарно для всех CURRENT ревизий
6. На основе колличества конфликтов для ревизий строится priority queue, где самый большой приоритет имеют ревизии с самым большим количеством конфликтов
7. С очереди снимается ревизия с самым большим приоритетом, которая получила изменения в текущем запуске hostctl и откатывается к предыдущей CURRENT
8. Если конфликтов до сих пор остались возвращаемся к шагу 6

Таким образом мы разрешим все конфликты (в худшем случае откатимся к стейту, который был пере очередным запуском hostctl).

### Throttling [(source)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/manager/throttle.go)
Все юниты, получившие изменения в конфигурации перед запуском джобов тротлятся об [Orly](https://wiki.yandex-team.ru/runtime-cloud/orly/). Если orly запретил применения новой конфигурации, применяется старая.

### Execution [(source)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/manager/exceute.go)
#### spec -> Revision
* При чтении новых конфигураций юнитов, получивших изменения
([SHA1 от protobuf spec пришедшего юнита отличается от spec текущей CURRENT ревизии](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/protoiterfaces/porto_daemon.go?rev=7164180#L105)),
создается новая CURRENT ревизия.
* Старая CURRENT становится REMOVED
#### Revision -> Job
* Для REMOVED ревизии создается [RemovedJob](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/revjob/removed.go) с `uninstall/remove/destroy_porto` тасками
* Для CURRENT ревизии создается [CurrentJob](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hostctl/internal/units/revjob/current.go) с `install/manage/run_porto` тасками
* Делаем prune каждой джобы с каждой для исключения идентичных тасков (для того чтобы не делать идентичные действия)
* Поочередно выполняем джобы
* Если все джобы для REMOVED ревизии выполнились успешно, удаляем ревизию из стейта
#### Tasks
* Install (установка set'а пакетов)
> Проверяем установлены ли актуальные версии пакетов командой `/usr/bin/dpkg-query -W -f="${Package}\t${Version}\t${Status}\n"`
>
> Если пакеты не установлены или установлены не актуальные версии,
> устанавливаем set пакетов командой `/usr/bin/apt-get install -q -y -o DPkg::Options::=--force-confold -o DPkg::Options::=--force-confdef --force-yes`
* Manage (приведение файлов в состояние описанное в spec юнита)
* RunPorto (запуск porto контейнера)
  * проверяем запущен ли контейнер в актуальной конфигурации
  * если запущен в актуальной конфигурации, завершаем таск
  * разрушаем контейнер
  * запускаем контейнер в актуальной конфигурации
* Uninstall (удаление set'a пакетов)
* Remove (удаление файлов)
* ShutdownPorto (разрушение porto контейнера)
  * Вызываем DisablePorto
  * Вызываем KillPorto
  * Ждем таймаут, пока porto завершится
  * Если после таймаута porto продолает работать вызываем DestroyPorto
### Reporting
После выполнения всех джобов hostctl рапортует статусы юнитов в [HM-reporter](https://a.yandex-team.ru/arc/trunk/arcadia/infra/hmserver/docs/HM_REPORTER.md) / YASM / JUGGLER
