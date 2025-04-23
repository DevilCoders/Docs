# event-sourcing-system-logic-processor

Все logic-processor'ы - классы, наследуемые от [BaseLogicProcessor](src/main/java/ru/yandex/direct/logicprocessor/common/BaseLogicProcessor.java).
LogicProcessor параметризуется пользовательским объектом, и должен быть помечен аннотацией [EssLogicProcessor](src/main/java/ru/yandex/direct/logicprocessor/common/EssLogicProcessor.java)

Каждый logic-processor - [шардированный job](../../../libs/scheduler/src/main/java/ru/yandex/direct/scheduler/support/DirectShardedJob.java) и [демон](../../../libs/scheduler/src/main/java/ru/yandex/direct/scheduler/Daemon.java)
Должен реализовывать метод <i>process</i>, принимающий на вход список пользовательских объектов и выполняющих основную бизнес-логику. Все пользовательские объеты будут переданы logic-processor'у с тем же шардом, который был указан в бинлоге.

logic-processor'ы читают объекты из LogBroker'а из топика, указанного в конфигурационном классе, и из группы, равной номеру шарда job'а.
Чтение происходит до тех пор, пока количество считанных объектов и время чтения меньше параметров из конфигурационного класса: RowsThreshold и TimeToReadThreshold соответственно.
После этого данные передаются в для обработки бизнес-логике.

После каждой итерации считается время отставания от бинлога. Если оно превысило критическое время из конфигурационного класса - в juggler отправляется статус CRIT.
Кроме того, в solomon также отправляется отставание. Плюс считается количество считанных байт и объектов.

Если во время обработки объектов случилась ошибка - они будут прочитаны и переданы processor'у еще раз.
Может получиться так, что данные будут переданы processor'у несколько раз(например, если во время коммита в логброкер случилась ошибка и тп.)

На данный момент коммит в логброкер происходит после каждой итерации.
