## Интегральная метрика стабильности ОХ
Исходим из следующих тезисов:
1. Интегральный процент доступности Datacamp рассчитывается как средняя от процентов доступности четырех метрик хранилища.
2. Процент доступности компонента рассчитывается как отношение времени простоя в сутках к 24 ч. 
3. Доступность по четырем метрикам рассчитываем, не детализируя доступность до компонент.
4. KPI берем от требований пользователей данных (для быстрых и медленных данных - 8 мин, для маркетных данных - 24 часа, для партнерского интерфейса - <0,5% для 500-ок, тайминги: 95% - >5с, 99% - >13с).

Интегральная метрика включает в себя следующие метрики:
1. Время поставки партнерских данных до получателей данных (8 мин) :
    1.1. Пробитие SLA быстрых данных (от момента отправки данных в хранилище до момента доставки в логброкер).\
    1.2. Пробитие SLA медленных данных (до момента поставки в индексатор).
2. Пробитие SLA маркетных данных (от момента появления в YT до доставки на B2C выдачу).
3. Процент 500-ок и пробитие SLA ответов микросервиса для партнеров (строллера).
4. Процент непомайненных вовремя оферов и пробитие SLA событийного майнинга.
5. Пробитие SLA свежести out таблиц.
6. Пробитие SLA скорости скачивания картинок пикроботом.

## Как считаются метрики?

1. KPI быстрых данных

    Для быстрых данных левой границей интервала является **запись сообщения в топик логброкера** в сторону датакемпа.
    Правой границей - **запись сообщения в топик на выходе** из датакемпа.
**Пример** быстрых данных: скрытия, скрытия по стокам, цены и ставки. Данные, полученные через rty (магазинные и прочие через аксесс сюда не входят).
2. KPI медленных данных\
    Это время доезда данных до хранилища, в него входит:
    - получить данные(каталог/парсер/апи)
    - записать в original часть
    - помайнить событийным майнингом
    - записать результат майнинга в actual часть(после всяких валидаций/преобразований)

    Левой границей интервала считаем **старт парсинга**.

    В качестве правой границы интервала используется технический таймстемп транзакции, который пишется внутрь версии оффера. Это примерно соответствует моменту **итоговой записи данных**.
3. KPI маркетных данных

    Левая граница - запись в таблицы хранилища данных, требующих обогащения маркетными знаниями.
    Правая - запись в таблицы хранилища результата обогащения.
**Пример**: поофферные данные - матчинг оффера на карточку, мастер-данные, старая доставка, статус модерации. Данные, полученные от майнера.
4. KPI партнерского микросервиса \
**Строллер** - Синхронный контроллер оферного хранилища; микросервис, отвещающий за обработку http запросов: получение и обновление оффера по идентификаторам, поиск. 
Недоступностью считаем превышение порога **500-ых ошибок >0,5%** или увеличение времени ответа на запросы: **95% - >5с**, **99% - >13с**.

## Дашборд метрик доступности
Дашборд содержит в себе отображение интегральной метрики и метрик доступности компонент в отдельности. [Смотреть тут](https://datalens.yandex-team.ru/sxsn29208df6l-stabilnost-datakempa?state=433e2e83159)

## Автоматическое создание тикетов
При падении метрики доступности ниже 95% создается тикет в очереди MARKETINDEXER и исполнителем ставится OnCall дежурный.

Если вас назначили исполнителем:
* Если понятно, что привело к падению метрики и что нужно чинить: прикрепите тикет на починку проблемы к тикету пробития интегральной метрики и закройте последений
* Если непонятно: заведите тикет для расследования проблемы на саппорт, прикрепите его к тикету пробития интегральной метрики и закройте последний


## Алерты
<details>
<summary>datacamp.quick.*</summary>

- testing

    не считается
- prestable, production

    [Свежесть документов в RTY](https://juggler.yandex-team.ru/project/market.datacamp/aggregate?host=mi-datacamp-quick-pipelines-white&service=quick_pipelines&project=market.datacamp)
</details>

<details>
<summary>datacamp.stroller.errors_perc</summary>

- testing

    [5xx ответы по ручкам](https://juggler.yandex-team.ru/aggregate_checks/?project=market.datacamp&query=host%3D*stroller*testing%26service%3D*5xx*)
- prestable

    [5xx ответы по ручкам](https://juggler.yandex-team.ru/aggregate_checks/?project=market.datacamp&query=host%3D*stroller*prestable%26service%3D*5xx*)
- production

    [5xx ответы по ручкам](https://juggler.yandex-team.ru/aggregate_checks/?project=market.datacamp&query=host%3D*stroller*production%26service%3D*5xx*)
</details>

<details>
<summary>datacamp.stroller.timing</summary>

- testing

    [тайминги общие](https://juggler.yandex-team.ru/project/market.datacamp/aggregate?host=datacamp-stroller-testing&service=stroller-timings-testing&project=market.datacamp)
- prestable

    [тайминги общие](https://juggler.yandex-team.ru/project/market.datacamp/aggregate?host=datacamp-stroller-prestable&service=stroller-timings-prestable&project=market.datacamp)
- production

    [тайминги общие](https://juggler.yandex-team.ru/project/market.datacamp/aggregate?host=datacamp-stroller-production&service=stroller-timings-SLO&project=market.datacamp)
</details>

<details>
<summary>datacamp.market_data.event_mining</summary>

- testing

    - [Лаг топика из майнера](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/lb-commit-time-lag-testing-united-datacamp-offers-from-miner)
    - [Лаг топика в майнер](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/485c2a4d-5b92-4946-9b40-aad6fadbd7e4)
- prestable, production

    - [Лаг топика из майнера](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/04eb83ce-9441-4984-85f2-3ac8669db123)
    - [Лаг топика в майнер](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/815eca44-b1fa-446d-a570-62129b81c2cd)
</details>

<details>
<summary>datacamp.market_data.regular_mining</summary>

- testing

    [Процент непомайненных вовремя оферов](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/3a3573ad-336c-4c03-a9f6-8da91f222302)
- prestable, production

    [Процент непомайненных вовремя оферов](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/42241e38-54a8-4e12-a895-ec17646fc3fe)
</details>

<details>
<summary>datacamp.partner_data.events</summary>

- testing

    - [Лаг топика market-quick](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/2fd243e6-5d56-4817-8287-cf272edf1c27)
    - [Лаг топика assortment-market-quick](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/lb-commit-time-lag-test-assortment-market-quick)
- prestable, production

    - [Лаг топика market-quick](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/00db5361-6976-45db-9523-a9b076eed8ac)
    - [Лаг топика assortment-market-quick](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/lb-commit-time-lag-prod-assortment-market-quick)
</details>

<details>
<summary>datacamp.partner_data.parsing</summary>

- testing

    - [Лаг топика white/datacamp-update-tasks](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/9e287665-b2ff-4df5-8ffc-55623a3e38f5)
    - [Лаг топика datacamp-qoffers](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/65cdd026-1cb7-44db-9286-ad3edf873ec2)
    - [Лаг топика datacamp-qoffers-upload-update](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/commit-time-lag-testing-united-datacamp-qoffers-upload-update)
- prestable, production

    - [Лаг топика white/datacamp-update-tasks](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/c2cab858-9f60-4b64-82e0-1ce3e4ca9bf4)
    - [Лаг топика datacamp-qoffers](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/5ac602bf-0053-48e0-a34e-74f63bbf6edf)
    - [Лаг топика datacamp-qoffers-upload-update](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/commit-time-lag-prod-united-datacamp-qoffers-upload-update)
</details>

<details>
<summary>datacamp.pictures.market.download_speed_q95</summary>

- testing

    [Мало данных](https://nda.ya.ru/t/zE6n9a5O58ZtSc), алерта нет
- prestable

    [Скорость скачивания картинок в неймспейсе marketpic (p95)](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/77225d7e-4c96-49c4-bd4c-02fdbebf687c)
- production

    [Скорость скачивания картинок в неймспейсе marketpic (p95)](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/20b5a398-6324-4497-926c-52fa410b8486)
</details>

<details>
<summary>datacamp.slow.*_out</summary>

- testing

    [Свежесть out таблиц](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/3bf82624-7414-4042-b957-4c40cedba41c)
- prestable, production

    [Свежесть out таблиц](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/6f6cf84d-ec1a-4b33-8213-6ca43ef28b86)
</details>
