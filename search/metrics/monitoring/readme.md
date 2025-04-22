# YTMonitoring

Рассчет метрик для мониторингов на yt.
[Тестовый крон](https://metrics.yandex-team.ru/crons/101096/runs).
## Примеры
### Настройка окружения
Предполагается что пользователь установил [yt cli](https://wiki.yandex-team.ru/yt/userdoc/cli/), положил свой токен в `~/.yt/token` и настроил `~/.yt/config` так что бы по умолчанию использовался hahn (`{proxy={url = hahn}}`).
Так же для работы с метриксом пользователь положил [метриксовый токен](https://wiki.yandex-team.ru/JandeksPoisk/Metrics/API/#avtorizacija) в `~/.metrics/token`.

### Получение запросов из корзинки
Локально
```(bash)
./metrics qg local 109915
```
На yt
```(bash)
./metrics qg yt 109915 //tmp/example_monitoring_qg
```

### Конвертация запросов для прокачки через Scraper-over-Yt (SoY)
#### Локальный запуск
На stdin подается корзинка в формате Qgaas (см. Получение запросов из корзинки), на stdout пишутся запросы, пригодные для прокачки через SoY.
Параметр определяет, с какого хоста качать (в примере это yandex.ru)
```(bash)
cat ~/testing/basket_187240 | ./metrics prepare local yandex.ru
```

Поддерживается передача дополнительных cgi-параметров (encoded-строкой):

```(bash)
./metrics prepare local yandex.ru --cgi 'nocache=da&foo=1'
```

Можно задать собственный класс для подготовки запроса:

```(bash)
./metrics prepare local yandex.ru --engine YandexBaobabParser
```

Подробнее см. метод `prepare` и родственные в [SerpParser](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/parsers/base_parsers.py), также
класс [YandexBaobabParser](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/parsers/yandex_baobab_parser.py).

Конфигурация может быть задана через json файл, содержимое которого попадает в параметры preparer'а:
```(bash)
./metrics prepare local --configuration config.json
```
Где `config.json`:
```(json)
{
    "host": "yandex.ru",
    "preparer": "YandexBaobabParser",
    "profileName": "dummy",
    "ignoreProfileConflicts": True
}
```
Command line аргументы, если заданы, имеют приоритет над файлом конфигурации и перетирают его части. Аргументы profile и ignoreProfileConflicts необязательны. Профили хранятся
[тут](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/profile).

#### Запуск на Yt
Параметры
* хост (в примере yandex.ru)
* табличка, содержащая запросы в формете Qgaas
* табличка, в которая будет заполнена запросами в SoY формате
```(bash)
./metrics prepare yt yandex.ru //tmp/basket_109915 //tmp/prepared_109915
```
* так же можно передавать все те флаги, которые доступны для локального запуска
### Скачка через yt
```(bash)
./metrics download yt //tmp/prepared_109915
```

### Парсинг
Работает с нераспаршенными таблицами scraper, [пример](https://yt.yandex-team.ru/hahn/navigation?path=//home/qe/scraper/dev/example/monitoring_notparsed_table&offsetMode=row).
Локальный запуск:

Вместо ```--module module_name --class class_name``` стоит использовать ```--engine engine```, который можно найти в [prepare_mapping](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform/parsers/preparer_mapping.py)
```(bash)
yt read --format '<encode_utf8=%false>json' //home/qe/scraper/dev/example/monitoring_overyt_notparsed_table > tmp
cat tmp | ./metrics parse local --engine YandexBaobabHTMLParser | jq .
```
Запуск на yt:
```(bash)
./metrics parse yt --engine YandexBaobabHTMLParser //home/qe/scraper/dev/example/monitoring_overyt_notparsed_table //tmp/example_monitoring_parse

```

Запуск локально парсинга вместе с рассчетом метрик
```(bash)
cat tmp | ./metrics parse local --engine YandexBaobabHTMLParser | ./metrics calculate local --aggregate
```

Запуск парсинга локально на одном серпе (html):
```bash
cat content.html | ./metrics parse local --engine YandexBaobabHTMLParser --parse-only
```
Здесь можно ещё добавить опцию `--pretty`, тогда JSON-выхлоп будет красиво отформатирован.


### Расчет метрик
Работает с распаршенными таблицами scraper, [пример](https://yt.yandex-team.ru/hahn/navigation?path=//home/qe/scraper/dev/example/monitoring_parsed_table&offsetMode=row).
Умеет работать локально. Например ниже можно подклеить оценки к первому серпу из таблицы, посчитать метрики и вывести получившиеся серпа со значениями метрик.
```(bash)
yt read --format '<encode_utf8=%false>json' //home/qe/scraper/dev/example/monitoring_overyt_parsed_table > tmp1
head -1 tmp1 | ./metrics calculate local --serps | jq .
```
Или вывести только среднее значение метрик:
```(bash)
head -1 tmp1 | ./metrics calculate local --aggregate
```
В результате получится что-то вроде:
```(json)
[{"count": 1, "metric": "judged-5", "average": 0.8}, {"count": 1, "metric": "empty-serp", "average": 0.0}]
```

Так же можно запустить локальный код на yt:
```(bash)
./metrics calculate yt //home/qe/scraper/dev/example/monitoring_overyt_parsed_table //tmp/example_monitoring_output //tmp/example_monitoring_metrics
```
В результате получится 2 таблицы - одна с серпами с оценками и метриками, вторая со средними значениями.

### Расчет диффа
Для бездифовой скачки есть возможность сравнения серпов попарно. Для этого входные данные должны быть отсортированы по полям GroupId и ConfigId
```(bash)
cat parsed-serps.lines | ./metrics diff local --metric 'diff-2-serps-5'
```
В комаде парсинга важно указать параметр ``--save-ids``, для того чтобы пара (GroupId, ConfigId) была сохранена в результатах парсинга.

#### Аспекты
Списки метрик и обогащений выбираются при помощи агрумента `--aspect`, например что бы рассчитать метрики по картиночным мониторингам стоит запускаться так:
```(bash)
cat image_serps | ./metrcis calculate local --aspect images_monitoring --aggregate
```

### Утилиты
#### Получение элементов оценки
Можно получить неоцененные/все элементы для дооценки по посчитанному серпсету:
```
cat serp_set_with_judgements | ./metrics tool unwrap local --type SEARCH_RESULT --depth 5 > tmp
```
Или то же самое на yt:
```
./metrics tool unwrap //home/qe/scraper/dev/example/monitoring_overyt_parsed_table //tmp/monitoring_ji
```
В данном случае несмотря на отсутствие `--judged` будут выгружены все элементы т.к. по входному серпсету не были рассчитаны метрики и оценки.

Можно сгенерить данные которые можно скормить на вход хитману:
```
cat serp_set_with_judgements | ./metrics tool unwrap local --depth 5 --type SEARCH_RESULT --hitman | jq -s .
```
Поскольку hitman принимает именно массив необходимо jq преобразование.

##### Обогащения
Обогащение можно выбрать при помощи аргумента `--enrichment`, напирмер сгенерить дооценку картиночной релевантностью можно так:
```
cat images_serp_set_with_judgements | ./metrics tool unwrap local --type SEARCH_RESULT --depth 5 --enrichment images_relevance > tmp
```

#### Построение идеального ответа по серпсету
По элементам оценки можно построить идеальный ответ (выгрузить все известные по запросу оценки):
```
./metrics tool ideal yt //tmp/monitoring_ji //tmp/monitoring_ideal --judgements //home/qe/scraper/testing/relevance_judgements
```
Таблица с оценками получена из оригинальной динамической таблицы оценок фильтрацией:
```
yt map cat --src //home/hitman/production/assessments/assessments --dst //home/qe/scraper/testing/relevance_judgements --spec '{input_query="* where hit_type = \'web_5_grades_relevance\'"}' --format yson
```
С [этой](https://yt.yandex-team.ru/hahn/navigation?path=//home/qe/scraper/testing/relevance_judgements&offsetMode=row) таблицей операции работают быстрее, но в ней могут быть не актуальные данные.
#### Подклейка оценок с кастомной нормализацией
```
./metrics tool judgements yt --serpset //home/qe/scraper/dev/example/monitoring_overyt_parsed_table //tmp/monitoring_tmp //tmp/judged_serp
```
После этого в `judged_serp` будет сохранен серп с подклееными оценками, по нему можно посчитать метрики используя команду `calculate` с флагом `--nojudgements`.

##### Локальный запуск
Для локального запуска вместо таблицы оценок стоит пользоваться идеальным ответом что бы не вылеать с oom (в целом для удаленного запуска нормализация по идеальному ответу так же будет работать быстрее):
```
yt read --format '<encode_utf8=%false>json' //tmp/monitoring_ideal > ideal
```
Затем можно запустить аналог mr на jq локально:
```
yt read --format '<encode_utf8=%false>json' //home/qe/scraper/dev/example/monitoring_overyt_parsed_table > parsed_serpset
cat ideal parsed_serpset | ./metrics tool judgements local | jq -s . | jq -c 'sort_by(.hash) | .[]' | ./metrics tool judgements local_reduce > tmp
cat tmp parsed_serpset | jq -s . | jq -c 'sort_by(.id) | .[]' | ./metrics tool judgements local_join_reduce > result_serpset
```
и посчитать по полученному серпсету метрики:
```
cat result_serpset | ./metrics calculate local --nojudgements --aggregate
```

#### Загрузка в Metrics

Загрузить серпа в выходном формате `./metrics calculate` на Metrics:

```bash
cat serpset_with_metrics | ./metrics tool upload local
```

Загрузить по пути в YT:

```bash
./metrics tool upload local path_to_yt
```

Посмотреть какие данные будут загружены можно при помощи
```bash
cat serpset_with_metrics | ./metrics tool convert metrics local | jq . -s > metrics-serpset.json
```

#### Нормализация оценок в соотвествии с функцией нормализации обогащения
```bash
./metrics normalize local --enrichment sinsig --format database
./metrics normalize yt //tmp/sinsig-eval-01-test //tmp/sinsig-eval-01-test-norm --enrichment sinsig --format database
```

enrichment - оценки из какого обогащения нужно нормализовать (выбирается функция нормализации, соответствующая обогащению)

format - формат входных данных, database - оценки из базы оценок, workflow - оценки из графа обогащения.

#### Перепарсинг
Можно перераспарсить большинство серпсетов на метриксе приблизительно такой командой:
```bash
./metrics tool reparse yt --engine GoogleWebParser 33290531 --convert
```
Вместо `engine` надо подставить нужный парсер.

Так можно перераспарсить конкретную таблицу:
```bash
./metrics tool reparse yt //home/metrics/metrics_executable/examples/images_to_reparse --engine YandexImagesJSONParser \
--convert --add-sqp-from-basket 298768 \
--regional WORLD --evaluation IMAGES --aspect default --basket 298768 --filter "true" --name "reparsed_images"
```

Если указан ключ `--convert`, перед заливкой будет произведена конвертация из формата Scraper.

Команда принимает все опции команд `parse`, `tool upload` и `tool convert scraper`, кроме путей к промежуточным таблицам.

#### Серпсеты крона
Получить список серпсетов крона:
```bash
./metrics tool cron info --cron-id 101073 --date-from 2020-04-04 --date-to 2020-04-09 --host-id 8792 --only-serp-ids
```
Список серпсетов по сегодняшний день с информацией о них:
```bash
./metrics tool cron info --cron-id 101073 --date-from 2020-04-04
```
#### Пересчет серпов
Перераспарсить 5 серпов из 101096 за неделю
```bash
./metrics tool recalculate --cron 101096 --limit 5 --engine YandexBaobabHTMLParser
```
И обновить графики
```bash
./metrics tool recalculate --cron 101096 --limit 5 --engine YandexBaobabHTMLParser --update-graphs
```
#### Репарс серпов скачанных через классический scraper
Иногда возникает задача перераспарсить пачку серпов из класического крона, дооценить их, а затем удалить старые, это можно сделать так (на примере METRICSSUPPORT-2747):

Сначала собираем нужные серпа (`--date-from` включается в диапазон, а `--date-to` нет):
```bash
./metrics tool cron info --cron-id 101071 --date-from 2020-03-21 --date-to 2020-03-24 | jq '.[] | {id, date, name, hostId, scraperId, cronSerpDownloadId}' -c | grep Blender > to_reparse
```
Или если нужен всего один серп или серпа не кроновые:
```bash
curl 'https://metrics.yandex-team.ru/api-ssc/serpset/info/?id=28931144' > to_reparse
```

Затем запускаем reparse:
```bash
cat to_reparse | ./metrics tool tp reparse
```
Команда выдает для получившихся задач ссылки на tp: `https://tp.yandex-team.ru/tp/metrics-serp-import/017492512764244771b2bd697d7d354e`.
Ждем пока все задачи выше сойдутся (час или два), затем формируем ссылку на новые:
```bash
./metrics tool cron info --cron-id 101071 --date-from 2020-03-21 --date-to 2020-03-24 | jq '.[] | {id, date, name, hostId, scraperId, cronSerpDownloadId}' -c | grep Blender > after_reparse
cat after_reparse | ./metrics tool cron deduplicate
```
Получаем ссылку на актуальные серпа - [пример](https://metrics.yandex-team.ru/mc/compare?serpset=26953219&serpset=26292208&serpset=26292205&serpset=26292194&serpset=26292191&serpset=26292189&serpset=26292170&serpset=26280859&serpset=26280749&serpset=26280744&serpset=26280574&serpset=26280558&serpset=26280448&serpset=26280161&serpset=26268465&serpset=26268263&serpset=26268172&serpset=26268146&serpset=26268118&serpset=26268104&serpset=26268075).
С ее помощью можно запустить дооценку.

Затем старые серпа можно удалить:
```bash
cat after_reparse | ./metrics tool cron deduplicate --remove-old
```

#### Поиск и обновление классических метрик
Манипуляции с метриками из [админки метрик](https://wiki.yandex-team.ru/JandeksPoisk/Metrics/new-metrics/).

Найти все метрики использующие модуль `video_proxima_z`
```bash
./metrics tool find metric --module video_proxima_z
```

Найти в каком аспекте есть метрика `ecom-assortment-dcg-5`
```bash
./metrics tool find aspect ecom-assortment-dcg-5
```

Задепрекейтить все метрики с `video_proxima-xp` в названии:
```bash
./metrics tool find metric --name video_proxima-xp | ./metrics tool update metric --deprecate
```

Обновить все метрики с модулем `has_video_words` до ревизии `7539938`:
```bash
./metrics tool find metric --module has_video_words | ./metrics tool update metric --revision 7539938
```

#### Поиск и обновление кронов
Получить json конфигурацию крона
```bash
./metrics tool cron get 102447 > cron.json
```

Обновить крон из полученной конфигурации
```bash
./metrics tool cron update < cron.json
```

Проставить runTtl всем мониторинговым кронам
```bash
./metrics tool cron filter --specification 016798019bd20000f6acd08dfe67f21d --owner robot-search-monitor --enabled | grep -v 101927 | grep -v 101660 | grep -v 102440 | ./metrics tool cron edit -c 'METRICS-7141: set runTtl to 40 minutes' --run-ttl PT40M
```

### CI/CD

На коммиты в [search/metrics/monitoring](https://a.yandex-team.ru/arc/trunk/arcadia/search/metrics/monitoring),
[search/scraper/parser_platform](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/parser_platform) и
[search/scraper/profile](https://a.yandex-team.ru/arc/trunk/arcadia/search/scraper/profile) запускается автоматическая сборка и развертывание артефакта.

Исполняемый файл заливается в директорию `//home/metrics/metrics_executable` с именем `metrics_yyyy-mm-dd`, на него ставится символическая ссылка `//home/metrics/metrics_executable/metrics`, предыдущей версии ставится TTL 3 дня.

* [//home/metrics/metrics_executable на Hahn](https://yt.yandex-team.ru/hahn/navigation?path=//home/metrics/metrics_executable)
* [//home/metrics/metrics_executable на Arnold](https://yt.yandex-team.ru/arnold/navigation?path=//home/metrics/metrics_executable)
* [search/metrics/monitoring/pkg.json](https://a.yandex-team.ru/arc/trunk/arcadia/search/metrics/monitoring/pkg.json)
* [sandbox/projects/metrics](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/metrics)
* [CI](https://a.yandex-team.ru/projects/metric/ci/actions/launches?dir=ci%2Fregistry%2Fprojects%2Ftestenv%2Fmetrics&id=metrics-binary-release-prod)

### Как обновить бинарь в проде вручную

Собираем артефакт:

```bash
ya make -r
```

Заливаем на YT:

```
cat metrics | yt write-file //home/qe/scraper/testing/metrics --executable --proxy hahn.yt.yandex-team.ru
cat metrics | yt write-file //home/qe/scraper/testing/metrics --executable --proxy arnold.yt.yandex-team.ru
```

Если не хватает прав, можно воспользоваться [токеном robot-scraper](https://wiki.yandex-team.ru/jandekspoisk/metrics/security/).

### Работа под Mac

Аркадийная сборка создает платформенно-зависимый артефакт. YT работает на Linux. Для сборки Linux-совместимого бинаря на рабочей станции под Mac OS нужно указать специальный ключ:

```bash
ya make --target-platform=linux -o linux_executable
```

Эта команда создаст по относительнму пути `linux_executable/search/metrics/monitoring/metrics` нужный артефакт. Его можно использовать в YT-версиях команд, передав путь к нему одним из следующих способов:

1. Ключ `--executable`, например:
    ```bash
    ./metrics parse yt --engine YandexImagesJSONParser \
   --scr //home/qe/scraper/production/serps-tables/5527/1582434045527 \
   --dst //home/metrics/images/2020-02-23-reparsed-over-yt-wip \
   --executable linux_executable/search/metrics/monitoring/metrics
    ```
2. Переменная окружения `METRICS_YT_EXECUTABLE_PATH`.
3. Файл `~/.metrics/executable_path`.

Ключ имеет высший приоритет, файл -- низший.

Не забывайте перекомпилировать Linux-совместимый артефакт!

Команды для обновления бинаря в проде:

```bash
cat linux_executable/search/metrics/monitoring/metrics | yt write-file //home/qe/scraper/testing/metrics --executable --proxy hahn.yt.yandex-team.ru
cat linux_executable/search/metrics/monitoring/metrics | yt write-file //home/qe/scraper/testing/metrics --executable --proxy arnold.yt.yandex-team.ru
```
