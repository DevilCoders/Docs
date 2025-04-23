## Задача

[SCOOTERDEV-139](https://st.yandex-team.ru/SCOOTERDEV-139)

Нужно поддержать флоу воскрешения самокатов поверх флоу перезарядки.

> Оффтоп.
> У нас будут и другие флоу. Так что хочется тут подумать над немного более генерализованным механизмом. Но не очень силльно так как усложнение и обобщение потребует своего диспатча и переделки scooters-misc.

Флоу воскрешения отличается лишь тем (от [флоу перезарядки](https://github.yandex-team.ru/taxi/rfc/blob/master/scooters/01_cargo_integration.md)), что у курьеров с собой должен быть специальный прибор. Таких приборов ограниченное количество и нужно в каждый момент времени понимать, у кого какой прибор находится.

## Решение

### В общих чертах

Сейчас recharge_task судя даже по названию предназначается только для задач перезарядки. Добавляем к нему поле `type` и расширяем его применимость. Других новых полей пока вводить не будем. Если понадобятся, то их лучше в каком-то json поле сделать.

Переписываем батчинг - на каждой итерации батчинга забираем ВСЕ самокаты из scooter-backend и уже внутри scooter-misc рассовываем их по различным workflow: перезарядка, воскрешение.

Заводим новую таблицу `tackles` с инфой о воскресителях. Также делаем набор ручек для бота начальника лавки.

В workflow для воскрешения берем самокаты, на которых стоит тег `dead`. Смотрим по таблице `tackles` где есть свободные воскресители и туда пытаемся сматчить самокаты.

При создании заявки в карго проставляем коммент: **возьми зарядник**.


### Новый батчинг

Тут хочется сделать небольшой рефакторинг. В идеале переименовать сущности: `recharge_task` -> `service_task`, `recharge_item` -> `vehicle`. Кажется, это сложно и дорого.

Что точно тут хочется сделать, так это отказаться от процесса `items_fetcher`. Он теперь не нужен.

Для батчинга заведем новый конфиг чтобы там настраивать разные workflow. Что-то такое:

```yaml
workflows:
    recharge:
        enabled: true
        interval-seconds: 600
        filter:
            required_tags:
                - battery_low
            prohibited_tags:
                - lost
                - broken
                - relocation_in_progress
                - disabled_for_all
                - dead
    dead:
        enabled: true
        interval-seconds: 3600
        filter:
            required_tags:
                - dead
            prohibited_tags: []
```

Удалим конфиги:

- SCOOTERS_MISC_PRE_BATCHING_CHECKS
- SCOOTERS_MISC_CAR_DETAILS_PAGE_SIZE
- SCOOTERS_MISC_PRE_BATCHING_CHECKS
- SCOOTERS_MISC_RECHARGE_ITEMS_FETCHER_CAR_DETAILS_REQUEST
- SCOOTERS_MISC_RECHARGE_ITEMS_FETCHER_SETTINGS
- SCOOTERS_MISC_RECHARGE_ITEMS_FETCHER_TAGS
- SCOOTERS_MISC_RECHARGE_TASKS_CREATOR_SETTINGS


Сейчас есть проблема, что нельзя быстро менять интервал батчинга. Если, например, прошлое значение было - 1час, а мы сейчас быстро хотим поставить 10 минут, то нужно будет ждать час перед тем как новое значение применится.

Хочется тут запускать итерацию батчинга каждую секунду (или 10/30) и смотреть на время последнего запуска того или иного workflow. Для этого стоит завести таблицу `workflows`:

```
create table scooters_misc.workflows (
    id text not null primary key,
    last_run datetimetz
);
```

Если хотя бы один workflow может быть запущен в текущей итерации будем запрашивать все машины из scooter-backend и через фильтры запускать различные workflow. Стоит тут сделать ограничение чтобы одна машина могла сматчится только в один workflow.

Для recharge алгоритм остается тем же. Просто копируем его. Единственное, стоит исправить баг - нужно батчить одновременно с построением пути обхода. Сейчас там очень неоптимально.

Для dead алгоритм следующий:
1) Берем все машины по фильтру
2) Берем все лавки, где есть свободные воскресители
3) Отфильтровавываем лавки из конфига чтобы остались только с воскресителями
4) Матчим мертвые самокаты на лавки и сразу делаем батчи в соответствие с экспериментом recharge_items_batch_settings. Важно делать батчи сразу потому что сейчас в алгоритме батчинга есть баг - мы делаем неоптимальные батчи
5) Создаем заявку в карго с нужным комментов и дальше все по старому :)


### Учет воскресителей

**Новая таблица** `tackles`

```
create table scooters_misc.tackles (
    id text not null primary key,
    kind text not null,
    version integer not null default 1,
    depot_id text null,
    performer_id text null
)
```

**Учёт выдач**. Таблица `tackles_history`.

В ней будем логировать все действия со снастями.

```
create table scooters_misc.tackles_history (
    tackle_id text not null,
    action text not null, -- assign, release, create
    occured_at datetimetz
)
```

**Ручки**

**Список снастей**

Запрос

```
GET v1/tackles/list?kind=power_supply&available=True&depot_id=<id>
```

Ответ

```
{
  "tackles": [
    {
      "id": "id",
      "kind": "kind",
      "version": 1,
      "depot_id": "depot_id",
      "performer_id": "performer_id"
    }
  ]
}
```

**Назначение исполнителя на снасть**

Запрос

```
POST v1/tackles/assign?id=<id>&performer_id=<performer_id>
```

Ответ пустой (в случае успеха)

**Списывание снасти с исполнителя**

Запрос

```
POST v1/tackles/release?id=<id>&performer_id=<performer_id>
```

Ответ пустой (в случае успеха)


**Обновление полей снасти (пока только номер лавки)**

Запрос

```
PATCH v1/tackles?id=<id>&version=<current_version>

{
  "depot_id": "str|null"
}
```

Ответ

```
{
  "tackle": {
    "id": "id",
    "kind": "kind",
    "version": 1,
    "depot_id": "depot_id",
    "performer_id": "performer_id"
  }
}
```


### Конфиг лавок

Есть большой конфиг Лавок - https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/SCOOTERS_MISC_DEPOTS_LOCATIONS?group=scooters-misc

Чтобы засунуть туда возможность включать/выключать батчинг флоу мертвецов предлагаю добавить в конфиг поле `workflows`, определяющее какие `workflows` разрешены в лавке. Что-то такое:

```
- id: grocery:yandekslavka_ordzhonikidze_11c7
  enabled: true
  allowed_from_polygons:
    - ch_akademicheskaya
  location:
    - 37.592186
    - 55.708212
  workflows:
    - name: recharge
      enabled: true
    - name: dead
      enabled: false
```
