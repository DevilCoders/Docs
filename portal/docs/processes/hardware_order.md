## Общее описание процесса заказа и инструментов

{% note warning %}

Необходимо прочитать перед началом оформления заказа [полное описание процесса и инструментов](https://capacity-planning.daas.yandex-team.ru/about/index.html)

{% endnote %}

## Календарь заказа

Полезно добавить в свой календарь для наблюдения расписание этапов заказа: [Календарь](https://calendar.yandex-team.ru/embed/week?embed&layer_ids=74680&uid=1120000000025851)

## График поставки железа

Обычно железо приходит: апрель, август, ноябрь **следующего года**. Об этом будут дополнительные оповещения в тикетах заказа.
Правильнее смотреть [в официальном графике](https://capacity-planning.daas.yandex-team.ru/timeline/index.html)

## Где посмотреть текущий заказ

Все заявки находятся в [ABC](https://abc.yandex-team.ru/services/home/hardware/) и должны быть в статусе "Одобрена", "Подтверждена" или "Готова к выдаче". Любые другие статусы вызывают подозрения.

## Под какие задачи заказывать

Ресурсы заказываются под 2 типа задач:
1. Поддержка естественного роста.
1. Запуск новых продуктов.

На эти два направления нужно оформлять _разные заявки_.

## С чего вообще начать

Сначала посмотреть примеры прошлых заказов.
Взять эксельку и скопировать её под новый заказ.

## Экселька для расчёта и учёта

Экселька имени Наташи лежит тут:
1. [2020](https://yandexteam-my.sharepoint.com/:x:/g/personal/wwax_yandex-team_ru/EVrQ-UEFlJlHr2utf4JhjCUBmRTJ1bNj5hVkCQri3TwHOw?e=0uxfXO)
1. [2021](https://yandexteam.sharepoint.com/:x:/s/morda-dev/EQteH8NpDVpChuZAN0C96CMBfnHsLdRKRHt0vm80vLwqGQ?e=6Shfak)


## Схема действий

{% note warning %}

Заказ ресурсов оформляется в августе - в сезон спада трафика. В октябре вероятен рост трафика до 30%. За основу нужно брать прогноз **на октябрь**.

{% endnote %}

{% note warning %}

Железо будет приходить через год после оформления заказа, значит прогноз нужно иметь на **2 года** вперёд.
Также нужно учитывать ресурсы, заказанные в прошлом году, которые будут приходить в текущем.

{% endnote %}

1. Скорректировать текущие значения в эксельке на новый сезон (rps, dau, resp time)
1. Внести проекты, под которые нужно заказывать отдельно
1. Задать вопросы менеджерам про прогнозы запуска проектов, а также по выходу существующих проектов на новые платформы
1. Запросить у аналитиков прогнозы роста DAU по платформам (если этого нет, то оценить по текущему тренду за прошедший год)
1. Утвердить полученные прогнозы роста у менеджеров
1. Оценить потребности в железе под новые продукты, отдельно под каждый продукт/проект (брать план Градиента **1.2**)
1. Оценить потребности инфраструктуры по переездам
1. Оценить потребности в железе под обеспечение естественного роста (sustain)
1. Оформить заявки (заявки будут читать ответственные за сервисы и задавать вопросы, помогать)
1. Предупредить наши смежные сервисы о прогнозе роста трафика (особенно сервисы, где трафик в сервис равен трафику в морду - Новости, Погоду и тп), так как на них трафик растёт линейно
1. Если давали ресурсы кому-то в долг, то проследить, чтобы они были заказаны сервисом-должником

## Как оценить потребности в железе под новый продукт

Для оценки потребления новым продуктом нужно:
- оценить аудиторию продукта (DAU) с помощью менеджера (на запуске + рост за год)
- оценить характер трафика (сколько запросов будет генерировать один заход пользователя)
- оценить, сколько запросов на пользователя в среднем будет в сутки

Из этих значений можно примерно получить **RPS**.

Если бекенд однопоточный, то оценить время работы бекенда в **ms** в 95й перцентили.
Если бекенд многопоточный и какой ещё угодно параллельный, тогда оценить время работы бекенда в 95й перцентили, умножить на количество потоков и получить эталонные **ms**, как будто это однопоточный бекенд.

Затем ``RPS * ms / 1000`` и получится количество CPU, необходимое для обслуживания одного запроса.
Это значение умножить на коэффициент запаса.

Для всех остальных ресурсов (mem, ssd, net...) берутся коэффициенты в пересчёте на ядро или контейнер. То есть, мы заказываем не отдельные ресурсы, а заказываем cpu, из которого формулами рассчитываются остальные ресурсы.

## Как оценить потребность в железе на поддержку (sustain)

Заказывать нужно **дополнительное** количество ресурсов.
Если ожидается переезд из одной инфраструктуры в другую (из голована в соломон, из yp в deploy), тогда нужно уточнить у этой инфраструктуры необходимость заказывать отдельно железо под переезд.

Для оценки потребности в ресурсах на обеспечение роста нужно:
- оценить динамику роста DAU по платформам на год вперёд
- взять время ответа бекенда по платформам в 95й перцентили
- взять текущий трафик по платформам

Исходя из этих значений спрогнозировать прирост трафика через год (брать оптимистичный прогноз).
Заказывать ресурсы по тому же принципу, как и на новый продукт.

### Где взять прогноз роста аудитории

1. Веб
- [Десктоп](https://stat-beta.yandex-team.ru/Yandex/Others/YANRevenueForecast?scale=d&quantile=_in_table_&measure=dau&version=2020-07-26&slice=%09internal%09%D0%AF.%D0%9C%D0%BE%D1%80%D0%B4%D0%B0%09Desktop%09&_incl_fields=value&date_min=2016-01-01+00%3A00%3A00&date_max=2023-08-01+23%3A59%3A59) 
- [Тач](https://stat-beta.yandex-team.ru/Yandex/Others/YANRevenueForecast?scale=d&quantile=_in_table_&measure=dau&version=2020-07-26&slice=%09internal%09%D0%AF.%D0%9C%D0%BE%D1%80%D0%B4%D0%B0%09Touch%09&_incl_fields=value&date_min=2016-01-01+00%3A00%3A00&date_max=2023-08-01+23%3A59%3A59)

2. Бро
- [Десктопный](https://stat-beta.yandex-team.ru/Yandex/Others/YANRevenueForecast?scale=d&quantile=_in_table_&measure=dau&version=2020-07-26&slice=%09internal%09%D0%AF.%D0%91%D1%80%D0%BE%09Desktop%09&_incl_fields=value&date_min=2016-01-01+00%3A00%3A00&date_max=2023-08-01+23%3A59%3A59)
- [Мобильный](https://stat-beta.yandex-team.ru/Yandex/Others/YANRevenueForecast?scale=d&quantile=_in_table_&measure=dau&version=2020-07-26&slice=%09internal%09%D0%AF.%D0%91%D1%80%D0%BE%09App%09&_incl_fields=value&date_min=2016-01-01+00%3A00%3A00&date_max=2023-08-01+23%3A59%3A59)

3. [ПП](https://stat-beta.yandex-team.ru/Yandex/Others/YANRevenueForecast?scale=d&quantile=_in_table_&measure=dau&version=2020-07-26&slice=%09internal%09%D0%9F%D0%9F%09App%09&_incl_fields=value&date_min=2016-01-01+00%3A00%3A00&date_max=2023-08-01+23%3A59%3A59).

Или можно брать тут, если ничего другого нет: [Дашборд аналитиков](https://datalens.yandex-team.ru/oy2ubw3rnq7ul-dnevnoy-dashbord-portala?tab=d7N&state=93f8140c442)

## Как считается коэффициент запаса

На 2021.08.23 приняты следующие значения:

- платформа	10%
- деплой (релизы) 10%
- 1дц 50%
- инфоповоды 20%
- ядро морды (кешапы, парсеры и тп)	20%
- спецпроекты 10%	
- новая функциональность 10%
- компенсация недоутилизации 5% (так как для оценки необходимых ядер берется 95я перцентиль)

Итого 135%

Следовательно, полученные значения нужно умножать на **2.35**

## Как расчитать остальные значения

mem = cpu * 2

Для остальных ресурсов (ssh, io, net) нужно посчитать, сколько контейнеров получится из новых ресурсов, взять текущие значения в продакшене и получить новые необходимые ресурсы.

## У каких провайдеров заказывать

[Посмотреть тут](https://wiki.yandex-team.ru/Intranet/abc/features/hardware/#providers)

## Разные полезные ссылки и инструкции
[s3](https://clubs.at.yandex-team.ru/storage/441)

[LogFeller](https://clubs.at.yandex-team.ru/data/77), [Графики](https://datalens.yandex-team.ru/2ihfm9k7771ky-kontroliruemyy-rost-dannyh-latest?tab=JV&state=42dbe9221081)

[Solomon](https://clubs.at.yandex-team.ru/solomon/781), [Stored metrics](https://datalens.yandex-team.ru/bhtpzroxy6ng6-solomon-usage-2021?state=03308705719), [Write Metrics](https://solomon.yandex-team.ru/admin/projects/yasm/autoGraph?selectors=service%3D%22tsdb%22%2C+cluster%3D%22production_replica_0%22%2C+sensor%3D%22tsdb.accepted.points%22%2C+host%3D%22cluster%22%2C+itype%3D%22wfront%22&b=1w)

[SandBox](https://st.yandex-team.ru/DEVTOOLS-7529)

[YT](https://clubs.at.yandex-team.ru/yt/4096/), [burst_meter](https://yt.yandex-team.ru/hahn/resource-planner/cpu?pools=morda), [Текущее потребление](https://nda.ya.ru/t/xtrk4X033X6yGe), [Resource Planner](https://yt.yandex-team.ru/hahn/resource-planner/hdd?accounts=morda&pools=logfeller-morda)

[LogBroker](https://st.yandex-team.ru/LBOPS-5921)

## Обоснование заказа

Для предыдущих заказов было достаточно приложить расчеты: текущий rps, время ответа ручек, формулы расчета.

## Примеры предыдущих заявок

1. [Новый продукт](https://st.yandex-team.ru/DISPENSERREQ-6782)
1. [Рост](https://st.yandex-team.ru/DISPENSERREQ-5531)

## Полезные контакты

1. Ответственный за планирование в Портале [Илья](https://staff.yandex-team.ru/golubtsov)
1. [Комитет планирования](https://abc.yandex-team.ru/services/capacity-planning-comitee/)

## Что делать, если ресурсы нужны уже сейчас
1. Можно попросить ресурсы в долг у смежных подразделений, обещая вернуть из заказа, который уже подтверждён и приедет в будущем.
1. Если ресурсов ни у кого нет, то можно сходить в [комитет capacity planning](https://abc.yandex-team.ru/services/capacity-planning-comitee/) и попросить там, обычно у них есть резерв.
1. Также можно оформить дозаказ ресурсов весной, если осенний заказ был сделан некорректно.

## История заказов
### 08.2021
[DISPENSERREQ-8564: [aug2021] Morda.Sustain (Portal)](https://st.yandex-team.ru/DISPENSERREQ-8564)

[DISPENSERREQ-8574: [aug2021] Morda.Go (Portal)](https://st.yandex-team.ru/DISPENSERREQ-8574)

[DISPENSERREQ-8585: [aug2021] Morda.Apphost (Portal)](https://st.yandex-team.ru/DISPENSERREQ-8585)

[DISPENSERREQ-8590: [aug2021] Morda.Dev (Portal)](https://st.yandex-team.ru/DISPENSERREQ-8590)

[DISPENSERREQ-8684: [aug2021] Morda.Betas (Portal)](https://st.yandex-team.ru/DISPENSERREQ-8684)

[DISPENSERREQ-8762: [aug2021] Главная страница (Морда) order to YT: hahn (Portal)](https://st.yandex-team.ru/DISPENSERREQ-8762)

[DISPENSERREQ-8842: [aug2021] Morda.Madm (Portal)](https://st.yandex-team.ru/DISPENSERREQ-8842)
