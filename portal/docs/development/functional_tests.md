## Фрэймворк функциональных конфиг тестов - Котэ 😻
- Документация для слабаков, скорее покажи [примеры!](https://docs.yandex-team.ru/portal/development/functional_tests#primery-kote)
- Скорее попробуй [веб 🌎 интерфейс ](https://docs.yandex-team.ru/portal/development/functional_tests#veb-interfejs-kote-%F0%9F%8C%8E) Коте, ждем отзывов и фичреквестов!

### Запуск


Фрэймворк живет в function_tests/tests/kote/ [см. Arcanum](https://a.yandex-team.ru/arcadia/portal/main/function_tests/tests/kote).

Все тесты запускаются разом в файле ```test_run_tests.py```, его запускаем так же, как и обычные тесты.
```
./venv/bin/py.test tests/kote/test_run_tests.py -s --morda_env=v175d0.wdevx
```

Можно передавать параметр ```--tests_path``` для того, чтобы запустить отдельный тест или прогнать папку с тестами.

Пример запуска конкретного yaml файла:
```
./venv/bin/py.test tests/kote/test_run_tests.py -s --tests_path=./tests/kote/tests/api/search/2/topnews_extended/test_favorites_off_by_option.yaml --morda_env=v175d0.wdevx
```
Пример запуска конкретной папки:
```
./venv/bin/py.test tests/kote/test_run_tests.py -s --tests_path=./tests/kote/tests/api/search/2/topnews_extended/ --morda_env=v175d0.wdevx
```

Самотесты запускаются, если передать в --tests_path значение self_test:
```
./venv/bin/py.test tests/kote/test_run_tests.py -s --morda_env=v209d0.wdevx --tests_path=self_test
```

Можно передавать параметр ```--morda_env``` для того, чтобы тестировать на деве, по дефолту равен production, тесты запускаются на проде. Везде далее {env} - обозначение места, куда мы ходим.

Тесты представляют из себя yaml-документы, где прописано, куда и с какими параметрами мы ходим, то, что хотим получить + путь до схемы. 

{% note warning %}

Запускаются только тесты, название которых начинается с 'test', например, 'test_touch_topnews.yaml'. Самотесты, находящиеся в папке tests/framework_test/ автоматически не запускаются.

{% endnote %}

Посмотреть [пример](https://paste.yandex-team.ru/6225553)

### Блоки в конфиге

Ямл разделен на 5 блоков: `meta`, `config`, `get_params`, `result` и `schema`:

#### meta

* `meta` - блок, содержащий общую информацию о тесте. В блоке `meta` есть 2 обязательных поля: `task` и `desc`
    * `task` - номер таска
    * `desc` - описание тесткейса
    * `xfail` - при значении True тест начинает работать как xfail (проходит, если падает и наоборот)

#### config

* `config` - словарь, в котором указан клиент и parent (если он есть), поле `client` обязательно, можно создавать список клиентов(см. `get_params`), списком можно задать клиенты, домены и path для url-клиента.

    * ```client``` - куда идем:
        * ```api_search_android``` - ПП андроид идет в {env}yandex.ru/portal/api/search/2/?app_platform=android
        * ```api_search_ios``` - ПП ios идет в {env}yandex.ru/portal/api/search/2/?app_platform=iphone
        * ```ya_bro_android``` - ябро андроид идет в {env}yandex.ru/portal/api/yabrowser/2/?app_platform=android
        * ```ya_bro_ios``` - ябро ios идет в {env}yandex.ru/portal/api/yabrowser/2/?app_platform=iphone
        * ```ya_bro_ipad``` - ябро ios идет в {env}yandex.ru/portal/api/yabrowser/2/?app_platform=ipad
        * ```desktop``` - десктоп идет в {env}yandex.ru/
        * ```touch``` - тач идет в {env}yandex.ru/?content=touch
        * ```ntp``` - нтп идет в {env}yandex.ru/portal/ntp/refresh_data/
        * ```url``` - задает урл, идет вместе с параметром ```path``` вида ```*/``` идет в {env}yandex.ru/path/
        * ```mock``` - имитатор сетевого соединения. Запросы никуда не отправляются. Ожидаемый "ответ" считывается из файла, указанного в параметре ```name```. Используется для самотестов фреймворка. Данные в файле должны быть в формате json. 
    
    * ```request_body``` - тело POST-запроса. При наличии поля `request_body` запрос автоматически становится POST'ом. В этом поле должен находится JSON в синтаксисе YAML'а.
    * `parent` - путь до файла с шаблоном. Шаблон представляет из себя yaml с какими-то параметрами, которые мы заимствуем или переопределяем, сейчас если и в тесте, и в шаблоне есть одинаковые поля, берется поле из теста. Можно задать списком, тогда отработает следующая логика: второй файл в списке возьмет первый как шаблон, третий возьмет как шаблон то, что получилось, в конце сам тест возьмет как шаблон общий результат.

    * `domain` - top-level domain (ru, com, etc.), по которому отправляем запрос
    * `sldomain` - second-level domain (yandex, ya, etc.). По умолчанию используется "yandex"
    * `headers` - заголовки, добавляемые в HTTP запросы
    * `name` - имя файла с "ответом" для клиента ```mock```
    * `path` - путь для `url` клиента
    * `get_headers_only` - игнорировать тело ответа (если нужно проверить заголовки, а в теле не json).

Пример:

``` 
config:
    client: url
    path: portal/ntp/refresh_data/
    domain: ru
    headers:
        Y-Browser-Experiments: MSwyLDM7MiwzLDQ7OCw3LC0xOzY1NDcxMiwwLDk=
        User-Agent: 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.85 YaBrowser/21.11.3.954 (beta) Yowser/2.5 Safari/537.36'

Запрос пойдет по адресу https://{env}yandex.ru/portal/ntp/refresh_data/?get_param1=get_param1&get_param2=get_param2..
```

```
config:
  client: mock
  name: internal_checks
result:
  re:
    simple_match: [ RE, Test ]
    url: [ RE, 'http(s)?://(www.)?yandex.ru/tests' ]
    start_with: [ RE, '^Bingo' ]
    not_start_with: [ NOT, RE, '^Bingo' ]
    utf: [ RE, 'текст в utf8' ]
```
Запрос никуда не отправляется. Данные "ответа" считываются из файла [framework_test/mocks/internal_checks](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/mocks/internal_checks)

#### get_params

* `get_params` - словарь с гет-параметрами, параметры можно задавать списком (задается несколько значений параметров в [], тесты будут использовать все возможные комбинации параметров в списках)

{% note warning %}

Ознакомиться со списком возможных get параметров можно [здесь](https://wiki.yandex-team.ru/Morda/Get-parametry/). Наиболее полезными для тестов являются:
- ab_flags - форсирование флагов
- httpmock - подмена ответа ручек на моки
- madm_mocks - подмена экспортов на моки
- madm_options - форсирование опций из экспорта options
- cleanvars - вывод клинваров (веб) или сырых данных в raw_data (api)

{% endnote %}

Если есть необходимость создать запрос с несколькими гет-параметрами с одинаковыми именами, то нужно задать их списком списков, например запрос, содержащий параметры `srcskip=TOP_NEWS&srcskip=GREENBOX` задается в тесте как 
```
get_params:
    srcskip: [[TOP_NEWS, GREENBOX]]
```

Пример:
```
get_params:
    geo: [213, 193, 194]
    time: [12:12:12, 12:12:13, 12:12:14]
    ab_flags: flag1:flag2=1:flag3=flag4=1
```
Будут созданы 9 запросов со всеми возможными комбинациями параметров `geo` и `date`.

#### result

* ```result``` - ожидаемый ответ, может проверять на конкретное значение/тип/None:
  * ```IS_EMPTY``` - проверка на None
  * ```NOT_EMPTY``` - проверка на not None
  * ```IS_INT``` - проверка на int
  * ```IS_DICT``` - проверка на dict 
  * ```IS_ARRAY``` - проверка на list
  * ```IS_STRING``` - проверка на строку
  * ```IS_EXIST``` - проверка на наличие ключа
  * ```NOT_EXIST``` - проверка на отсутствие ключа

При других значениях проверяет на равенство. Может быть задан списком(в ```[]```), где первый элемент(`NOT`, `AND`, `OR`, `RE` или `CALLBACK`) соответствует логическому 'не', логическому 'и', логическому 'или', регулярному выражению или callback-функции соответственно. В этом случае ко всем проверкам применяется соответствующая операция.

Для численных типов можно использовать интервалы и операторы сравнения - нужно передать в значение ключа строку в формате 'a..b', где a и b - числа, тогда выполнится проверка на то, что a <= value >= b, или передать '>a' (вместо > могут быть <, <=, >=), a и b могут быть дробными, тогда отделяем дробную часть точкой.

В `result` лежат словари с такой же структурой, как в ответе запроса:
```
result:
    Mail:
        show: [NOT, 2, 3, 0, 4]
        processed: [OR, 1, 0]
        banner: IS_EMPTY
```

Заголовки ответа, в том числе заголовки `set-cookie`, лежат в словаре `HEADERS` ([пример](https://paste.yandex-team.ru/10663067)). Ключи этого словаря приведены к нижнему регистру. Если ключи совпадают, то новое значение добавляется к предыдущему через запятую в порядке их следования в ответе.

##### Ссылки

В качестве значения можно указать ссылку на поле из блока get_params. Пример:
```
config: 
    client: desktop
get_params:
    geo: 213
result:
    GeoID: '@geo'
```
Проверим, что у поля GeoID в ответе значение такое же, как у гет-параметра geo.

##### Логические выражения

Для проверки логических выражений нужно передать в список один из параметров NOT, AND или OR.

Например, нужно проверить, что элемент show не равен 0, 2, 3 или 4, тогда пишем:

`show: [NOT, 2, 3, 0, 4]`

Если нужно проверить, что show одновременно и int и равен 1(числу), то пишем:

`show: [AND, IS_INT, 1]`

Если нужно проверить, что processed равен или 1 или 0, то пишем:

`processed: [OR, 1, 0]`

Логические выражения могут быть большими и включать в себя проверку на пару ключ-значение и другие логические выражения, например выражение по типу:

`Stocks: [OR, value: IS_EXIST, [AND, value1: IS_EXIST, value2: IS_EXIST]]`

##### Регулярки

В result поддержаны регулярные выражения - нужно передать в список параметр RE

Примеры регулярных выражений RE:
```
config:
  client: mock
  name: internal_checks
result:
  re:
    simple_match: [ RE, Test ]
    url: [ RE, 'http(s)?://(www.)?yandex.ru/tests' ]
    start_with: [ RE, '^Bingo' ]
    not_start_with: [ NOT, RE, '^Bingo' ]
    utf: [ RE, 'текст в utf8' ]
    # RE в сложных условиях воспринимается как строка
    # combo: [ OR, 'a', 'b', [ RE, zen ], [ RE, core ] ]
```

##### CALLBACK

Поля из ответа можно передавать для проверки в сторонние функции. Для этого нужно передать в список параметр CALLBACK и имя функции, которой будем проверять ответ. Функция должна быть в файле kote/utils/kote_callback_functions.py. Функцию лучше называть в формате HOME_(номер задачи)_(что проверяет), чтобы не возникало конфликтов и путаницы. В функцию передается 2 аргумента: response(кусок ответа, который проверяем) и test_path(путь до файла с ямлом).

Например, мы хотим проверить ответ целиком, тогда нужно положить функцию в kote/utils/kote_callback_functions.py:
```
def HOME_0_example(response, test_path):
    assert isinstance(response, dict), 'Response is not dict\nFailed on test {}'.format(test_path) 
```
В самом тесте указываем, что проверяем весь ответ:
```
config:
    client: desktop
result: [CALLBACK, HOME_0_example]
```
Или, например, хотим проверить только какой-то кусок от ответа, тогда напишем что-то такое:
```
config:
    client: desktop
result:
    Mail: [CALLBACK, HOME_0_example]
```

#### schema

* `schema` - блок, в котором лежат схемы и все, что с ними связано

Корень пути для схемы - папка function_tests

Если хотим проверить весь ответ по схеме, то просто указываем путь до схемы, если хотим проверить конкретный блок(блоки), то передаем в блок словарь, повторяющий структуру ответа до нужного нам блока, например:
```
schema:
    Weather: path/to/weater/schema/weather.json
    Afisha:
        something: path/to/afisha/something/schema/something.json

или

schema: path/to/schema/schema.json
```
Сейчас нельзя проверить одновременно и весь ответ и отдельные блоки по схемам, добавлю позже, если понадобится такая возможность.


### Проверки массивов

Для проверки массивов введены служебные слова LENGTH, ITEM, FILTER и FILTERED_LENGTH.

- `LENGTH` - используется для проверки длины массива. Поддержаны операторы сравнения и интервалы.
- `FILTER` - задает условие для выбора элементов из массива, на которые будет распространяться действие ITEM. В условиях фильтра можно использовать все поддерживаемые котэ проверки.
- `ITEM` - обозначает каждый элемент массива, соответствующий заданному условию фильтра. Если фильтр не задан, для всех элементов массива.
- `FILTERED_LENGTH` - проверяет количество проверенных элементов. Например, если задан `FILTERED_LENGTH: 2`, то будет проверка на то, что было проверено ровно 2 элемента массива(полезно использовать в связке с FILTER). Если FILTERED_LENGTH не задан, то будет проверка на то, что был проверен хотя бы 1 элемент массива. Поддержаны операторы сравнения и интервалы.

Допустим, что нам нужно проверить массив block на то, что его длина всегда 5, а в каждом элементе есть ключ key со значением value, тогда можно использовать служебные слова ITEM и LENGTH:

```
block:
    LENGTH: 5
    ITEM:
        key: value
```

ITEM работает как цикл по всем элементам массива, то есть можно просто обращаться с ним как с индексом.

FILTER можно использовать, например, так:
```
config:
  client: mock
  name: internal_checks
result:
  filter:
    FILTER:
      f1: test1
      f2: f2
      f3: [ OR, 7, 8, 9 ]
    ITEM:
      message: ok
```

Мок internal_checks можно посмотреть [здесь](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/mocks/internal_checks)

Если нужна проверка на то, что ровно 1 элемент массива удовлетворяет условиям FILTER, то можно написать так:
```
array:
    FILTER:
        item_0: IS_INT
        item_1: IS_STRING
    FILTERED_LENGTH: 1
    ITEM:
        item_3: IS_EXIST
```

### Авторизация

Сейчас существует 2 способа авторизоваться в Котэ - воспользоваться готовыми авторизованными клиентами или гет-параметром `test_auth`.

#### Авторизованные клиенты

Это - предпочтительный способ. Для того, чтобы воспользоваться таким клиентом, нужно к названию клиента дописать `_oauth` или `_session_id` для авторизации по oauth-токену или session_id  соответственно. Например, нам нужно авторизоваться в тесте для пп на двух платформах, тогда блок config будет выглядить примерно следующим образом: 

```
config:
    client: [api_search_android_oauth, api_search_ios_oauth]
```

#### Гет-параметр test_auth

В случае, когда авторизованных клиентов почему-то не хватило для написания теста, можно пользоваться моком ответа блекбокса и гет-параметром test_auth. Для этого мок ответа блекбокса(то, что находится в data) нужно поместить в [папку с моками](https://a.yandex-team.ru/arc_vcs/portal/main/tests/data/http) и в самом тесте добавить гет-параметр test_auth со значением `'oauth_token@mock_name'` или `'session_id@mock_name'` в зависимости от того, какая авторизация нужна(oauth или session_id). Как пример - конфигурация одного из авторизованных клиентов:

```
config:
  parent: tests/kote/clients/touch.yaml
get_params:
  test_auth: 'oauth_token@blackbox_testing_1'
```

### Флаподав
Флаподав создан с целью бороться с флапающими тестами. Работает так же, как ретраи в старом фреймворке. Активируется, когда передается параметр `--retry_count=n`, где n - количество ретраев (по умолчанию, 0). В мейке прописан как RETRY_COUNT. 

### Сбор статистики с пулл-реквестов
Будет актуально, когда выедет этот [таск](https://st.yandex-team.ru/HOME-79625).

Сбор статистики включается при передачи параметра `--yt_collect=1` в фреймворке или `YT_COLLECT=1` в мейке. В таком случае, фреймворк начинает собирать флапнувшие (если передан параметр --retry_count или RETRY_COUNT) и упавшие тесты. Затем эти тесты отправляются в [yt](https://yt.yandex-team.ru/hahn/navigation?path=//home/morda/function_tests/rc_tests) и голован, отдельно [упавшие](https://yasm.yandex-team.ru/chart/signals=push-morda_kote_fails1_num_tttt;hosts=ASEARCH;itype=portal-yasm-proxy/) и [флапнувшие](https://yasm.yandex-team.ru/chart/signals=push-morda_kote_flaps_num_tttt;hosts=ASEARCH;itype=portal-yasm-proxy/). Скрипт, который за это отвечает, живет в kote/utils/yt_sender.py
 
## Примеры Котэ

{% note warning %}

Во всех примерах, использующих мок internal_checks, подразумевается файлик живущий [тут](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/mocks/internal_checks)

{% endnote %}


№1. [Отправляем запрос через клиент пп андроида без гет-параметров, проверяем на код 200](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_1.yaml)
```
config:
    client: api_search_android
```

№2. [Отправляем запрос через клиент десктопа с доменом ua, проверяем код 200](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_2.yaml)

```
config:
    client: desktop
    domain: ua
```

№3. [Отправляем запросы через разные клиенты с разными доменами(всего 6 запросов)](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_3.yaml)

```
config:
    client: [desktop, touch]
    domain: [ru, ua, by]
```

В `[]` можно задать несколько значений, тогда на все возможные комбинации параметров будет отправлен запрос

№4. [Отправляем запросы в произвольный путь через url-клиент](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_4.yaml)

```
config:
    client: url
    path: "portal/api/search/2/?geo=213"
```

№5. [Запросы через url-клиент, но сложнее](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_5.yaml)

```
config:
    client: url
    path: ['portal/ntp/refresh_data/?ab_flags=yabro_newtgo_exp', '?ab_flags=focus_search&cleanvars=1']
```
Кавычки нужны потому что yaml ругается некоторые символы. Отправятся всего 6 запросов: 3 в нпт, 3 в десктоп.

№6. [Запросы с гет-параметрами geo](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_6.yaml)

```
config:
    client: desktop
    domain: [ru, ua, by]
get_params:
    geo: [213, 2, 225]
```
№7. [Запросы с наборами гет-параметров(geo и какие-то аб-флаги)](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_7.yaml)

```
config:
    client: desktop
get_params:
    ab_flags: ['covid_block', 'covid_speed', 'covid_block:covid_speed']
    geo: [213, 2, 225]
```
№8. [Мокать МАДМ тоже можно](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_8.yaml) (см [доку](https://docs.yandex-team.ru/portal/development/functional_tests#moki-madm))

```
config:
    client: desktop
get_params:
    madm_mocks: 'div_fullscreens=div_fullscreens_mock_1:shortcuts_settings_v2=shortcuts_settings_v2_mock_1'
```

№9. [Проверяем ответ](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_9.yaml)

```
config:
    client: ya_bro_ios
get_params:
    geo_country: 213
result:
    pages:
      0:
        title: 'Дзен'
        type: 'zen'
    api_version: '2'
```
pages - массив, обращаемся по индексу как к словарям

№10. [Проверяем ответ на типы](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_10.yaml)

```
config:
    client: ya_bro_ios
get_params:
    geo: [213, 2, 225]
result:
    block: IS_ARRAY
    geo_country: IS_INT
    lang: IS_STRING
```

№11. [Проверяем какие-то поля на типы, какие-то на значения](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_11.yaml)

```
config:
    client: desktop
    domain: [ru, ua, by]
get_params:
    cleanvars: weather
    geo: [213, 2]
result:
    Weather:
        show: 1
        t1: NOT_EMPTY
        t2: IS_STRING
        t2name: IS_STRING
    Weather_map: IS_DICT
```

№12. [Проверяем ответ на значения + проверяем схему](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_12.yaml)

```
config:
    client: desktop
    domain: [ru, by]
get_params:
    ab_flags: ab_flag
    cleanvars: weather
    geo: [213, 2]
result:
    Weather_map:
        show: 1
        time: IS_INT
        GenTime: IS_INT
schema:
    Weather: schema/cleanvars/weather/desktop/weather.json
```

№13. [Проверяем ответ и на значения и на схему, только сложнее](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_13.yaml)

```
config:
    client: desktop
    domain: [ru, ua, by]
get_params:
    cleanvars: weather
    geo: [213, 2]
result:
    Weather:
        show: [OR, 1, "1"]
        t1: IS_STRING
        t2: IS_STRING
        t3: IS_STRING
    Weather_map:
        show: 1
        time: IS_INT
        GenTime: IS_INT
schema:
    Weather: schema/cleanvars/weather/desktop/weather.json
```

№14. Пример использования шаблона

[Файлик-шаблон(parent_test):](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/parent_test_example_14.yaml)

```
config: 
    domain: [ru, ua, by]
get_params:
    geo: [213, 2, 225]
```

[Сам тест:](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_14_1.yaml)
```
config: 
    client: desktop
    parent: tests/kote/tests/framework_test/examples/parent_test_example_14.yaml
get_params:
    ab_flags: ab_flag
```

Тест "забирает" поля из parent_test_example_14, теперь [пример](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_14_2.yaml), где мы переопределяем эти поля:

```
config: 
    client: desktop
    parent: tests/kote/tests/framework_test/examples/parent_test_example_14.yaml
get_params:
    ab_flags: ab_flag
    geo: 213
```
Теперь в итоговом тесте мы будем отправлять запрос только с одним geo.

№15. [Логические выражения](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_15.yaml)

```
config: 
    client: desktop
get_params:
    cleanvars: weather
result:
    Weather:
        show: [OR, 0, 1]
        processed: [NOT, 0]
```
№16. [Множественное наследование](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_16.yaml)
```
config:
  parent: ['tests/kote/tests/framework_test/examples/test_example_14_2.yaml', 'tests/kote/tests/framework_test/examples/parent_test_example_14.yaml']
```
Сначала второй файл наследует от первого, затем сам тест наследуется от результата, работает как обычное наследование, но несколько раз.

№17. [Использование ITEM](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_17.yaml)
```
config:
  client: api_search_ios
result:
  block:
    ITEM: 
      data: IS_DICT
```

№18. [Использование LENGTH](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_18.yaml)
```
config:
  client: desktop
result:
  blocks_layout:
    LENGTH: 2
```

№19. [Большое логическое выражение вместе с ITEM](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_19.yaml)
```
config:
  client: desktop
get_params:
  geo: 213
result:
  AfishaInserts:
    events:
      ITEM: [AND, event_id: IS_STRING, type: IS_STRING, [OR, genre: IS_INT, name: IS_STRING]]
```

Проверяем, что все элементы массива events содержат ключи event_id и type + их значения - строки + проверяем, что каждый элемент массива содержит или ключ genre(число) или ключ name(строка).

№20. [mock-клиент и регулярки](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/examples/test_example_20.yaml)
```
config:
  client: mock
  path: internal_checks
result:
  example20:
    array:
      LENGTH: "<2"
      0:
        inner_array:
          FILTER:
            regular_string1: [RE, "^Regular e*"]
          ITEM:
            regular_string2: "Another regular expression"
```
Сначала проверяем, что длина массива array меньше двух, затем, при проверке массива inner_array, указываем, что нас интересуют только те элементы, в которых ключ regular_string1 соответствует регулярному выраженю, а уже в таких элементах проверяем ключ regular_string2. 

№21. [Callback-функция](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/tests/framework_test/test_callback.yaml)
```
config:
  client: mock
  path: internal_checks
result: [CALLBACK, HOME_77872_callback_example]
```
Функция живет [тут](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/tests/kote/utils/kote_callback_functions.py)
```
def HOME_77872_callback_example(response, test_path):
    assert response['logic']['int'] == 1, 'Failed on callback function HOME_77872_callback_example\nFailed on test {}'.format(test_path)
```

## Фичреквесты Котэ

{% cut "Как написать фичреквест так, чтобы поняли" %}

Пожалуйста, постарайтесь писать фичреквесты как можно более подробно. В идеале - пример синтаксиса, объяснение, что он делает, можно сделать пасту или писать сразу здесь. Пример:

Логика для IS_EXIST и NOT_EXIST
```
result:
    key: [OR, [AND, key1: IS_EXIST, key2: IS_EXIST], [AND, key3: IS_EXIST, key4: IS_EXIST]]
```
Проверит, что существует одна из пар ключей (key1, key2) или (key3, key4)

{% endcut %}

### Фичреквесты странички

1. Красный текст для падающих тестов*
2. Короткая ссылка, чтобы можно было зафиксировать и отправить параметры текущего запуска (тело теста + мок полей + окружение). Кейс - набрал тест, нужно им поделиться в мессенджере (по аналогии с расшариванием запроса в yt).

### Фичреквесты фреймворка

1. Проверка количества ключей для хэшей
2. b2b тесты
3. Проверка массивов без учета порядка элементов
4. Проверка HTTP параметров ответов: заголовков и cookie в частности, кодов ответа, времени ответа
5. Макросы для регулярных выражений. Например, DOMAIN, URL, DATE, TIMESTAMP, DATETIME и т.д.
6. Поддержка цепочек контейнеров для элементов: base64, json, plain text, protobuf. Может пригодиться, например, для проверки содержимого heavy_req (вложенный json), заголовков с идентификаторами тестов (в base64), данных из вершины в protobuf, текста AS IS с параметром subreqs=1 без for_apphost
7. Несколько тесткейсов в одном файле yaml
8. inline наследование
9. Логика для IS_EXIST и NOT_EXIST
    ```
    result:
        key: [OR, [AND, key1: IS_EXIST, key2: IS_EXIST], [AND, key3: IS_EXIST, key4: IS_EXIST]]
    ```
    Проверит, что существует одна из пар ключей (key1, key2) или (key3, key4)

10. Сделать автоматическую проверку на устаревание экспортов
11. Прикрутить секретницу
12. !Перегруппировать тесты по фичам а не по платформам
13. Показать в логах таск из блока meta ^^
14. Уметь доставать из заголовка ответа X-Yandex-Req-Id или X-Requestid идентификатор запроса и использовать его для получения логов из ручек:
    - /test/errorlog/?Requestid=%requesid
    - /portal/front/errorlog/?Requestid=%requesid
15. Уметь совершать последовательные запросы в одном тесте. Например, для url-клиента указывать массив path. Так же можно подумать над увключением последовательных запросов указанием гет-параметров в массивах одинаковой длины, сейчас в таком случае происходит умножение параметров, что скорее всего бесполезно и не используется.
 
    с последующим анализом логов на предмет наличия ошибок/варнингов

## Веб интерфейс Коте 🌎
На любом инстансе любого дева уже есть веб интерфейс Коте.
Расположен в ```/test/kote```, например, [https://v175d1.wdevx.yandex.ru/test/kote](https://v175d1.wdevx.yandex.ru/test/kote)

{% note warning %}

Если вместо результата тестов возникают ошибки вида ```Unable to open ../function_tests/tests/kote/tests/framework_test/mocks/tmp/mock_file_28.06.2022_19:43:18.022709.json``` или другие, нужно в папке ```function_tests```  инстанса сделать ```make kote_fix```. Это даст доступы страничке на запись в нужные директории. Если не помогло, попробуйте ```sudo chmod -R 777```. Если проблема так и не ушла, пишите [alexeybabenko@](https://staff.yandex-team.ru/alexeybabenko).

{% endnote %}

![](https://jing.yandex-team.ru/files/alexeybabenko/Screenshot%20from%202022-06-28%2019-25-55.png)

Что сейчас в нем можно сделать:
- Написать тест в поле Test field.
- Запустить, нацелив на любой дев, прод или рц.
- Посмотреть прошел тест или нет, логи в поле Result.
- Искать и открывать файлы с тестами на текущем инстансе дева.
- Сымитировать ответ тестируемой ручки в поле Mock field. Для этого в поле Test field достаточно только указать result, клиенты и прочие параметры не нужны. Этот режим хорошо подходит для тех, кто хочет попрактиковаться в написании тестов.

Чего-то не хватает или можно улучшить - пишите [сюда!](https://docs.yandex-team.ru/portal/development/functional_tests#fichrekvesty-stranichki)



## Функциональные тесты

{% note warning %}

При написании новых тестов или исправлении старых **обязательно** добавляйте в ```@allure.feature``` фичу ```'function_tests_stable'```

{% endnote %}

Функциональные тесты живут в папке ```function_tests``` [см. в GitHub](https://github.yandex-team.ru/morda/main/tree/dev/function_tests).

Инструкция по инициализации и запуску есть в той же директории в файле [readme.md](https://github.yandex-team.ru/morda/main/blob/dev/function_tests/readme.md).

Основные 3 теста, на которые мы сейчас смотрим:
* [function-tests-stable](https://teamcity.yandex-team.ru/buildConfiguration/PortalMorda_TestsFunctional_FunctionTestsStable?mode=builds) - стабильные тесты, написанные вручную ```feature=function_tests_stable```
* [api-search-schema-tests](https://teamcity.yandex-team.ru/buildConfiguration/PortalMorda_TestsFunctional_ApiSearchSchemaTests?mode=builds) -  схема тесты ПП и Ябро, написанные вручную с проставлнной ```feature=api_search_v2```
* [schema-tests-simple](https://teamcity.yandex-team.ru/buildConfiguration/PortalMorda_TestsFunctional_SchemaTestsSimple?mode=builds) - схема тесты ПП и Ябро, добавляются автоматически при выходе новых версий приложений. Живут в ```function_tests/tests/schema```

Можно локально запустить каждых из этих трех тестов для текущего инстанса, используя следующие команды в папке ```function_tests/```:
* ```make t_stable``` - запуск теста function-tests-stable
* ```make t_api``` - запуск теста api-search-schema-tests
* ```make t_simple``` - запуск теста schema-tests-simple

*[Инструкция дополняется]*

## Схемы для функцинальных тестов

[Репозиторий схем](https://github.yandex-team.ru/portal/morda-schema)

Как открыть доступ к репозиторию:
1. На гитхабе добавить пользователя, которому нужен доступ в группу [Autotests Home](https://github.yandex-team.ru/portal)
2. Дать пользователю роль "Owner"
    1. Во вкладке "People" найти нужного пользователя
    2. В настройках справа от имени пользователя выбрать "Change role"
    3. Выбрать "Owner"
    4. Это откроет доступ ко всем реозиториям, в том числе к morda-schema

## Моки МАДМ

Моки делались в [этом таске](https://st.yandex-team.ru/HOME-72980).


{% note warning %}

Сейчас моки работают для всех экспортов, кроме options. Их будем задавать как get параметр, по аналогии с ab_flags. Таск на это: https://st.yandex-team.ru/HOME-76272

{% endnote %}

Основная задача моков - повысить стабильность функциональных тестов. Экспорты в МАДМ часто изменяются, с помощью моков же можно сохранить необходимое состояние экспорта (например, на момент написания теста) и использовать именно его, указывая это через get параметры запроса.

* В экспортах в МАДМ появилась кнопка MOCK рядом с GET.
По нажатию на нее скачивается файл с данными экспорта в формате json, который можно использовать как мок.
![](https://jing.yandex-team.ru/files/alexeybabenko/Screenshot%20from%202021-11-15%2013-14-35.png)

* Моки кладутся в папку ```tests/data/madm``` [см. в Arcanum](https://a.yandex-team.ru/arcadia/portal/main/tests/data/madm)
* В запросе добавляется cgi параметр madm_mocks.

{% note warning %}

Имя файла мока задаётся без расширения!

{% endnote %}

В примере ниже для экспорта ```<export_name_1>``` применяем мок ```<mock_name_1>.json``` из папки ```tests/data/madm``` и т.д.
```
Схема:
madm_mocks=<export_name_1>=<mock_name_1>:<export_name_2>=<mock_name_2>:<export_name_n>=<mock_name_n>
Пример:
https://yandex.ru/?madm_mocks=bell=bell_example
```

* Если по каким-то причинам не удалось загрузить мок из запроса, в ответе появляется поле ```madm_mock_error``` с текстом ошибки. При этом остальные моки не применяются.

* Если формат экспорта изменился, например, добавились новые поля, мы так же получим в ответе ```madm_mock_error``` с соответствующим сообщением. Моки при этом тоже не применятся. В этом случае необходимо сделать новый мок и пересохранить его вместо устаревшего.

{% note warning %}

При написании тестов с моками проверяйте ответ морды на наличие ```madm_mock_error```. Если оно пришло, то:
* тест не должен проходить
* строка из ```madm_mock_error``` должна выводиться в логах упавшего теста, чтобы понимать, что именно произошло

```madm_mock_error``` сейчас поддержан в десктопе, таче и ручке api, для других ручек нужны аналогичные доработки в перле (пару строк).

{% endnote %}
