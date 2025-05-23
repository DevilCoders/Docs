# Реферальная программа

## Новые конфиги

Для реализации новой логики реферальной программы нужно поменять её конфиг.
Для того, чтобы сумма скидки зависела от региона использования, а не создания промокода, нужно разделить конфиг рефералки с точки зрения создателя и с точки зрения пользователя.

### referral –– конфиг создателя рефералки

Конфиг должен содержать следующие поля:

- `country` –– страна пользователя, который создаёт реферальный промокод;
- `zone_name` –– имя зоны пользователя, который создаёт реферальный промокод;
- `id` –– id данного конфига, чтобы ссылаться на него из объекта созданного промокода;
- `success_activations_limit` –– общий лимит на количество успешных добавлений промокода;
- `rewards` –– массив правил начисление бонуса, каждый элемент содержит:
  - `max_completion_number` –– конечный порядковый номер завершения (включительно) –– диапазон действует от предыдущего конечного порядкового номера (не включая); если это минимальный номер в конфиге, до действует от нулевого;
  - `series_id` –– серия промокода для начисления награды (опционально); если не задано, значит при попадании в данный range награда не начисляется.

При создании реф. промокода ищем подходящий сначала по зоне, а затем по стране создателя (пока по последней поездке).

При использовании промокода для определения ограничений ищем нужный конфиг по cfg_id реферального промокода.

Начислении награды ищем по cfg_id промокода нужный конфиг и по порядковому номеру активации для данного промокода находим нужную награду.

Ограничение по количеству активаций нужно для аудита: мы должны всегда знать, сколько денег сможем пообещать.

### referral_give –– конфиг пользователя рефералки

Конфиг должен содержать следующие поля:

- `country` –– страна пользователя, который едет по реф. промокоду;
- `zone_name` –– имя зоны пользователя, который едет по реф. промокоду;
- `duration_days` –– срок действия промокода после первой активации пользователем;
- `series_id` –– серия в базе промокодов, которая содержит ограничения на сумму, регион и прочие детали.

При проверке промокода для использования в заказе и при попытке коммита заказа (coupon_reserve) ищем сумму и/или процент в конфиге сначала по зоне, а потом по стране поездки.

Ограничение на количество дней использования нужно чтобы не давать бесконечных обещаний на скидку.

## Необходимые таблицы в БД

### referral –– таблица с реферальными промокодами

- `id`
- `cfg_id`
- `code`
- `yandex_uid` –– создателя
- `created`

Уникальные индексы по `code` и `yandex_uid`

### referral_activations –– таблица с активациями реферального промокода (записывается любое добавление реф. промокода в список, или попытка проверить/использовать в поездке)

- `id`
- `referral_id`
- `yandex_uid` –– пользователя
- `created`
- `start`
- `finish`
- `series_id` –– копия значения из конфига: нужно зафиксировать, чтобы можно было однозначно сказать, какие скидки мы уже пообещали и проще посчитать экономику фичи

Уникальный индекс по (`referral_id`, `yandex_uid`).

Добавление активации происходит с помощью следующего запроса:

```sql
INSERT INTO referral_activations
  (referral_id, yandex_uid, start, finish, series_id)
SELECT $1,$2,$3,$4,$5
WHERE
  NOT EXISTS (
    SELECT id FROM referral_activations
    WHERE
      promocode_id = $1 AND yandex_uid = $2
  );
```
Если активация для данного промокода и пользователя уже существует –– попытки INSERT не будет, поэтому не будет лишнего инкремента SEQUENCE для SERIAL поля `id`.
Однако гонка все равно возможна, если параллельно пытаться добавить **новую** активацию.


### referral_success_activations –– таблица с успешными активациями

- `id`
- `yandex_uid`
- `activation_id` –– id записи из таблицы `referral_activations`

Уникальный индекс по `yandex_uid` и по `activation_id`.

В старой схеме то, что в данном документе названо активацией, разделено на две сущности: виртуальная серия промокода (refclaims) и активация в документе `promocode_referrals`. Сейчас создаётся запись в `referral_activations` при первой попытке использовать реферальный промокод для фиксации ограничений. А при успешной проверке создаётся запись в `referral_success_activations`.

Запись успешной активации происходит с помощью следующих запросов в транзакции:
```sql
SELECT code FROM referral WHERE code = $3 FOR UPDATE;

INSERT INTO referral_success_activations
  (yandex_uid, activation_id)
SELECT $1,$2
WHERE
  NOT EXISTS (
    SELECT id FROM referral_success_activations
    WHERE
      yandex_uid = $1
  ) AND NOT EXISTS (
    SELECT id FROM referral_success_activations
    WHERE
      activation_id = $2
  ) AND (
    SELECT COUNT(*)
    FROM referral_success_activations rsa
    JOIN referral_activations ra ON ra.id = rsa.activation_id
    JOIN referral r ON r.id = ra.referral_id
    WHERE
      r.code = $3
  ) < $4;
```

Первым шагом берется лок на промокод, для которого записывается активация. Это нужно для избежания гонок на следующем шаге.
Затем происходит вставка записи об успешной активации, если:
- нет успешной активации для данного пользователя
- нет успешной активации для драфта активации (`referral_activation`)
- количество успешных активаций для данного промокода не превосходит заданный конфигом лимит


### referral_completions –– таблица с завершенными поездками по рефералке, нужна для начислений наград

- `id`
- `referral_id`
- `yandex_uid` –– пользователя
- `order_id`
- `reward_token`
- `created`
- `updated`

Уникальные индексы по `reward_token`, `order_id`
Неуникальный индекс по `referral_id`

Обновлять обязательно в транзакции и с select for update.

## Основные сценарии работы с рефералкой

В этом документы прописаны особенности реферальных купонов, и это не отменяет общее флоу использования купонов (запись usages, проверка на фрод и всё прочее).

### get referral

1. ищем конфиг по зоне, затем по стране; если не находим –– рефералка недоступна в этом регионе;
1. пытаемся вставить в таблицу referral новую запись; если вставили –– возвращаем, если нет –– селектим и возвращаем;

### activate referral

1. селектим referral по коду
1. ищем нужный конфиг по referral.cfg_id
1. пытаемся вставить в таблицу referral_activations новую запись, если вставилась –– возвращаем, если нет –– селектим и возвращаем то, что заселектилось
1. дальше идут обычные проверки для купонов на количество первых поездок, количество использований, срок действия и прочее

### check referral

Делаем то же самое, что и при активации, только дополнительно ищем нужную скидку в конфиге `referral_give` по зоне и стране поездки

### reserve referral

аналогично check referral

### complete referral

Подробно схема описана в доке на referral_reward

1. селектим referral по коду
1. вставляем в referral_completions
1. селектим из referral_completions все записи по referral_id, с сортировкой по id
1. получаем из конфига серию промокода для вознаграждения
    1. вычисляем порядковый номер добавленной активации
    1. ищем нужный конфиг по `referral.cfg_id`
    1. находим нужную серию по диапазону в разделе `rewards` конфига
1. запускаем выдачу награды с нужной серией
