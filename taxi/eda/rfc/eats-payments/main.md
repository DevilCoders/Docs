## Опросник для ревью комитетом

> Этот опросник нужен для [архитектурного ревью комитетом](https://forms.yandex-team.ru/surveys/25357/). Его можно будет скопировать.

> После его написания можно пробежаться по списку из [этой статьи](https://stackoverflow.blog/2020/04/06/a-practical-guide-to-writing-technical-specs/). Он подскажет, какие аспекты еще стоит осветить.

**Название сервиса**

eats-payments

**Какую продуктовую проблему решает сервис?**

Сервис отвечает за формирование позиций заказа и отправляет в `transactions` данные, необходимые для оплаты заказа через Trust. Сервис предоставляет интерфейс для работы с заказом (создание, изменение, завершение, отмена, получение состава заказа, рефанд).

**Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?**

Сервис создаётся в рамках выноса логики из монолита Еды в отдельный микросервис. Достаточно похожей функциональностью обладает на текущий момент payments-eda, однако есть следующие причины для создания нового сервиса:

- payments-eda написан на Python 3, а в экосистеме Еды сейчас принято писать микросервисы на C++
- payments-eda сейчас имеет достаточно большой спектр полномочий, начиная от работы с заказами в ресторанах по QR-коду и заканчивая определением доступных методов оплаты. Хочется иметь набор микросервисов в ведении команд Еды с понятной и ограниченной зоной ответственности.
- payments-eda обслуживает заказы в Супераппе, а Еде нужен свой микросервис для работы с Трастом. В идеале потом можно доработать payments-eda так, чтобы он работал с этим новым микросервисом.


**Как именно сервис будет решать поставленные перед ним задачи?**

Сервис будет предоставлять возможность для работы с заказом (создание, изменение, завершение, отмена, получение состава заказа, рефанд), подготавливая данные для создания инвойсов в transactions.

**Разрабатывается один сервис или система?**

Один сервис, однако полноценный вынос обработки платежей из монолита Еды предусматривает несколько взаимодействующих сервисов. [Документация.](https://wiki.yandex-team.ru/users/alextrust/Novaja-sxema-oplaty-v-prilozhenijax-Edy/)

**Сколько и какие сервисы входят в систему?**

[Документация.](https://wiki.yandex-team.ru/users/alextrust/Novaja-sxema-oplaty-v-prilozhenijax-Edy/)

**С кем взаимодействует сервис?**

- Монолит Еды (HTTP):
    - Процессинг (создание заказа, уведомление о состоянии платежа по заказу)
    - Чаевые курьерам/ресторанам (добавление к заказу дополнительных услуг)
- Адаптер биллинговой информации (HTTP) (см. [документацию](https://wiki.yandex-team.ru/users/alextrust/Novaja-sxema-oplaty-v-prilozhenijax-Edy/) по новым сервисам Еды, там он называется EatsBillingProxy).
- transactions (проведение заказа через Траст)  (HTTP для запросов, stq для колбеков)
- cashback (STQ)
- Колл-центр (получение оплаченных позиций, возврат денег за полученные позиции) (HTTP)

<!-- 1. Какие (микро-)сервисы и как используются.
2. Как гарантируется идемпотентность внешний операций.
3. Как поддерживается консистентность данных при частичных отказах.
4. Как организованы ретраи внешних сервисов. -->

**Какие базы использует?**

PostgreSQL.

**Какие периодические процессы?**

Периодическая очистка данных в БД для старых заказов, раз в сутки.

**Прикрепите схему того, где этот сервис находится в текущей инфраструктуре**

Сервис будет являться одной из центральных частей в цикле заказов Еды. См. схему в [документации.](https://wiki.yandex-team.ru/users/alextrust/Novaja-sxema-oplaty-v-prilozhenijax-Edy/)

**Какие данные и по какой схеме сервис будет хранить в базе?**

```sql
CREATE SCHEMA eats_payments;

CREATE TABLE IF NOT EXISTS eats_payments.orders_info
(
  order_id TEXT  NOT NULL,
  yandex_uid TEXT NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  PRIMARY KEY (order_id)
);

CREATE INDEX orders_info_yandex_uid_idx ON eats_payments.orders_info (yandex_uid);  
CREATE INDEX orders_info_created_at_idx ON eats_payments.orders_info (created_at); 


CREATE TABLE IF NOT EXISTS eats_payments.items_info
(
  item_id SERIAL,
  order_id TEXT REFERENCES eats_payments.orders_info (order_id),
  place_id TEXT NOT NULL,
  balance_client_id TEXT NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  PRIMARY KEY (item_id)
);

CREATE INDEX items_info_order_id_idx ON eats_payments.items_info (order_id);
CREATE INDEX items_info_created_at_idx ON eats_payments.orders_info (created_at); 
```

**Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?**

Объём хранимых данных: несколько десятков Гб при хранении заказов за последние три месяца.
--

<details><summary>Запрос</summary>
<p>
Для работы запроса нужно сначала создать таблицы из предыдущего пункта.
Предполагается (завышенное) количество сущностей в каждом заказе, равное 10.
За количество заказов в день взята величина 140000 заказов.

```sql
INSERT INTO eats_payments.orders_info(order_id, yandex_uid)
VALUES ('123', '123456');
INSERT INTO eats_payments.items_info(item_id, order_id, place_id, balance_client_id)
VALUES ('456', '123', 'test_place_id', 'test_balance_client_id');
SELECT pg_size_pretty(90 * 140000 * ((SELECT sum(pg_column_size(o.*)) as filesize FROM eats_payments.orders_info as o) + 10 * (SELECT sum(pg_column_size(i.*)) as filesize FROM eats_payments.items_info as i))) as data_volume;
-- data_volume
-- 11 GB
```

</p>
</details>

Изменение данных:
- добавление строк: до нескольких десятков в секунду
- массовое удаление (при очистке старых данных): несколько десятков тысяч раз в день

**Есть ли какой-то стейт в памяти, как он обновляется и валидируется?**

--

**Какая нагрузка ожидается?**

- Ожидается до 10 RPS на ручку создания заказа. Рассчитано как 140000 заказов в день/86400 = 1.6 RPS (без учёта пиков в дневные и вечерние часы). Возможен рост нагрузки с ростом количества заказов в Еде.
- На остальные ручки нагрузка до 1 RPS, т.к. они будут использоваться только саппортом при обработке проблемных заказов.

**Какие фолбеки предусмотрены на сам этот сервис?**

Бекенд Еды должен ретраить попытки создать заказ. На все остальные действия фолбеки/ретраи не предусматриваются.

Подробнее:
  - Запросы в transactions отправляются синхронно из обработчиков ручек. При любой ошибке (сетевая недоступность, ошибка обработки запроса на стороне transactions) обработчик возвращает ошибку.
  - Запросы в billing-proxy:
    - для уведомления о создании заказа отправляются из обработчика ручки через постановку stq-таски. При невозможности создать таску обработчик возвращает ошибку.
    - для уведомления о заморозке/списании средств отправляются из stq-колбека transactions (на хосте eats-payments). При ошибках таска ретраится.
  - Запросы в процессинг для уведомления о заморозке/списании денег отправляются из stq-колбека transactions (на хосте eats-payments). При ошибках таска ретраится.

**Какие фолбеки предусмотрены внутри этого сервиса на взаимодействие с другими сервисами?**

-- 

**Какие возможности масштабируемости закладываются?**

Наращивание количества инстансов сервиса при увеличении нагрузки.

**Какие точки отказа есть в сервисе?**

- БД
- Потеря сетевой связности с бекэндом Еды и transactions

**Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить**

- Количество созданных заказов в единицу времени
- Общее количество заказов в разных статусах

**Укажите технические метрики**

- vhost4xx, vhost5xx
- Количество ретраев stq-тасок
- Ошибки в логах (logserrors)

**Какая функциональность ожидается в сервисе в будущем?**

Этапы разработки:
1. MVP:
- Арх. ревью и создание сервиса (параллельно): 3д (s-rogovskiy)
- Реализация ручки получения доступных методов оплаты: 2д (rekub)
- Реализация ручки создания заказа: 3д (s-rogovskiy)
  - Создание заказа в transactions: 2д (s-rogovskiy)
  - Консолидация данных и поход в billing-proxy: 1д (s-rogovskiy)
- Реализация ручки изменения заказа: 1д (s-rogovskiy)
- Реализация ручки закрытия заказа: 0.5д (rekub)
- Реализация ручки отмены заказа: 0.5д (rekub)
- Проверки интеграции и тестирование: 1д (s-rogovskiy)
2. Остальное:
- Уведомления о заморозке/списаниии средств (2д) (s-rogovskiy)
- Реализация ручки добавления элемента в заказ (1д) (s-rogovskiy)


**Какое изменение нагрузки планируется?**

В соответствиии с ростом количества заказов в Еде.

**Активно ли будет изменяться сервис?**

После начальной разработки скорее всего нет.

## Бизнесовая задача

## Архитектура

### API

[Здесь.](api/api/)

### Клиентская логика

Должна поддерживать поход как в старые урлы (payments-eda), так и по новым урлам через бек Еды в новый сервис, что должно разграничиваться экспериментом для постепенной раскатки.


## Дополнительные важные вопросы
### Антифрод

При получении метода оплаты от клиента бек Еды будет использовать внутреннюю ручку сервиса `/v1/payment-methods-availability`, которая проксирует ручку `/4.0/payments/v1/list-payment-methods`, которая, в свою очередь, использует ручку `/v1/payment/availability` сервиса `card-antifraud`. Таким образом, дополнительно ходить в антифрод не нужно.

### Дальнейшая судьба payments-eda

`payments-eda` понемногу упраздняется, следить за процессом можно [здесь](https://st.yandex-team.ru/TAXIBACKEND-30390).


### Фолбек для Траста

Учитывая, что в последнее время у Траста достаточно часто возникают проблемы с проведением платежей, необходимо продумать механизм, с помощью которого можно разрешать (части) пользователей совершать заказы в долг с тем, чтобы списать с них деньги тогда, когда Траст станет доступным. В рамках данного RFC такой механизм не прорабатывается, но его необходимости нужно помнить.