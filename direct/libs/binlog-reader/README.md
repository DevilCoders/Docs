# binlog-reader - библиотека для чтения mysql бинлогов

Это обертка над direct/libs/mysql-streaming с немного другим интерфейсом.
Дополнительно позволяет:

- группировать события и строки по транзакциям
- доставать из комментариев к запросам мета-инфу Директа (request_id, method, service)

Пример использования см. в [тестах](/arc/trunk/arcadia/direct/libs/binlog-reader/src/test/java/ru/yandex/direct/binlog/reader/ReaderTest.java).
