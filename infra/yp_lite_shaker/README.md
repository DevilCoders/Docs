## YP Lite Shaker

Nanny service - https://nanny.yandex-team.ru/ui/#/services/catalog/yp-lite-shaker/


Микросервис который перевозит ноды в Няне раз в n минут. Сервис пытается обновить ноды при помощи записи всех нод в 
ReplicationPolicy.down_nodes, а также отслеживает после что ноды успешно смогли переехать.


Сервис записывает логи об успешности или фейле, а также отправляет в https://sentry.nanny.yandex-team.ru/swat/yp-lite-shaker/ все exception которые ловит

### Параметры для запуска
Обязательные параметры

    1. service_ids  - имена сервисов в Няне которые будут возиться.  
    
Вспомогательные параметры

    1. "--sleep-time" (без кавычек) Время требуемое для переезда на другую ноду, в секундах.  120 по умолчанию.
    2. "--logging-path" (без кавычек) Название файла для записи логов о перевозе сервисов. При отсутствии параметра логи будут записываться в консоль
    3. "--move-cooldown" (без кавычек) Частота перевозов по нодам, в секундах. 3600 по умолчанию.