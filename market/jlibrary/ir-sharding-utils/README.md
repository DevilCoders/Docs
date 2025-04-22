# Sharding utils

Либа для шардирования инстансов сервиса, как это было сделано в скутчере [Вики](https://wiki.yandex-team.ru/market/development/datapreparation/Как-работает-шардирование-в-Скутчере-и-Матчере/)

Была скопирована из подлибы матчера


### Функционал

* Self discovery - позволяет узнать свой хост, дц, cluster_id и replica_id

В девелопмент профиле подставляется мок, иначе вычисляется из sys env машинки

* Shard discovery - обнаружение инстансов шардов определенного сервиса

Нужно указать название сервиса в пропсе `sharding.service-discovery.nanny-service-name`, например market_smartmatcher_shard

* Hosts holder - сторедж шард хостов, который регулярно рефрешит использовая дискавери сервис с периодом `sharding.hosts-refresh-rate-ms` (по дефолту 60сек). Инициализируется лениво
