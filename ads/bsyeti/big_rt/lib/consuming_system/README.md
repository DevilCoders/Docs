# Consuming system (+ Mediator)

ConsumingSystem = CS

Класс TConsumingSystem отвечает за то, чтобы инстанс обрабатывал
правильный набор шардов. Он порождает ряд дочерних сущностей, которые в сумме обеспечивают:
1) Балансировку шардов между инстансами
2) Автоопределение количества шардов
3) Перезапуски при всевозможных ошибках. Класс обеспечивает работу до поступления внешнего сигнала об остановке.
4) Запуск читателей (suppliers) и обработчика (shard processor) для каждого шарда, 
 который будет обрабатываться на инстансе.
5) Публикует информацию о том, что обрабатывает CS на YT.

Побробнее о внутреннем устройстве CS написано в обзоре архитектуры процессингов BigRT.

## Устройство директории на YT

Лучше работать со всей директорией как с цельным объектом и не размешать ней пользовательские объекты. (Или хотя бы называть, начиная с `_`)

```
<MainPath> (тот самый, что написан в конфиге)
├─> locks
│   ├─> shards (пустой документ, на нем берутся shared блокировки на каждый обрабатываемый шард. Не используется при мастер-балансировке)
│   ├─> workers (пустой документ, на нем берутся shared блокировки на каждого воркера, по этим блокировкам узнается полный список воркеров при балансировке)
│   ├─> public_config_updater (пустой документ, на нем берется exclusive блокировка хостом, который обновляет public_config)
│   └─> shards_count_resolver (пустой документ, на нем берется exclusive блокировка хостом, который обновляет shards_count_cache)
├─> offsets (динтаблица с оффсетами CS)
├─> public_config (публичный конфиг CS. Используется big_rt_cli для диагностик CS)
└─> shards_count_cache (кеш количества шардов, используется при AutoResolve количетсва шардов, чтобы запрашивать у LB количетсво шардов максимально редко (договоренность с LB))
```	
