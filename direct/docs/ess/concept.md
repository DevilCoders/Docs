[Разработка ESS контура](howto-code.md)

[Эксплуатация ESS](jeri.md)


# Event Sourcing System - ESS

Система на базе обработки бинлогов, которая позволяет изменение в БД MySQL воспринимать как триггер и производить по этому тригеру (событию) какие-то вычисления. Например что-то где-то агрегировать, совершать какие-то выгрузки во внешние системы и т.д.


## Основное компоненты
* MySQL - первичная (источник истины) БД в которой хранится и изменяется информация;
* binlogbroker - приложение которое читает бинлоги MySQL и в специальном формате записывает их в топик logbroker-а;)
* [Logbroker](https://logbroker.yandex-team.ru/docs/) - внутрияндексовый сервис для передачи упорядоченных потоков данных (там есть топики, в них можно писать);
* ess-router - приложение Директа, вычитывающее топик логброкера, и распределяющая записи по отдельным ess-топикам в logbroker-е, согласно описанным правилам;
* direct.jobs - специальные job-ы, вычитывающие каждая свой топик логброкера, и производящая какие-то действия согласно прочитанным событиям (сообщениям из топика).

Схема того, как это выглядит на примере транспорта в модерацию: [картинка со схемой](https://jing.yandex-team.ru/files/aleran/Untitled%20Diagram%283%29.jpg)

