### Введение

##### Сервисы

- `Maps UGC Account` - сервис, который предоставляет единую точку доступа к контенту, генерируемому силами пользователей Карт
- `MRC ride UGC Account` - сервис, который обслуживает предметную область последовательностей снимков ride_photo

##### Зона ответственности `MRC ride UGC Account`

- предоставляет программный интерфейс для управления вкладом:
  - показывает детальную информацию о ride и ride_photo
  - удаляет ride
  - удаляет края ride
  - сокрытие авторства
- сообщает сервису `Maps UGC Account` о событиях, которые происходят с ride

##### Взаимоотношения с GDPR

| Состояние                             | Поездки/Фото видны в ЛК | Фото видны в продукте | Авторство видно в продукте            | Фотки и авторство храним в базе |
|---------------------------------------|-------------------------|-----------------------|---------------------------------------|---------------------------------|
| По-умолчанию                          | Да                      | Да                    | = настройке пользователя по-умолчанию | Да                              |
| Пользователь удалил поездку           | Нет                     | Нет                   | Нет                                   | Да                              |
| Пользователь удалил авторство поездки | Да                      | Да                    | Нет                                   | Да                              |
| Пользователь удалил данные через GDRP | Нет                     | Да                    | Нет                                   | Да                              |

### База данных

##### Таблица ride.ride (создана специально для личного кабинета)

| Column                   | Type                      | Nullable |
|--------------------------|---------------------------|----------|
| ride_id                  | bigint                    | not null |
| user_id                  | text                      | not null |
| start_time               | timestamp with time zone  | not null |
| end_time                 | timestamp with time zone  | not null |
| source_id                | text                      | not null |
| track                    | geometry(LineString,3395) | not null |
| distance_in_meters       | double precision          | not null |
| photos                   | bigint                    | not null |
| upload_start_time        | timestamp with time zone  | not null |
| upload_end_time          | timestamp with time zone  | not null |
| is_deleted               | boolean                   | not null |
| show_authorship (new)    | boolean                   |          |
| status (new)             | enum                      |          |

is_deleted:
- FALSE -- поездка видна в ЛК
- TRUE -- поездка удалена пользователем или при объединении - не видна в ЛК


show_authorship:
- NULL -- значение по-умолчанию, пользователь явно ничего не сказал - подписываем
- FALSE -- пользователь запретил подписывать
- TRUE -- пользователь разрешил подписывать

##### Таблица ride.deleted_interval (new)

Cкрытые пользователем участки проездов.
Добавляются при удалении краев или проезда целиком.

| Column                   | Type                      | Nullable |
|--------------------------|---------------------------|----------|
| deleted_interval_id      | bigint                    | not null |
| user_id                  | text                      | not null |
| start_time               | timestamp with time zone  | not null |
| end_time                 | timestamp with time zone  | not null |
| source_id                | text                      | not null |

##### Таблица signals.feature

| Column                               | Type                      | Nullable |
|--------------------------------------|---------------------------|----------|
| ...                                  |                           |          |
| moderators_should_be_published (new) | boolean                   |          |

moderators_should_be_published:
- NULL -- значение по-умолчанию, у модератора нет мнения
- FALSE -- модератор считает, что фотография не должна публиковаться
- TRUE -- модератор считает, что фотографию можно опубликовать

##### Таблица signals.ride_photo

| Column                | Type                      | Nullable |
|-----------------------|---------------------------|----------|
| ...                   |                           |          |
| show_authorship (new) | boolean                   |          |
| deleted_by_user (new) | boolean                   |          |

deleted_by_user:
- NULL -- старый снимок (сделан до ЛК) и/или пользователь явно ничего не сказал - можно публиковать
- FALSE -- пользователь считает, что фотографию можно опубликовать
- TRUE -- пользователь запретил публиковать

##### Таблица service.ugc_account (new)

| Column                   | Type                      | Nullable |
|--------------------------|---------------------------|----------|
| user_id                  | text                      | not null |
| show_authorship          | boolean                   |          |

### Правка данных ЛК

##### Общие решения

- grinder-задача **async_ugc_rides_modify(deletedIntervalIds, rideIds)**
  - устанавливает deleted_by_user = true всем снимкам попавшим в удаленный интервал
  - переносит из db::ride в db::ride_photos show_authorship
  - вычисляет статус, трек, кол-во фотографий и записывает в db::ride
  - удаляет вклады (если нет в БД) или
  - изменяет/добавляет вклады в [`Maps UGC Account`:`PUT /v1/contributions/modify`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/ugc_account/Backoffice.md#v1contributionsmodify)

- Конфликты правки объекта db::ride, db::feature решаются с помощью:
  - retry
  - [поля xmin для оптимистической блокировки](https://wiki.yandex-team.ru/maps/dev/core/sqlchemistry/#optimisticheskieblokirovki)

##### Процессы правки данных ЛК

- Редактирование пользователя ЛК: cокрытие авторства, удаление краев проезда
  Endpoint: `MRC ride UGC Account`:`PUT /v1/rides/my/update`
  Реакция:
    - Синхронное добавление объектов db::deleted_interval
    - Синхронное изменение объекта db::ride(show_authorship, start_time, end_time)
    - Запуск grinder-задачи async_ugc_rides_modify для затронутых db::deleted_interval и db::ride

- Редактирование пользователя ЛК: удаление проезда
  Endpoint: `MRC ride UGC Account`:`DELETE /v1/rides/my/delete`
  Реакция:
    - Синхронное добавление объекта db::deleted_interval
    - Синхронное изменение объекта db::ride(is_deleted = true)
    - Запуск grinder-задачи async_ugc_rides_modify для затронутых db::deleted_interval и db::ride

- Редактирование пользователя ЛК: удаление пешеходной неточности
  Endpoint: `MRC ride UGC Account`:`DELETE /v1/walk_objects/my/delete
  Реакция:
    - Сокрытие фотографий неточности (deleted_by_user=true)
    - Попытка удаления задачи в social feedback
    - Удаление contribution в UGC Account

- Обработка снимков пользователя
  Endpoint: ride_inspector
  Реакция:
    - Создание, объединение, изменение объектов db::ride
      При объединение нового и старого(ых) участков заезда:
        - снимки попавшие в db::deleted_interval исключаются из рассмотрения
        - начало съемки, начало выгрузки выбирается минимальным
        - конец съемки, конец выгрузки выбирается максимальным
        - флаг подписывания имени show_authorship ставится FALSE если есть хоть один такой заезд
        - заездам которые были "поглощены" при объединении ставим is_deleted = true
    - Запуск grinder-задачи async_ugc_rides_modify для затронутых db::deleted_interval и db::ride

- Отказ пользователя от снимков
  Endpoint: tasks-planner:`POST /1/takeout/delete/`
  Реакция:
    - Запуск grinder-задачи async_takeout_data_erasure внутри которой:
      - Запуск grinder-задачи async_ugc_rides_modify для затронутых db::ride

- Редактирование картографом отдельного снимка: сокрытие/публикация, rotate
  Endpoint: tasks-planner:`PATCH /photos/$`
  Реакция:
    - модификация снимка

- Редактирование картографом пачки снимков: сокрытие/публикация, изменение направления съемки, выставление уровня приватности
  Endpoint: tasks-planner:`PATCH /photos_batch_edit`
  Реакция:
    - модификация пачки снимков

- Редактирование картографом пачки снимков: позиционирование (неявное сокрытие в случае неудачи)
  Endpoint: tasks-planner:`POST /photos_adjust_positions`
  Реакция:
    - модификация пачки снимков
    - Запуск grinder-задачи async_ugc_rides_modify для затронутых db::ride

- Экспорт фотографий
  Endpoint: export_generator
  Реакция:
    - модификация is_published/should_be_published учитывает поля moderators_should_be_published и deleted_by_user (для ride_photo)
