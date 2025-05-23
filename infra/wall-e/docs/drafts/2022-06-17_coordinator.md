
# Координатор нескольких инсталляций walle

## Текущая ситуация

Имеем основную RTC инсталляцию, тестовую инсталляцию RTC с десятком машин и YC инсталляцию с одной машиной, но на которую в будущем переедут все облачные машины. Хочется не допустить ситуации когда одна машина лечится сразу несколькими инсталляциями или когда машина не обрабатывается никакой инсталляцией вообще.

## Предлагаемое решение

Поднять отдельный микросервис со своей базой, который бы знал о том, какие хосты существуют во всех инсталляциях и разрешал или запрещал бы операции по их добавлению и удалению из инсталляций.

### Схема базы данных:

```
  * key: int
  * host_type: enum
  * installation_id: enum
  * uuid: str
  * inv: int
  * name: str
  * exclude_from_monitoring: bool
```

mongo? postgres? пока склоняюсь к mongo

### Дополнительные действия со стороны инсталляции валли

Кажой инсталляции предстоит научится ходить в координатор на этапах работ стейджей в FSM и некоторых кронячек. Некоторые действия над хостами можно будет делать только с одобрения координатора:
  + добавление хоста - проверяем, что хост не обрабатывается другой инсталляцией (не касается shadow типа)
  + удаление хоста - только уведомление
  + смена имени - проверяем, что такого хоста нет на другой инсталляции
  + смена инвентарника - проверяем, что такого инвентарника нет на другой инсталляции

### Работа координатора

  + джобы, поллящие все хосты всех инсталляций, обновляют данные в табличке
  + принимаем запросы от инсталляций, вносим изменения в базу
  + джоба мониторящая ситуацию когда 1 хост (с одним инвентарником/именем) обрабатывается более чем одной инсталляцией

### Прочие моменты:
  + у будущей инсталляции IL не будет возможности устанавливать исходящие соединения, поэтому на ней надо будет отключить хождение в координатор и оставить только мониторинг по фактическому составу хостов
  + возможно, у IL будет отдельный BOT с отдельным пулом инвентарников. В этом случае координатору надо будет это учитывать. Кажется, что будет достаточно маппинга installation_id <-> bot_id, зашитого в коде.
  + отдельный сетевой макрос для явных доступов из разных инсталляций
  + тестовый стенд, на котором крутятся джобы, но в который не ходят инсталляции.

## Ссылки
  + [обсужение на доске](https://jing.yandex-team.ru/files/rocco66/IMG_2105.HEIC)
