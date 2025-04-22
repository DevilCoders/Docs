### Shedlock tms
Как подключить:
- Сделать конфиг TmsConfig, унаследовав от ShedlockTmsConfig
- поставить ему @Configuration
- описать там свой ShedlockTmsJobService

ShedlockTmsJobService нужен для
- определния таблицы для локов
- логгирования запусков
- определения активности джоб для их быстрого выключения

Есть стандартная имплементация с тремя таблицами. Пример описания:
- https://a.yandex-team.ru/arc_vcs/market/pers/qa/pers-qa-core/src/main/resources/changesets/table/core/SHEDLOCK.xml
- https://a.yandex-team.ru/arc_vcs/market/pers/qa/pers-qa-core/src/main/resources/changesets/table/qa/SCHEDULED_JOBS_LOG.xml
- https://a.yandex-team.ru/arc_vcs/market/pers/qa/pers-qa-core/src/main/resources/changesets/table/core/TASK_SWITCH_CONFIGURATION.xml

Важно: при подключении tms-модуля к обычному реалтаймовому сервису стоит использовать отдельный ограниченный датасорц, чтобы оффлай-задания не влияли на онлайн-задания.

#### Запуск джобы
При подключении конфига также подключается простой контроллер.
Запустить джобу можно вручную командой
`curl -X GET "localhost:8081/tms/run?task=sendNewTelegramAnswers"`

#### Локальный запуск
При локальном запуске удобно отключать автоматический запуск заданий. 
Сделать это можно, выключив в таблице виртуальную джобу "tms.enabled"
Настройка применяется только при запуске сервиса, не выключит задания на лету.
Будут работать только задачи, запущенные вручную.
