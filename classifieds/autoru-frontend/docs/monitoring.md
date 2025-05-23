# Мониторинг

## Список основных дашбордов:

* [autoru-frontends-summary](https://grafana.vertis.yandex-team.ru/d/jUwX30jMk/autoru-frontends-summary) - сводный дашборд по всем сервисам фронтенда авто.ру

* [autoru-nodejs-frontends](https://grafana.vertis.yandex-team.ru/d/000000595/autoru-nodejs-frontends) - дашборд с основной информацией в разрезе по конкретному сервису. Коды ответов, ошибки, роботы, парсеры, мемкеш, версии сервиса

* [autoru-nodejs-frontends-backend-total-timings](https://grafana.vertis.yandex-team.ru/d/gijPm-Iik/autoru-nodejs-frontends-backend-total-timings) - всё про бекенды и эндпоинты: коды и время ответов, рейт запросов, таймауты, ретраи, ошибки

* [autoru-nodejs-frontend-health](https://grafana.vertis.yandex-team.ru/d/G-kshN9ik/autoru-nodejs-frontend-health) - здоровье нод: память, процессы в обработке, биндинги

* [autoru-nodejs-frontends-ssr-timings](https://grafana.vertis.yandex-team.ru/d/i74CyLIiz/autoru-nodejs-frontends-ssr-timings) - всё про контроллеры: время и коды ответов, время ssr, размер пейлоада

* [autoru-frontend_proof-of-work](https://grafana.vertis.yandex-team.ru/d/YovUqQxGk/autoru-frontend_proof-of-work) - всё про Proof of Work: графики по всем ручкам, закрытым за POW

* [autoru-frontend-prometheus-performance](https://grafana.vertis.yandex-team.ru/d/7Rl42HjGk/autoru-frontend-prometheus-performance) - дашборд с показателями нашей системы мониторинга. Если есть проблемы с аномальными графиками/алертами, нужно идти сюда

* <span style="color:slateBlue">[сторонний]</span> [auto-ru-codes](https://grafana.vertis.yandex-team.ru/d/Pi3K-n7Zk/auto-ru-codes) - дашборд админов с данными nginx по всему авто.ру

* <span style="color:slateBlue">[сторонний]</span> [autoru-public-api-requests](https://grafana.vertis.yandex-team.ru/d/V4oPI2Imk/autoru-public-api-requests) - дашборд бекенда по всему publicApi


## Основы и как пользоваться графиками

Для мониторинга наших приложений мы используем Prometheus в качестве системы мониторинга и Grafana для визуализации данных. За каждым графиком лежит PromQL запрос к серверу Prometheus, который можно редактировать.

С основами построения запросов можно ознакомиться [здесь](https://prometheus.io/docs/prometheus/latest/querying/basics/). Пример PromQL запроса для графика запросов от парсеров с разбивкой по сервисам: `sum by(_service) (rate(incoming_requests_total{isParser="true"})[2m])`.

### Аннотации
Для всех основных дашбордов Grafana доступны аннотации, которые включаются через тогглы в верхнем левом углу дашборда. Аннотации - это события деплоя, изменения в экспериментах, инфраструктурные анонсы, которые отображаются на всех графиках, что облегчает поиск причин аномалий на графиках. [Скриншот с примером работы аннотаций](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2013.48.09.png).

### Описания графиков
"Что делать, если я вижу кучу графиков и не понимаю, что это всё значит?" - Около множества графиков в левом верхнем углу есть символ `i`, наведя на который можно прочесть словесное описание графика. [Скриншот с примером](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2013.55.20.png).

### Параметры дашборда
Важно, что у части дашбордов есть параметры. Выбранные параметры изменят часть запросов на дашборде, но не гарантированно всё и эти параметры вручную прокидываются в запрос для каждого графика. Так например в  дашборде по сервисам можно [выбрать конкретный сервис](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2017.40.13.png), а в дашборде по бекендам, [выбрать конкретный бекенд и эндпоинт](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2017.47.03.png).

### Выбор нужного дашборда
Во всём многообразии дашбордов и количестве информации на них можно легко запутаться. При попытке понять, какой дашборд тебе нужен для того или иного случая, стоит в первую очередь определиться с областью исследования, поскольку большинство дашбордов оперируют одними и теми же данными, просто визуализируют их в разном "приближении". Также стоит принять во внимание, что дашборды частично дублируют информацию, где это необходимо и удобно. Примеры по выбору нужного дашборда в процессе исследования проблем:
* Ты дежурный и хочется иногда поглядывать на общую картину всех сервисов? Используй [сводный дашборд по всем сервисам](https://grafana.vertis.yandex-team.ru/d/jUwX30jMk/autoru-frontends-summary).
* Есть проблемы с конкретным сервисом и нужно начать её исследовать? Используй [дашборд по сервисам](https://grafana.vertis.yandex-team.ru/d/000000595/autoru-nodejs-frontends) и выбери нужный в параметрах.
* В дашборде по сервису увидел, что повысился рейт ошибок от конкретного бекенда? Используй [дашборд по бекендам и эндпоинтам](https://grafana.vertis.yandex-team.ru/d/gijPm-Iik/autoru-nodejs-frontends-backend-total-timings), выбери нужный в параметрах.
* Пришел алерт о повышенном времени ответа контроллера? Используй [дашборд по контроллерам](https://grafana.vertis.yandex-team.ru/d/i74CyLIiz/autoru-nodejs-frontends-ssr-timings), выбери нужный в параметрах.
* Хочется увидеть картину на уровень выше, до наших приложений? Используй [админский дашборд по nginx](https://grafana.vertis.yandex-team.ru/d/Pi3K-n7Zk/auto-ru-codes).
* Есть проблемы с мониторингами или видишь аномальные значения на графиках? Используй [дашборд с статистикой по prometheus](https://grafana.vertis.yandex-team.ru/d/7Rl42HjGk/autoru-frontend-prometheus-performance).

### Где посмотреть, какие метрики у нас есть

Все метрики собраны [едином файле с метриками](../auto-core/prometheus/metrics.js)

### Большие пики на графиках мешают восприятию
Grafana сама выбирает значения оси Y на графиках, если она явно не задана. Если за выбранный период наблюдений был какой-то аномальный скачок, то графики становится [сложно воспринимать](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2016.16.22-1.png), особенно если выбран большой временной период, например 7 дней. Чтобы исправить это, можно [открыть редактирование графика](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2017.18.56.png), после чего он откроется на весь экран, а затем [выбрать максимальное значение по оси Y](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2017.21.02.png) для удобного отображения. Далее можно нажать стрелочку "назад" в верхнем левом углу дашборда и график сохранит свои параметры, однако не стоит нажимать кнопку "Сохранить", чтобы настройки графика не сохранились насовсем.

### Как удобно смотреть графики за большой период времени

Если при просмотра графика за несколько дней или недель, начинает хотеться взять лупу или много раз уменьшать временной диапазон, стоит открыть редактирование графика (описано в предыдущем пункте про пики на графиках) и [изменить значение max data points](https://jing.yandex-team.ru/files/yakovlev-sv/Screenshot%202021-08-27%20at%2017.25.02.png) до более низких значений, что сильно улучшит читаемость графика. Важно так же не сохранять изменения.



## Алерты

Алерты - регулярно исполняемые PromQL запросы к серверу Prometheus, которые при возникновении определенных заданных условий сообщают команде разработки о том, что что-то пошло не так.
Алерты лежат в репозитории [prometheus-config](https://a.yandex-team.ru/arcadia/classifieds/infra/prometheus-config/production/alerts);

Пример алерта для `af-desktop`, который сработает если на протяжении 5 минут количество ответов на входящие запросы в секунду __непрерывно__ держалось выше отметки в 270rps.
```
- alert: AFDesktop_TooMany3xxResponses
    expr: sum(autoru:frontend:incoming_requests_count{code=~"^3.*",_service="af-desktop"})
      > 270
    for: 5m
    labels:
      _service: af-desktop
      juggler_aggr_host: vertis_ops_autoru-frontend
      juggler_tag1: response_codes
    annotations:
      description: Too many 3xx response codes {{ .Value }}rps for more than 5 minutes.
      summary: 'af-desktop: Too many 3xx response codes'
```

## Добавление новой метрики

У Prometheus как системы мониторинга есть явные ограничения и паттерны целевого использования. Например, его совершенно точно не стоит использовать для данных с высокой вариативностью вроде id юзера, объявления и пр. Также сам процесс мониторинга предпологает сбор большого количества данных на протяжении всего времени и эти данные нужно где-то хранить. А еще чем больше данных по какой-то метрике, тем сложнее серверу Prometheus обрабатывать PromQL запрос. В общем, мониторинг, это а) не бесплатно б) если быть неосторожным, [можно всё уронить](https://jing.yandex-team.ru/files/yakovlev-sv/Screen%20Shot%202021-05-18%20at%203.56.48%20PM-67624.png). Поэтому нужно хорошо подумать прежде чем добавлять новую метрику, а также примерно расчитать вариативность лейблов. Если в метрике планируется 4 лейбла, у каждого из котрых 2-5 возможных значений, это нормально. А если вам хочется добавить 5 лейблов, у каждого из которых 20+ значений - скорее всего, вы делаете что-то не так. То же самое касается лейблов с значениями 100+.

Как добавить новую метрику:
* изучить [правила нейминга метрик](https://prometheus.io/docs/practices/naming/)
* выбрать лейблы для метрики, осознанно подойти к их именованию. Лейбл `name` - плохой выбор, несмотря на то, что у нас уже есть ряд метрик с такими лейблами
* проверить себя на "я собираюсь сделать что-то плохое": для каждого лейбла новой метрики взять максимальное возможное количество его значений и перемножить их.  Для примера: булевые лейблы `isParser`, `isRobot` и `isAjax` дадут `2 * 2 * 2 === 6`. Если у тебя получилось значение больше тысячи, то с высокой долей вероятности, ты используешь Prometheus как-то не так, проконсультируйся с коллегами
* добавить метрику нужного типа в [единый файл с метриками](../auto-core/prometheus/metrics.js)
* если нужно проверить то, что данные приходят, можно выкатить бранч в тестинг и воспользоваться [Grafana Explore](https://grafana.vertis.yandex-team.ru/explore) и выбрать источник данных `prometheus-testing`.
* добавить график на подходящий дашборд в Granafa

## Recording rules

Некоторые PromQL запросы являются очень ресурсоемкими для сервера Prometheus (что напрямую отражается на времени его ответа) и при этом являются важными и частоиспользуемыми для графиков в дашбордах Grafana и в алертах. Для решения этой проблемы Prometheus позволяет производить оптимизациии над собираемыми данными через recording rules. Если коротко, то это когда по одной очень большой метрике с кучей данных регулярно собирают необходимый запрос и сразу записывают это в другую метрику.

Recording rules лежат в репозитории [prometheus-config](https://a.yandex-team.ru/arcadia/classifieds/infra/prometheus-config/production/recording-rules). Для получившихся в результате выплнения recording-rules метрик действуют [другие правила нейминга](https://prometheus.io/docs/practices/rules/#naming-and-aggregation), в результате получается что-то вроде `autoru:frontend:incoming_requests_count`.
