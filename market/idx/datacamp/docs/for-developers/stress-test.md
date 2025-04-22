# Нагрузочное тестирование
Для фактической проверки максимальной допустимой нагрузки на хранилище предлагается проводить нагрузочное тестирование: генерировать и обрабатывать искусственные офферы.

# Генерация
Генерируются офферы при помощи утилиты [ddos_tool](https://a.yandex-team.ru/arcadia/market/idx/datacamp/dev/ddos_tool). Подробнее на [соответствующей странице](https://docs.yandex-team.ru/market-datacamp/components/degradation).

# Сервис координации
Для управления процессом обработки синтетических офферов используется [сервис координации](https://ydb.yandex-team.ru/docs/concepts/coordination). Кратко: отслеживаются изменения конфига, приложенного к конкретной ydb-ноде. После изменения конфига в течение незначительного тайминга (по дефолту секунда) вызываются функторы, определённые в функции [подписки](https://ydb.yandex-team.ru/docs/concepts/coordination).

# Изменение конфига
Для изменения конфигурационного файла используется ручка в [Datacamp Routines](https://docs.yandex-team.ru/market-datacamp/components/routines/admin#put-/set_drop_filter).
Также есть консольная тулза [drop_filter_tool](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/drop_filter_tool) с дублирующим функционалом

# Примерный сценарий работы
По умолчанию синтетические офферы фильтруются и не обрабатываются. Для исправления этого недоразумения при желании провести нагрузочное тестирование дёргается ручка `set_drop_filter`. 
Командой `curl -X PUT "https://datacamp-admin.white.tst.vs.market.yandex.net/set_drop_filter" -d "{\"dropSynthetic\":false,\"filterInside\":false}"` выключается фильтрация синтетических офферов в [пайпере](https://a.yandex-team.ru/arcadia/market/idx/datacamp/lib/processors/filter_synthetic/filter_synthetic.cpp?rev=r9573104#L69), [майнере](https://a.yandex-team.ru/arcadia/market/idx/datacamp/miner/processors/proto_unpacker/proto_unpacker.cpp?rev=r9573104#L62) и [парсере](https://a.yandex-team.ru/arcadia/market/idx/feeds/qparser/bin/qparser/lib/qparser.cpp?rev=r9573104#L1026).

После этого используется `ddos_tool` для нагрузки: 
```./ddos_tool --tvm-client-id 2002296 --tvm-token `ya vault get version sec-01dsfcej668h548vxvxgh8vw41 -o tvm` ```

Графики по нагрузке на таблицу можно смотреть например в [Соломоне](https://solomon.yandex-team.ru/?project=yt&cluster=seneca-sas&service=node_tablet&sensor=yt.tablet_node.write.data_weight.rate&l.host=Aggr&l.tablet_cell_bundle=market-datacamp-testing&l.table_path=-&l.table_tag=-&l.user=*&graph=auto&filter=top&filterBy=max&filterLimit=10&hideNoData=true&b=1h&e=), метрики пайпера - в [разделе](https://docs.yandex-team.ru/market-datacamp/market/idx/datacamp/parser/README#deploy).
По окончании тестирования достаточно вернуть фильтр в исходное состояние: `curl -X PUT "https://datacamp-admin.white.tst.vs.market.yandex.net/set_drop_filter" -d "{\"dropSynthetic\":true,\"filterInside\":true}"`

# Очистка
Для того чтобы очистить стейт хранилища от синтетических офферов, имеется тулза [drop_synthetic](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/drop_synthetic).
```./drop_synthetic --yt-proxy hahn```
Окружение задаётся параметром `--environment` по умолчанию соответствующего тестингу.
Настройки ытя (токен, пул, прокси) передаются стандартным для индексатора способом через протобафгые опции программы.

# Парсер
ID нагрузочного магазина в тестинге - 11012013.
