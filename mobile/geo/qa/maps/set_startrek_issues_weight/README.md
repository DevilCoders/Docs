#### Описание
Скрипт, проставляющий веса тикетам в RFT для дашборда тестирования.
В config.py словарь WEIGHTS, определяющий коэффициенты веса.
При редактировании конфига ставить ревьюером @kamaeff.

#### Запуск
1. Собрать c помощью `ya make -DDISABLE_BLACKLIST=yes`
2. Запустить собранный бинарник
   При запуске без опций скрипт только рассчитывает веса и выводит их в stdout.

Чтобы проставить веса тикетам, запускать с ключом `--apply`.
Для работы скрипта требуется положить OAuth-токен стартрека того пользователя,
от чьего имени будут проставляться веса, в переменную окружения `ST_TOKEN`.

#### Регулярный запуск
Скрипт запускается каждые 15 минут в Нирване посредством Реактора (ссылки ниже).
Запускается от имени робота @robot-mobnavi-cloner, поэтому важно убедиться, что у этого робота есть доступы:
- к самому фильтру
- к тикетам, попадающим в фильтр

### Конфиг
Конфиг для назначения весов располагается в файле config.py в словаре WEIGHTS.
Ключами словаря являются id фильтров из трекера – цифры из ссылок вида https://st.yandex-team.ru/issues/429272
Скрипт получает тикеты по указанному фильтру и проставляет им веса в соответствии с конфигом.
По умолчанию применяется только один фильтр – 429272, но при необходимости можно добавить другие.
Значениями словаря являются словари с развесовкой по разным параметрам, все они обязательны и перечислены ниже.


#### sprint
Спринт тикета. В конфиге можно указать множители для следующих типов спринта:
- `SprintType.PREVIOUS` – вес для тикетов в уже закончившемся спринте
- `SprintType.CURRENT` – вес для тикетов в текущем спринте
- `SprintType.NEXT` – вес для тикетов в ещё не начавшемся спринте
- `SprintType.NONE` – вес для тикетов без спринта

Если у тикета указаны несколько спринтов, в расчёт берётся самый ранний из них.

Если тип спринта тикета отсутствует в конфиге, будет применён стандартный множитель – единица.

#### type
Тип тикета. Словарь с развесовкой для типов тикета, следующего вида:
```python
    "type": {
        "bug": 2,
        "task": 1.1,
    },
```

Ключи словаря – ключи типов из API Startrek, посмотреть можно в [трекере](https://st.yandex-team.ru/admin/types)
или в [API](https://st-api.yandex-team.ru/v2/issuetypes?pretty).
Если тип тикета не будет найден в словаре, к нему будет применён стандартный множитель – единица.
Само поле `"type"` обязательное, но если тип тикета не важен, может содержать просто пустой словарь:
```python
    "type": {},
```

#### priority
Приоритет тикета. В конфиге можно заполнить множители для пяти приоритетов:
- "trivial"
- "minor"
- "normal"
- "critical"
- "blocker"

Если приоритет тикета отсутствует в конфиге, к тикету будет применён стандартный множитель – единица.

Само поле `"priority"` обязательно, но если приоритет тикета не важен для весов, может содержать просто пустой словарь:
```python
    "priority": {},
```

#### tags
Теги тикета. Само поле `"tags"` обязательно и должно содержать словарь `"имя_тега": множитель`.
Если развесовка по тегам не нужна, то словарь можно сделать пустым: `"tags": {}`
Если в тикете встречаются несколько тегов из конфига, то их веса перемножаются.
**ВАЖНО!** Все теги должны быть указаны строго в нижнем регистре.
Вкратце, это нужно потому что теги в трекере регистронезависмы, а строки в Python – нет.

#### components
Работает аналогично тегам, но для компонентов.
**ВАЖНО!** В отличе от тегов, имена компонентов должны быть не в нижнем регистре, а один в один как они называются в трекере.

#### statusStartTime
Веса в зависимости от того, сколько времени на момент проставления веса тикет уже висит в определённом статусе.
Представляет собой словарь с вложенными словарями по статусам.
Ключи словаря – это ключи статусов из трекера.
Значения словаря – вложенные словари.
Ключи вложенных словарей – временные интервалы python.
Если по-простому, то пишем `dt.timedelta(days=количество_дней)`.
Пример:
```python
"statusStartTime": {
    "readyForTest": {
        dt.timedelta(days=3): 10,
        dt.timedelta(hours=10): 2,
        dt.timedelta(days=0): DEFAULT_FACTOR,
    },
    "open": {
        dt.timedelta(days=5): 10,
    },
},
```
В данном примере:
- если тикет висит в статусе `readyForTest` 3 часа, то его вес домножится на `DEFAULT_FACTOR`, т.е. на 1
- если тикет висит в статусе `readyForTest` 15 часов, то его вес домножится на 2, потому что это больше, чем `hours=10`, и меньше, чем `days=3`
- если тикет висит в статусе `readyForTest` 4 дня, то его вес домножится на 10, потому что 4 дня это больше, чем `days=3`
- если тикет висит в статусе `open` 2 дня, то его вес не изменится (домножится на `DEFAULT_FACTOR`, равный единице), потому что это меньше, чем `days=5`
- если тикет висит в статусе `open` 10 дней, то его вес домножится на 10, потому что 10 дней это больше, чем `days=5`

Словарь `"statusStartTime"` может быть пустым:
`"statusStartTime": {}`
Тогда время ожидания в статусах не будет никак влиять на вес тикета.

#### Ссылки
- [Папка в Нирване](https://nirvana.yandex-team.ru/browse?selected=11298864)
