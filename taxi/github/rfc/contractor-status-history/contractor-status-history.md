## Опросник для ревью комитетом

> Этот опросник нужен для [архитектурного ревью комитетом](https://forms.yandex-team.ru/surveys/25357/). Его можно будет скопировать.

> После его написания можно пробежаться по списку из [этой статьи](https://stackoverflow.blog/2020/04/06/a-practical-guide-to-writing-technical-specs/). Он подскажет, какие аспекты еще стоит осветить.

**Название сервиса**

contractor-status-history

**Какую продуктовую проблему решает сервис?**

* Собрать ответственность за статусы исполнителя в одном месте
* Разобрать старые механизмы, в первую очередь, основанные на использовании dbstatus\_history.status\_history
* Отказаться от старых водительских и таксиметровых статусов в пользу статусов от сервиса `driver-status`

**Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?**

Ставится цель разобрать существующие решения и собрать обработку статистики/истории по статусам в одном месте

**Как именно сервис будет решать поставленные перед ним задачи?**

Сервис будет сохранять события изменения статуса потребителя. Будет вычисляться агрегация, сколько в каком статусе провёл в заданный временной интервал.
Потребители смогут получать как ленту событий, так и агрегированные данные

**Разрабатывается один сервис или система?**

Один сервис

**Сервис внутренний или внешний?**

Внутренний

**С кем взаимодействует сервис?**

События смены статуса исполнителя и статуса заказа будут поступать через logbroker из сервиса `driver-status`
Планируемые потребители:
* MPH
* driver-weariness
* driver-supply-hours
* contractor-random-bonus
* Админка/Оптеум

**Какие базы использует?**

Новая БД `contractor-status-history` в PGaaS. Нужна для персистентного хранения событий смены статуса.

**Какие периодические процессы?**

* Удаление "старых" событий - старше, разрешённого значения (2-3 суток)
* Вычисление агрегированных данных

**Какие данные и по какой схеме сервис будет хранить в базе?**

Примерная схема:
```
CREATE SCHEMA history;

CREATE TYPE history.status AS ENUM('offline', 'online', 'busy');
CREATE TYPE history.order_status AS ENUM('none', 'driving', 'waiting', 'transporting', 'complete', 'failed', 'cancelled', 'expired', 'preexpired', 'unknown');

CREATE TABLE history.contractors (
  id BIGSERIAL PRIMARY KEY,
  park_id VARCHAR(48) NOT NULL,
  profile_id VARCHAR(48) NOT NULL,
  CONSTRAINT unique_contractor UNIQUE (park_id, profile_id)
);

CREATE TABLE history.events (
  event_ts TIMESTAMP WITH TIME ZONE NOT NULL,
  contractor_id BIGINT REFERENCES history.contractors(id),
  status history.status NOT NULL,
  order_statuses history.order_status[],
  CONSTRAINT events_ts_id_pk PRIMARY KEY (event_ts, contractor_id)
);
```

Таблица `history.contractors` статическая, в неё производится толко вставка и чтение. Размер таблицы около 4 млн записей, с медленным ростом (15 тыс записей в сутки). Оценка размера на диске ~1GB.
Таблиц типа `history.events` планируется создать несколько, по одной на сутки. По прошествии 2-3 дней очищать самую старую таблицу целиком. Одна таблица с данными за полные сутки будет содержать до 100 млн записей. Оценка размера на диске ~5GB на одну таблицу.

**Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?**

Будет храниться 15-20GB. За сутки будет "набегать" ~5GB, и раз в сутки дропаться эквивалентный объём.

**Какие операции над данными заложены?**

INSERT, SELECT, постараемся обойтись без UPDATE. DROP TABLE для устаревших таблиц.

**Есть ли какой-то стейт в памяти, как он обновляется и валидируется?**

-

**Какая нагрузка ожидается?**

Рейт вычитывания событий из logbroker - до 1500 событий в секунду.
Нагрузка на чтение из ручек - порядка 100 RPS.

**Какие фолбеки предусмотрены на сам этот сервис?**

-

**Какие фолбеки предусмотрены внутри этого сервиса на взаимодействие с другими сервисами?**

При недоступности PG сервис будет отвечать ошибкой

**Какие возможности масштабируемости закладываются?**

Увеличение числа инстансов сервиса, flavor PGaaS

**Какие точки отказа есть в сервисе?**

* PGaaS
* Отказ сервиса `driver-status`

**Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить**

* RPS, тайминги и ошибки ручек

**Укажите технические метрики**

* RPS, тайминги и ошибки ручек
* Потребление ресурсов PGaaS
* Рейт поставки событий по logbroker

**Какая функциональность ожидается в сервисе в будущем?**

1. MVP. Реализация сохранения данных в PG, реализация методов ленты событий и агрегированных интервалов.
2. Думаем над долгосрочным хранением истории - MDS, YT, etc
3. Думаем над учётом блокировок в истории статусов исполнителя

**Какое изменение нагрузки планируется?**

Пропорционально числу и активности исполнителей

**Активно ли будет изменяться сервис?**

Ближайшие месяцы сервис будет активно разрабатываться

**Комментарий**

Ссылка на RFC: https://github.yandex-team.ru/taxi/rfc/pull/614

<hr>

## Архитектура

### API

#### Лента событий смены статуса исполнителя

`POST /v1/events`:
Ожидаемая нагрузка на первом этапе ~10RPS
Первоначально храним данные за 2 суток

Request (json)
```json
{
  "from": 1603670400,  // секунды
  "to": 1603670600,
  "period": 86400 // секунды; указывается либо period (т.е. интервал [now - period, now]), либо from-to
  "contractors": [
    {
      "park_id": "park_1",
      "profile_id": "profile_1",
    },
    ...
  ]
}
```

Response (flatbuffer, ответ представлен в виде JSON для иллюстрации)
```json
{
  "contractors": [
    {
      "park_id": "park_1",
      "profile_id": "profile_1",
      "events": [
        {
          "status": "online",
          "on_order": true, // опционально, если опущено - false,
          "ts": 1603670401  // секунды
        },
        ...
      ]
    },
    ...
  ]
}
```

#### Агрегированные данные

`POST /v1/intervals`
Ожидаемая нагрузка на первом этапе ~100RPS
Первоначально храним данные за 2 суток

Request (json)
```json
{
  "from": 1603670400,  // секунды
  "to": 1603670600,
  "period": 86400, // секунды; указывается либо period, либо from-to
  "contractors": [
    {
      "park_id": "park_1",
      "profile_id": "profile_1",
    },
    ...
  ]
}
```

Response (flatbuffer, ответ представлен в виде JSON для иллюстрации)
```json
{
  "contractors": [
    {
      "park_id": "park_1",
      "profile_id": "profile_1",
      "intervals": [
        {
          "from": 1603670400, // секунды
          "to": 1603670600,
          "online": 123, // секунды; online, без заказов
          "busy": 123, // busy, без заказов
          "on_order": 123 // любой статус на заказе
        },
        ...
      ]
    },
    ...
  ]
}
```

