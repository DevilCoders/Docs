### Бандл конфигов свежести

Конфиги генерируются таской [ASSEMBLE_REFRESH_CONFIGS](https://sandbox.yandex-team.ru/tasks?type=ASSEMBLE_REFRESH_CONFIGS&children=true&hidden=true&status=RELEASED&limit=20)

Идентичны для всех окружений: basesearch-refresh и environment
OxygenOptionsRt.cfg для всех окружений получается путём применения патча 
`OxygenOptionsRt.cfg.patch` к `OxygenOptions.cfg` данного окружения

`OxygenOptions.cfg-frozen.patch` и `OxygenOptions.cfg-isolated.patch` прикладываются к `OxygenOptions.cfg` 
утилитой **patch** для получения `OxygenOptions.cfg` для frozen и isolated окружений соотвественно.

`rtyserver.conf-frozen_patch.json` и `rtyserver.conf-isolated_patch.json` прикладываются к rtyserver.conf-common 
[патчером yconf](https://a.yandex-team.ru/arc/trunk/arcadia/library/cpp/yconf/patcher) для получения `rtyserver.conf-common` 
для frozen и isolated окружений соотвественно.

yconf патчер доступен в виде оригинальной C++ библиотеки, 
[python обёртки](https://a.yandex-team.ru/arc/trunk/arcadia/library/python/yconf_patcher) и 
[консольной утилиты](https://a.yandex-team.ru/arc/trunk/arcadia/search/tools/config_patcher).
С помощью тех же инструментов можно построить diff между двумя конфигами. 

### Список суффиксов и окружений:
- без суффикса - production Samohod
- frozen - замороженный хамстер
- isolated - хамстер
- news_quiсk - новый новостный контур
- news_quick_prestable - престейбл новостного контура
- staging - стейджинг Mercury
- staging_base - стейджинг для приемки rtyserver
- quick2 - экспериментальный контур Самохода
- samokhod_beta2 - второй экспериментальный контур Самохода

### Dev-окружения:
- dev_samohod - базовый Самохода со включенной индексацией
- dev_samohod_frozen - базовый Самохода с замороженным индексом, наливающимся из бэкапа
- dev_shmick - базовый Шмика со включенной индексацией
- dev_shmick_frozen - базовый Шмика с замороженным индексом, наливающимся из бэкапа
