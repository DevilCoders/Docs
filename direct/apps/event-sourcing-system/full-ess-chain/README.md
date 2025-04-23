# Приложение для запуска всей цепочи ess для конкретного правила и бизнес-логики без промежуточного logbroker'а

Приложение читает топик бинлогов, применяет правило, результат сразу отправляет обработчику бизнес-логики без записи в промежуточный топик.

### Параметры запуска

- `ess-config` - имя класса ess-конфига (например, CampAggregatedLastchangeConfig или CpmBannerModerationConfig), можно задать несклько.
- `ess-group` - название ess-группы (https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/common/src/main/java/ru/yandex/direct/ess/common/models/EssGroup.java). Будут отобраны все ess-конфиги, входящие в эту группу (https://a.yandex-team.ru/arc/trunk/arcadia/direct/apps/event-sourcing-system/common/src/main/java/ru/yandex/direct/ess/common/models/EssGroups.java помеченные аннотацией @EssGroups). Например, если задать группу `moderation`, то будут выбраны все конфиги, относящиеся к модерации.
- `t`/`working-time` - время работы приложения в секундах(по умолчанию 60)

Параметры `ess-config` и `ess-group` являются взаимоисключающими.

Обработчики бизнес-логики подбираются автоматически под заданные (или отобранные по шаблону) правила на основе соответствия EssConfig-ов у правила и logic-processor'а.

Остальные параметры совпадают с паметрами из router'а, актуальные для работы этого приложения:
- `partitions` (например, 1,2,3,4) - шарды, на которых будет работать приложение
- `read-only-new-data`/`read-new-data` - читать только те данные из логброкера, которые записались позже времени старта приложения
- `read-only-data-created-after`/`read-data-after` (ожидается московское время в формате `yyy-MM-ddTHH:mm:ss`) - читать из логброкера только те данные, которые были записаны после указанного момента времени. Использовать `read-only-new-data` не всегда удобно, а без него приложение может и не добраться за разумное время до нужных данных, т.к. в топике бинлогов может быть много.
- `ess-tag` (о нем ниже)

Параметр `logbroker-no-commit` недоступен в этом приложении, он всегда равен <i>true</i> (коммит не происходит)


### Тестирование доработок по уже работающей в стабльном процессе задачи
Для тестирования доработок на бетах можно использовать параметр <b>ess-tag</b>. С помощью него в обработку будут попадать только те события, которые помечены этим тегом.
Тегом может быть что угодно, что верноятно больше никто не будет использовать: логин, номер задачи, номер беты и тд.
1) На своей бете нужно выполнить `beta-ctl set-from-json java_properties='{"tracing.tags.ess": "my_tag"}'`. После чего перезапустить java-приложения(чтобы из запросов java проставлялся тег) и выполнить `direct-mk beta-postupdate` (чтобы из запросов перла проставлялся тег).
После этих действий ко всем sql-запросам, инициированным на бете, будет добавлен в комментарий тег.
Стабильный процесс не будет обрабатывать такие запросы.
2) Запустить второй процесс без промежуточного logbroker'а командой `direct-mk run_ess_chain -- --ess-config CampAggregatedLastchangeConfig -t 300 --read-new-data`.
Если этот процесс запускается не на той же бете, что и пункт 1, то при запуске можно указать параметр `--ess-tag my_tag` (по умолчанию берется значение из beta-settings)
Приложение будет обрабатывать только запросы с вашим тегом.
3) После тестирования выполнить `beta-ctl unset java_properties` или поправить руками файл beta-settings.json


Запуск производится с бет. Нужно собрать приложение ess_chain командой:
```
direct-mk java-init -- -a ess_chain
direct-mk java-ya-make ess_chain
```

Запуск:
`direct-mk run_ess_chain -- --ess-config CampAggregatedLastchangeConfig -t 300 --read-new-data \[--ess-tag my_tag \]`

### Выбор консьюмера для чтения
Консьюмер выбирается автоматически через блокировку в yt.
Сейчас консьюмеров 10, если приложение не запустилось с ошибкой <i>"All consumers are busy"</i>, то надо посмотреть [тут](https://yt.yandex-team.ru/freud/navigation?path=//home/direct/tmp/debug-ess-consumers), что все ноды действительно залочены, и, если это так, создать нового консьюмера:
1) добавить в [файл конфигурации](src/main/resources/app-production.conf) в debug-ess.logbroker.consumers следующий консьюмер
2) выполнить команды [отсюда](https://paste.yandex-team.ru/794222), где $n - номер нового консьюмера

### Локальный запуск
Обычным образом из IDEA запускаем `DebugEssRunner`

В `VM Options` добавляем
```
-Dtracing.tags.ess=14525-hmepas-ess-tst
-Dyandex.environment.type=development
-Dess.tvm.secret="file://~/.direct-tokens/tvm2_direct-event-sourcing-system-test"
```

В `Program arguments` прописываем соответствующие аргументы, пример:
```
--ess-tag my_tag
--ess-config CampAggregatedLastchangeConfig
-t 300
--read-new-data
```
подставив свои значения `ess-tag`, `ess-config`/`ess-group` и `t`

Если при локальном запуске использовать параметр `--ess-tag my_tag` и потом делать обновление базы с этим же tag примерно так `direct-sql dt:ppc:19 'UPDATE /* reqid:0:::ess=my_tag */  banners set body = "12.40" where bid = 9881008621 \G'`, то такие апдейты будут обрабатываться локально запущенным приложением (а апдейты без tag не будут). Общий инстанс наоборот пропустит апдейты с тэгом и это позволит комфортно проводить отладку не рискуя получить "concurrent write". Важно делать апдейт одним запросом `direct-sql...`, а не подключившись к базе, иначе не сработает.
