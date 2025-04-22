# workflows

Конфиги сущностей Реактора для ETL-процессов аналитического хранилища Вертикалей

Проекты:
- Solomon - [vertis-dwh](https://solomon.yandex-team.ru/admin/projects/vertis-dwh)
- Juggler -  [vertis-dwh](https://juggler.yandex-team.ru/project/vertis-dwh/dashboard?project=vertis-dwh)
- Reactor -  [/verticals/vertis-bi](https://reactor.yandex-team.ru/browse/resolve?path=/verticals/vertis-bi)


Для работы с конфигами используется CLI-утилита [lama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama).

## Структура
Структура директорий соответсвует неймспейсу [/verticals/vertis-bi](https://reactor.yandex-team.ru/browse?selected=7780818) в Реакторе. Подробнее про [организацию процессов в Реакторе](https://wiki.yandex-team.ru/vertis-bi/reactor).

```sql
.
├── stg            -- слой
│  ├── auto        -- домен
│  |   ├── revenue -- код проекта/задачи
│  |   ├── offer
|  |   └── ...
│  ├── realty
│  └── general
├── ods
├── dds
├── dm
├── dq
├── tableau
├── external
├── email
└── utils
```

* `stg`, `ods`, `dds`, `dm` - процессы для загрузки в соответсвующий слой хранилища. Пути к конфигам реакций должны **однозначно** соответствовать путям к таблицам в YT для которых выполняется загрузка. Все директории разбиты на домены `auto`, `realty`, `general`. Подробнее про [слои хранения данных](https://wiki.yandex-team.ru/vertis-bi/#sloixranenijadannyx)
* `dq` - статистические проверки качества данных
* `tableau` - рефреши сущностей Tableau
* `external` - поставки во внешние системы
* `email` - email-рассылки. Гайд для создания [новой рассылки](https://wiki.yandex-team.ru/vertis-bi/guides/generic-email-sender)
* `utils` - технические процессы (инициализация триггеров, подграфы для генерации суррогатных ключей и т.п.)
