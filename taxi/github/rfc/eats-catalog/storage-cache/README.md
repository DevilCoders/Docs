# Кэш eats-catalog-storage

## Что кэшируем

В кэше находятся следующие словари:

- словарь [ID ресторана - ресторан]
- словарь [ID зоны доставки - зона доставки]

## Как кэшируем

Сервис eats-catalog-storage предоставляет две ручки:

- для получения зон доставки и их ревизий
- для получения ресторанов их их ревизий

Обсуждение API происходит [здесь](https://github.yandex-team.ru/taxi/rfc/pull/724).

Кэш имеет два независимых периодика, которые наполняют соответствующий словарь и
дампают состояние на диск.

### Start/full update

При первом запуске сервиса кэш попытается взять состояние из локального дампа,
в случае успеха запросы в eats-catalog-storage на получение данных будут
содержать максимальную ревизию из дампа. В том случае, если дампа нет, либо из
дампа не удалось поднять состояние кэша, запросы в eats-catalog-storage будут
отправлены без ревизии вообще.
Подробнее о дампе в [соответствующем разделе](#how-to-dump).

### Incremental update

Периодик отправляет последнюю полученную ревизию, с которой нужно получить
обновления зон или ресторанов.

### Резолв пропусков

В ревизиях возможны пропуски. Пропуск выглядит так:

```plain
place_id: 1
revision: n
...
...
next update
...
place_id: 1
revision: n + m (m > 1)
```

Пропуск ревизии может быть валиден, т.к. один ресторан мог измениться несколько
раз до перестроения индекса eats-catalog-storage (т.е. кэш получил последнее
актуальное состояние).
Пропуск ревизии может быть не валиден, т.к. eats-catalog-storage считал данные
с реплики, которая отстала о мастера таким образом, что некое событие обновления
2 записалось на реплику, а событие обновления 1 еще нет.

На стороне кэша нет возможности понять, был ли пропуск валиден или нет, поэтому
в случае, когда такой пропуск обнаружился, будет сделан дозапрос конкретно этой
ревизии.

- если в ответе пришла ревизия, то применяем ее на соотвествующий словарь (рестораны/зоны)
- если в ответе ревизии нет, то сохраняем ревизию в отдельный список, чтобы
запросить в следующий раз
- если в ответе ревизии нет и она есть в списке "на дозапрос", то проверяем, что
она не вышла за TTL из конфига (время или количество дозапросов); таким образом
мы узнаем натуральный пропуск

### Резолв с помощью таймстампов

Мы рассматривали вариант с запросом данных от стораджа с помощью таймстампа:
например, `now - 5m` как время, с которого нужно получить все обновления, и
запрос за следующей пачкой сделать с максимальным временем из первой пачки.
Тут остается проблема того, что мы не можем определять пропуски, но они рано или
поздно должны уйти, при правильном выборе размера "нахлеста".
Вторая проблема здесь в том, что количество данных, которые отправляет
eats-catalog-storage, вырастет многокрано. Одно дело дозапрашиваь конкреные
ревизии (список интов), другое дело - гонять большие JSON-ы ресторанов или зон.

<a id="how-to-dump"></a>

## Как дампаем и поднимаемся из дампа

Дамп сохранятеся на диск после каждой итерации обновления, когда сформирован
обновленный кэш.
В дампе для каждого элемента хранится его ревизия. При включении сервиса с нуля
из дампа, компонент кэша получает список всех ревизий отсортированных
по-возрастанию. Среди списка ревизий точно также можно найти пропуски и дозапросить
их у eats-catalog-storage.

