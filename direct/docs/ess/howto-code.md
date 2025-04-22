[Концепция](concept.md)

[Эксплуатация ESS](jeri.md)

# Как написать ESS-контур

[README.md](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/common/README.md) для связности


## Какие классы надо написать

### Конфиг
Класс-наследник [BaseEssConfig](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/common/src/main/java/ru/yandex/direct/ess/common/models/BaseEssConfig.java).

Задает топик в который пишет события `ess-router`, название процесса, лимиты и трежолды. А также этот класс связывает между собой Rule и Proccessor классы (обозначает из каког топика поставляются данные в процессор и каким набором правил этот топик логброкера наполняется).

Пример [BsExportCampaignConfig](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/config/src/main/java/ru/yandex/direct/ess/config/bsexport/campaign/BsExportCampaignConfig.java)

### Rule (набор правил)
Класс-наследник [AbstractRule](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/router/src/main/java/ru/yandex/direct/ess/router/models/rule/AbstractRule.java)
Задает объект-сообщение (`LogicObject`) который будет хранить нужную процессору информацию из бинлога и сериализованную версию которого мы запишем в топик логброкера указанный в конфиге.

Также задает правила, по которым мы из общего потока сообщений в бинлога отбираем интересные для данного контура сообщения.

Правило состоит из указания таблицы MySQL, операции над этой таблицей и маппера, преобразующего сообщение бинлога в `LogicObject`.

Пример [BsExportCampaignRule](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/config/src/main/java/ru/yandex/direct/ess/config/bsexport/campaign/BsExportCampaignConfig.java)

Для написания правил вам может пригодится схема базы данных [ppc](https://direct-dev.yandex-team.ru/db/ppc/index.html).

Также можно посмотреть какие бывают бинлоги в [logviewer](https://direct.yandex.ru/logviewer/short/2-p7Na3I3aDbDR)

Также см. [README.md](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/router/README.md)

### Processor (джоба для обработки сообщений)
Класс-наследник [BaseLogicProcessor](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/common/BaseLogicProcessor.java), реализует метод `void process(int shard, List<?> logicObjects`, на вход которого подается номер шарда в MySQL, который обрабатывается данным инстансом процессора и список LogicObjecto-ов
Чтобы логика была отчуждаемой принято не реализовывать логигу в процессоре, а вызывать из него сервис, таким образом этот же сервис можно будет вызывать из внутренних инструментов в java-web или из oneshot-а для заполнения первичных данных
Также выделение логики в отдельный сервис решает возможные проблемы с зависимостями

Пример [BsExportCampaignProcessor](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/bsexport/campaign/BsExportCampaignProcessor.java)

Также см. [README.md](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/logicprocessor/README.md)

### Опционально сервис
Чаще всего где-то в `core-модуле`
Пример [BsExportCampaignService](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/logicprocessor/src/main/java/ru/yandex/direct/logicprocessor/processors/bsexport/campaign/BsExportCampaignService.java)



## Проверить локальным запуском на бете

О запуске на бете есть хороший [README.md](https://a.yandex-team.ru/arc_vcs/direct/apps/event-sourcing-system/full-ess-chain/README.md)
(TODO: перенести сюда)





