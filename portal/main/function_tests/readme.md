#### Настройка
Для запуска нужен virtualenv:
- osx: `pip install virtualenv`
- ubuntu: `sudo apt-get install python-virtualenv`

`make init` - создаст virtualenv, выкачает нужные зависимости, схемы для api_search_v2, добавит прекоммитные хуки

#### Настройка для красивого просмотра отчетов allure

`sudo apt-add-repository ppa:qameta/allure`

`sudo apt-get update`

`sudo apt-get install allure`

При запуске тестов с формированием отчетов, в консоли будет сформирована ссылка на локальнозапущенный allure, где можно всё смотреть более красиво.

#### Прекоммит хуки
Запуск прекоммит хуков для проверки
`
make pc
`

#### Как запускать
- `make t` - запуск теста
- `make tm` - запуск теста в режиме мониторинга с отправкой сигналов yasm
- `make ta`
- `make tl` - список тестов и параметров
- `make tar` - запуск теста, генерация отчета allure и откртие отчета

#### Быстрый запуск важных тестов в текущем инстансе
- `make t_stable` - запуск теста function-tests-stable
- `make t_api`    - запуск теста api-search-schema-tests
- `make t_simple` - запуск теста schema-tests-simple

#### Системные переменные для запуска тестов

- `MORDA_ENV=rc (production, v3d0.wdevx)` - окружение морды, в которое тесты должны ходить
- `N=10` - количество воркеров для запуска тестов
- `K=%str%` - фильтр для запуска тестов по названию
- `D=%str%` - фильтр для запуска тестов по каталогу и имени файла
- `FEATURES=a,b,c` - фильтр для запуска тестов по allure.feature
- `STORIES=a,b,c` - фильтр для запуска тестов по allure.story
- `DNS_MORDA=127.0.0.1` - все запросы в морду в окружении MORDA_ENV будут перенаправлены на этот ip
- `DNS_OVERRIDE=%regex%=%ip%,%regex2%=%ip2%` - запросы, которые матчатся на регулярки, будут перенаправлены на соответствующий адрес
- `RATE_LIMIT=10` - ограничение частоты запросов в секунду для HTTP-клиента


Пример запуска:

`N=10 FEATURES=any make tar`

`N=10 K=api_search_district make tar`

`N=10 D=tests/api_search/v2/test_api_search_stream.py make t`

#### Как запустить тесты вручную в одном потоке
`. venv/bin/activate`
`py.test $dir -k $testregex -s`

`-s` - разрешает stdout тестам

Примеры запуска:

`./venv/bin/py.test tests/config_pp/ -k test_check_schema -s --morda_env=production`

`./venv/bin/py.test tests/morda/blocks/afisha/test_afisha.py::TestAfishaDesktopMinsk -l -v -s --morda_env=rc`

`./venv/bin/py.test tests/morda/blocks/etrains/test_etrains.py -s --morda_env=v131d1.wdevx`

Примеры запуска тестов Коте:

`./venv/bin/py.test tests/kote/test_run_tests.py -s --tests_path=./tests/kote/tests/geo/ --morda_env=v131d1.wdevx`

`./venv/bin/py.test tests/kote/test_run_tests.py -s --tests_path=./tests/kote/tests/geo/test_new_tourist_morda_searchapp.yaml --morda_env=v131d1.wdevx`

Отключить варнинги:

`PYTHONWARNINGS="ignore:Unverified HTTPS request" ./venv/bin/py.test tests/morda/blocks/topnews/test_topnews.py -s --morda_env=v198d0.wdevx`
