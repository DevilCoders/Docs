# porchmark-metrics

## ссылки

- [postgres-кластер](https://yc.yandex-team.ru/folders/fooasjkvnrvo67kkfdou/managed-postgresql)
- [vault, porchmark-metrics-db-password](https://yav.yandex-team.ru/secret/sec-01eq1edenc7vnf81w3cpkd339f/explore/versions)
- [vault, porchmark-metrics-db-read-password](https://yav.yandex-team.ru/secret/sec-01eq1mz70hvy5kp1p69dn4k9xx)
- [datalens, read connection](https://datalens.yandex-team.ru/connections/5rqut6w8180o0-porchmark-metrics-db)


## utils

- [pgmigrate](https://github.com/yandex/pgmigrate)

__

- https://stackoverflow.com/a/50173148
- https://sandbox.yandex-team.ru/task/894503826/resources
- https://pypi.org/project/schema/

## migrations

```bash
virtualenv _venv
. _venv/bin/activate
pip install -r requirements.txt
cd porchmark-metrics-db

# создать и заполнить .production.env.sh по шаблону .example.env.sh

. .production.env.sh && pgmigrate info

# смотрим версию на которую нужно мигировать и передаем ее в -t

. .production.env.sh && pgmigrate migrate -t 1
```

## parse and save example

```
cd parse-save
. .production.env.sh && python example.py
```

# format 1.0

- [postgres data types](https://www.postgresql.org/docs/12/datatype.html)

database: `porchmark-metrics`
table: `metrics`

**! Для БД должно быть включено расширение `uuid-ossp`**


## список полей

- [x] id
- [x] app_owner
- [x] app_repo
- [x] project
- [x] app_branch
- [x] commit
- [x] test_mode
- [x] test_page
- [x] compare_id
- [x] sandbox_task_id
- [x] sample_url
- [x] test_url
- [x] porchmark_config
- [x] porchmark_version
- [x] report_version
- [x] format_version
- [x] created_at
- [x] updated_at
- [x] started_at
- [x] completed_at
- [x] status
- [x] status_message
- [x] extra
- **__ metrics**
- [x] request_start
- [x] response_start
- [x] response_end
- [x] first_paint
- [x] first_contentful_paint
- [x] dom_content_loaded_event_end
- [x] load_event_end
- [x] dom_interactive
- [x] dom_complete
- [x] market_ttr
- [x] market_tti
- [x] node_count
- [x] image_count
- [x] script_count
- [x] style_count
- [x] transfer_size
- [x] encoded_body_size
- [x] decoded_body_size
- **__ diffs**
- [x] diff_request_start
- [x] diff_response_start
- [x] diff_response_end
- [x] diff_first_paint
- [x] diff_first_contentful_paint
- [x] diff_dom_content_loaded_event_end
- [x] diff_load_event_end
- [x] diff_dom_interactive
- [x] diff_dom_complete
- [x] diff_market_ttr
- [x] diff_market_tti
- [x] diff_node_count
- [x] diff_image_count
- [x] diff_script_count
- [x] diff_style_count
- [x] diff_transfer_size
- [x] diff_encoded_body_size
- [x] diff_decoded_body_size

в скобках в заголовке поля указывается источник - откуда заполняется поле

- db
- task
- report

## подробное описание всех полей

### [db] `id`: uuid, primary key

уникальный uuid для каждой записи, создается БД

### [task] `app_owner`: varchar(100)

организация на github = `market`

### [task] `app_repo`: varchar(100)

репозиторий на github = `marketfront`

### [task] `project`: varchar(50)

проект в репозитории = `market` OR  `pokupki`

### [task] `app_branch`: varchar(255)

git-ветка

### [task] `commit`: varchar(60)

hash git-коммита

### [task] `test_mode`: varchar(30)

[Режимы работы porchmark](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L18)

От этого зависит скорость и точность, [опытным путем подобрали значения](https://st.yandex-team.ru/GOALZ-87197#5fb160c9e452712aef0bf652) и они будут в конфиге для режимов light и normal

### [task] `test_page`: varchar(30)

страница для теста, урлы также находятся в [конфиге проекта](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L4)

= `index` OR `product` OR `catalog` OR `search`

### [internal] `compare_id`: varchar(300)

Уникальный идентификатор для проекта, ветки, режима и страницы

Для одной ветки может быть несколько запусков, например, сделали PR и там обнаружилась деградация, после этого ее исправили и снова был запущен таск, но это уже другой запуск по id, но по compare_id они будут одинковы

Значение заполняется в таске сохранения

= `${app_owner}-${app_repo}-${app_branch}-${project}-${test_mode}-${test_page}`

### [task] `sandbox_task_id`: numeric(0)

id sandbox-таска

### [report] `sample_url`: varchar(300)

Урл эталона

### [report] `test_url`: varchar(300)

Урл тестового стенда

### [task] `porchmark_config`: jsonb

Полный конфиг porhmark


### [report] `porchmark_version`: varchar(10)

Версия porchmark


### [report] `report_version`: numeric(1)

Версия porchmark-отчета `report_total.json`

Сейчас будет 0.0, пока в самом отчете нет версии

### [task] `format_version`: numeric(1)

Версия текущего формата, дальше будет описано много jsonb-полей, эта версия как раз нужна чтобы понимать и фильтровать по наличию данных по перцентилям и другим данным

Сейчас версия = `1.0`

### [db] `created_at`: timestamp

Timestamp создания записи в БД

Заполняется базой при создании

### [db] `updated_at`: timestamp | null

Timestamp модификации записи, заполняется БД

### [report] `started_at`: timestamp

Timestamp когда был запущен porchmark


### [report] `completed_at`: timestamp

Timestamp когда завершился porchmark


### [report] `status`: varchar(10)

Статус проверки

= `success` OR `failed`


### [report] `status_message`: varchar(200)

Текстовое описание статуса

### [?] extra: jsonb | null

Поле может пригодится для флагов при обработке данных

### __ metrics

Формат всех метрик одинаковый, если в описании не описано иное

- `q50`
  - `sample` - значение с эталонного стенда
  - `test` - значение с тестового стенда
- `q80`
  - `sample`
  - `test`
- `q95`
  - `sample`
  - `test`

Пока для метрик есть только эти перцентили, но дальше можно добавить еще -- <mark>эти изменения должны обязательно изменить версию формата (поле `format_version`)</mark>

### [report] `request_start`: jsonb

Время потраченное на dns resolve, ssl handshake, connect до момента начала запроса. В нашем случае все выполняется локально поэтому здесь практически всегда значения в районе 1ms

Кроме перцентилей только в этой метрике есть значение `count` - общее количество запросов страницы для каждого стенда, может отличаться на единицу между sample и test

- `count`
  - `sample`
  - `test`
- `q50`
  - ...

### [report] `response_start`: jsonb

Время потраченное на обработку запроса сервером до начала полуения ответа, в нашем случае мы собираем WPR-архив и также изолируемся от сети и издержек на сервер

Чуть подробнее можно почитать [в черновике на wiki](https://wiki.yandex-team.ru/users/asvasilenko/market/plan/marketfront-6252-poisk-degradacijj-do-reliza/draft-porchmark-doc/#performance-testyporchmark2.0)


### [report] `response_end`: jsonb

Время потраченное на полное получение html-ответа


### [report] `first_paint`: jsonb

[MDN](https://developer.mozilla.org/ru/docs/Glossary/First_paint) - время между переходом на страницу и моментом, когда браузер отображает первые пиксели на экране

### [report] `first_contentful_paint`: jsonb

[MDN](https://developer.mozilla.org/ru/docs/Glossary/First_contentful_paint) - время, за которое пользователь увидит какое-то содержимое веб-страницы, например, текст или картинку.

Эта метрика показывает, какое время потребуется браузеру для отображения части DOM после того, как пользователь перешёл на веб-страницу. Контентом в данном случае считаются любой текст, изображения, не пустой canvas и SVG. Данный показатель не учитывает загрузку контента в iframe, но учитывает текст, шрифт которых ещё загружается.

### [report] `dom_content_loaded_event_end`: jsonb

[MDN](https://developer.mozilla.org/ru/docs/Web/API/Window/DOMContentLoaded_event) - Событие DOMContentLoaded происходит когда весь HTML был полностью загружен и пройден парсером, не дожидаясь окончания загрузки таблиц стилей, изображений и фреймов. Значительно отличающееся от него событие load используется для отслеживания только полностью загруженной страницы

### [report] `load_event_end`: jsonb

[MDN](https://developer.mozilla.org/ru/docs/Web/API/Window/load_event) - Событие load происходит когда ресурс и его зависимые ресурсы закончили загружаться.


### [report] `dom_interactive`: jsonb

[MDN](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceTiming/domInteractive) - парсер закончил обрабатывать основной документ, страница отрисована.

### [report] `dom_complete`: jsonb

[MDN](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceTiming/domComplete), [Google Developers](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp?hl=ru) - загрузка всего контента страницы завершена

### [report] `market_ttr`: jsonb

То значение, которое мы видим на графиках.

[Берется из таймеров](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L77) виджетов - [(eventTimers[].portion === 'firstScreen').occured](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L118)

По сути это время когда виджеты первого экрана приехали на фронт, но еще не инициализировались

Сами таймеры отсылаются в метрику и доступны на странице в [window.marketMandrel](https://github.yandex-team.ru/market/mandrel/blob/b3951cda1512dd7a567d60328d878e93f7076384/src/launchClient/index.js#L149)

### [report] `market_tti`: jsonb

Берется из таймеров виджетов [(portion === firstScreen).occured + .duration](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L119)

По сути это market_ttr + время на инициализацию виджетов в браузере

### [report] `node_count`: jsonb

Общее количество DOM-нод в документе

Получаем в [пост-обработке](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L120) после открытия страницы

Может использоваться для интерпретации отчета, например, видим что страница очень сильно ускорилась, но при этом количество nodeCount тоже сократилось (может оказаться что-то на странице сломалось :))

### [report] `image_count`: jsonb

Общее количество картинок на странице - тэгов `<img>`

Получаем в [пост-обработке](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L121) после открытия страницы


### [report] `script_count`: jsonb

Общее количество скриптов - тэгов `<script>`

Получаем в [пост-обработке](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L122) после открытия страницы

### [report] `style_count`: jsonb

Общее количество стилей - тэгов `<style>`

Получаем в [пост-обработке](https://github.yandex-team.ru/market/marketfront/blob/master/pokupki/configs/porchmark/helpers.js#L123) после открытия страницы

### [report] `transfer_size`: jsonb

Размер переданного по сети в байтах

### [report] `encoded_body_size`: jsonb

Размер страницы (html) со сжатием в байтах

### [report] `decoded_body_size`: jsonb

Размер страницы (html) без сжатия в байтах


### __diffs

Далее идут значения разницы метрик между эталоном (sample) и тестом (test)

Формат одинаковый для всех метрик, если не описано иное

- `q50`
  - `test` - из значения test вычитаем sample, получаем насколько `test` быстрее или медленнее `sample`
- `q85`
  - `test`
- `q90`
  - `test`


### [report] `diff_request_start`: jsonb

добавляется разница в количестве итераций

- `count`
  - `test`
- `q50`
  - ...

### [report] `diff_response_start`: jsonb

Общий формат diff

### [report] `diff_response_end`: jsonb

Общий формат diff

### [report] `diff_first_paint`: jsonb

Общий формат diff

### [report] `diff_first_contentful_paint`: jsonb

Общий формат diff

### [report] `diff_dom_content_loaded_event_end`: jsonb

Общий формат diff

### [report] `diff_load_event_end`: jsonb

Общий формат diff

### [report] `diff_dom_interactive`: jsonb

Общий формат diff

### [report] `diff_dom_complete`: jsonb

Общий формат diff

### [report] `diff_market_ttr`: jsonb

Общий формат diff

### [report] `diff_market_tti`: jsonb

Общий формат diff

### [report] `diff_node_count`: jsonb

Общий формат diff

### [report] `diff_image_count`: jsonb

Общий формат diff

### [report] `diff_script_count`: jsonb

Общий формат diff

### [report] `diff_style_count`: jsonb

Общий формат diff

### [report] `diff_transfer_size`: jsonb

Общий формат diff

### [report] `diff_encoded_body_size`: jsonb

Общий формат diff

### [report] `diff_decoded_body_size`: jsonb

Общий формат diff
