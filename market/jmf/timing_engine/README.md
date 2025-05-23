# Временные метрики

Модуль добавляет справочник времени обслуживания. Примером элементов справочника является "Рабочая неделя с 8 до 17 с перерывом на обед с 12 до 13".
Каждый элемент содержит описание рабочего времени по дням недели (понедельник с 8 до 16) и дни исключения (8 марта нерабочий день).

Добавляются два типа атрибутов:
1) [Счетчик времени](src/main/java/ru/yandex/market/jmf/timings/attributes/timer/TimerType.java)
2) [Обратный счетчик](src/main/java/ru/yandex/market/jmf/timings/attributes/backtimer/BackTimerType.java)

Счетчики имет статусы:
1) NOT_STARTED - счетчик создан, но еще не запущен.
2) ACTIVE - счетчик считает время.
3) PAUSED - преостановлен.
4) STOPPED - отсчет времени остановлен. В отличает от PAUSED счетчик больше не может перейти в состояние ACTIVE.
5) EXCEEDED - просрочен (только для обратного счетчика).

Счетчики считают время либо по астрономическому времени, либо по настроенному времени обслуживания (отсчет ведется только в рабочее время).

Счетчик времени используется, например, для подсчета времени потраченного на решение задачи. Обратный счетчик считает остаток времени, например,
если на решение задачи отводится 1 час, то счетчик показывает сколько времени осталось от отведенного часа.

Счетчики времени могут изменять свой статус либо при изменении статуса объекта (если объект поддерживает жизненный цикл), либо по скрипту. Во 
втором случае в конфигурации указывается четыре скрипта: скрипт условия запуска счетчика, приостановки, активации и остановки.

Пересчет счетчиков осуществляется при модификации объектов, а рассчет актуальных значений в момент получения значения атрибута.