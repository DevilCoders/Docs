# Tap Config
Тестируйте фронтенд yaml-конфигом.
Запускает тесты [в TAP-парадигме](https://testanything.org/).

Инструмент позволяет быстро создавать автотесты для сценариев использования приложения (use cases).
Для этого просто опишите сценарий в yaml-формате. Пример простого yaml сценария:
  ```
options:
  width: 800
  height: 600
  # url to the selenium server
  selenium_hub_url: http://127.0.0.1:4444/wd/hub
  timeout: 10
  base_url: http://nginx

tests:
  - get_ok:
      url: base.html
  - click_ok: css:button#to-click
  - log: Clicked
  - has: [/html/body/div, Has common html.]
```

# Оглавление
- [Оглавление](#оглавление)
- [Гайд](#гайд)
  - [Системные требования](#системные-требования)
  - [Установка](#установка)
  - [Запускаем простой тест](#запускаем-простой-тест)
  - [Браузеры](#браузеры)
  - [CLI](#cli)
  - [Основы](#основы)
    - [Виды записи тестов](#виды-записи-тестов)
  - [Параллельные тесты](#параллельные-тесты)
  - [Глобальные опции](#глобальные-опции)
    - [Список опций](#список-опций)
    - [Варианты опций](#варианты-опций)
  - [Переменные окружения](#переменные-окружения)
  - [Утилиты](#утилиты)
    - [Wait](#wait)
    - [Import](#import)
  - [Активные тесты (плагины)](#активные-тесты-плагины)
    - [clear_ok](#clear_ok)
    - [click_ok](#click_ok)
    - [exec_js](#exec_js)
    - [fill_ok](#fill_ok)
    - [focus_ok](#focus_ok)
    - [get_ok](#get_ok)
    - [hover_ok](#hover_ok)
    - [size_ok](#size_ok)
    - [set_window_ok](#set_window_ok)
  - [Пассивные тесты (плагины)](#пассивные-тесты-плагины)
    - [clickable](#clickable)
    - [visible](#visible)
    - [eq](#eq)
    - [ne](#ne)
    - [has](#has)
    - [hasnt](#hasnt)
    - [is](#is)
    - [isnt](#isnt)
    - [like](#like)
    - [unlike](#unlike)
    - [log](#log)
    - [print_log](#print_log)
    - [ok](#ok)
    - [url](#url)
    - [wait](#wait-1)
    - [sleep](#sleep)
    - [count](#count)
    - [run](#run)
    - [print](#print)
  - [Для разработчиков](#для-разработчиков)
    - [Как работает dataset](#как-работает-dataset)
  - [Общие поля для плагинов](#общие-поля-для-плагинов)
    - [xpath / css](#xpath--css)
    - [description](#description)
  - [Ожидание в тестах](#ожидание-в-тестах)
    - [Ожидание пассивного после активного](#ожидание-пассивного-после-активного)
  - [Подводные камни](#подводные-камни)
    - [Ожидание url](#ожидание-url)

# Гайд

## Системные требования
Для работы тестов нужны python >=3.7 и запущенный selenium server.

Selenium server можно запустить с помощью докера. Докер-образ selenium server для нужного браузера
[есть на docker hub](https://hub.docker.com/u/selenium).
Примеры запуска selenium server через докер:
[из официального репозитория](https://github.com/SeleniumHQ/docker-selenium#selenium-grid-hub-and-nodes),
[из нашего проекта](https://github.yandex-team.ru/andrew-zak/pahtest/blob/master/docker-compose.yml).

## Установка
Устанавливаем pahtest
```
pip3 install pahtest
```

Предварительно укажите pip-репозиторий Яндекса в [pip config файле](https://pip.pypa.io/en/stable/user_guide/#config-file)
```
[global]
timeout = 60
index-url = https://pypi.yandex-team.ru/repo/default
```

Проверяем установку
```
pahtest -V
```

## Запускаем простой тест
Для работы библиотеки нужен selenium remote webdriver.
Самый простой способ - запустить selenium remote через него. Рассмотрим его ниже.

Создаём файл `docker-compose.yml` со следующим содержимым:
```
version: '3'

services:
  selenium:
    image: selenium/standalone-chrome:3.141.59
    restart: always
    ports:
      - 4444:4444
    environment:
      - DBUS_SESSION_BUS_ADDRESS=/dev/null
    networks:
      - selenium
```

Создаём файл yaml файл с тестами.
```
# form.yml

options:
  width: 800
  height: 600
  browser: chrome
  selenium_hub_url: http://127.0.0.1:4444/wd/hub
  timeout: 10.0
  base_url: https://ya.ru

tests:
  - get_ok: [/, Загружаем главную страницу поиска.]
  - has: [css:form, Страница поиска содержит форму.]
```
Обратите внимание на опцию "selenium_hub_url". В примере у неё корректное значение для docker-compose конфига выше.

Запускаем команду:
```
$ pahtest form.yml
ok 1 - Загружаем главную страницу поиска.
ok 2 - Страница поиска содержит форму.
```


Пример [для конфигурации](https://github.yandex-team.ru/andrew-zak/pahtest/blob/master/docker-compose.yml) из репозитория pahtest.
```
# button.yml

options:
  width: 800
  height: 600
  browser: chrome
  # url to the selenium server
  selenium_hub_url: http://127.0.0.1:4450/wd/hub
  timeout: 20
  base_url: https://ya.ru

tests:
  - get_ok:
      url: base.html
  - click_ok: css:button
  - url:
      like: search
      desc: Went to the search page
```

## Браузеры
Рассмотрим пример одновременной поддержки браузеров
через официальные докер-репозитории standalone image selenium_hub_url.
1. Кладём конфиг докер-сервисов для браузеров в docker-compose.yml
```
# docker-compose.yml
version: '3.6'

services:
  chrome:
    image: selenium/standalone-chrome-debug:3.141.59
    restart: always
    ports:
      - 4445:4444
      # VNC port. Password: secret
      - 5901:5900
    environment:
      - DBUS_SESSION_BUS_ADDRESS=/dev/null
    networks:
      - selenium
    # https://github.com/SeleniumHQ/docker-selenium#running-the-images
    shm_size: 3G

  firefox:
    image: selenium/standalone-firefox-debug:3.141.59
    restart: always
    ports:
      - 4446:4444
      # VNC port. Password: secret
      - 5902:5900
    environment:
      - DBUS_SESSION_BUS_ADDRESS=/dev/null
    networks:
      - selenium
    # https://github.com/SeleniumHQ/docker-selenium#running-the-images
    shm_size: 3G
```

2. Запускаем контейнеры с браузерами
```
docker-compose up -d
```

3. Создаём файл с тестами `run.yml`
```
# run.yml
options:
  timeout: 5
  base_url: https://ya.ru
  list:
    - browser: chrome
      selenium_hub_url: http://127.0.0.1:4445/wd/hub
    - browser: firefox
      selenium_hub_url: http://127.0.0.1:4446/wd/hub

tests:
  - get_ok: /
  - has: css:form
```

4. Запускаем тесты
```
pahtest run.yml
```
Если видим успешно пройденные тесты, значит браузеры подключены правильно
```
1..2  # run.yml
  1..2  # chrome 800x600
  ok 1 - Get page from browser
  ok 2 - Check if page contains locator
ok 1 - chrome 800x600
  1..2  # firefox 800x600
  ok 1 - Get page from browser
  ok 2 - Check if page contains locator
ok 2 - firefox 800x600
```

## CLI
Тесты можно запускать с помощью консольной утилиты
```
pahtest path/to/my.yaml

> ok 1 - Первый тест из my.yaml.
> ok 2 - Второй тест из my.yaml.
```

Через опции консольной утилиты `pahtest` можно переопределить глобальные опции yaml конфига
(см секцию "Глобальные опции").

Для подобностей смотрите `pahtest --help`.

**Папка** тоже может быть аргументом.
Утилита запустит переданные папку как тест.
Содержимое папки утилита запустит как сабтесты.
```
$ tree folder/
folder/
├── first.yaml
└── second
    ├── fourth
    │   └── fifth.yml
    └── third.yml

$ pahtest folder/
1..1  # first.yaml
  1..2  # first chrome 800x600
  ok 1 - Get "/"
  ok 2 - Has form
ok 1 - first chrome 800x600

1..2  # folder/second
  1..1  # folder/second/fourth
    1..1  # fifth.yml
      1..2  # fifth chrome 800x600
      ok 1 - Get "/"
      ok 2 - Has form
    ok 1 - fifth chrome 800x600
  ok 1 - fifth.yml
ok 1 - folder/second/fourth
  1..1  # third.yml
    1..2  # third chrome 800x600
    ok 1 - Get "/"
    ok 2 - Has form
  ok 1 - third chrome 800x600
ok 1 - third.yml
```

Можно передавать **несколько аргументов**,
тогда они выполнятся в порядке следования в аргументах
```
pahtest first.yml second/ third.yml
```

## Параллельные тесты

Опцией `-j, --jobs` можно задать количество параллельных тасков для исполнения тестов. Подробнее про саму опцию [Список опций](#список-опций).

Параллельно испольняются только тесты-папки, и только из первого уровня вложенности

```
$ tree pahtests
├── one
│   ├── 01-first.yml
│   └── 02-second.yml
├── three
│   ├── 01-first.yml
│   └── 02-second.yml
└── two
    ├── 01-first.yml
    └── 02-second.yml
$ pahtest --jobs 4 pahtests
```

В примере параллельно запустятся тесты-папки one, two, three.
Тесты-файлы внутри папок будут идти последовательно.

```
$ tree pahtests/one
├── 01-first.yml
└── 02-second.yml
$ pahtest --jobs 4 pahtests/one
```

А здесь файлы внутри папки one запустятся последовательно, опция `--jobs` будет проигнорирована.

## Основы

Конфиг состоит из трёх основных секций: обязательные options и tests.
И необязательный skip. Подробнее о skip см раздел "список опций".

Секция options содержит общие для каждого теста настройки.
Секция tests - сами тесты.
```
options:
  browser: chrome
  selenium_hub_url: http://127.0.0.1:4444/wd/hub
  ...

tests:
   - get_ok: ...
   - has: ...
   - click_ok: ...
```

Тесты выполняются по следующим правилам:
- тесты всегда выполняются последовательно;
- в случае ошибки одного теста все следующие ему тоже выполняются;
- результат выполнения тестов выводится [в формате tap](https://testanything.org/).
- если не пройден хотя бы один тест, pahtest отдаёт ненулевой код возврата.

Тесты бывают двух видов:
- Активные тесты - те что меняют состояние страницы в браузере.
- Пассивные тесты - не меняют состояние.

*Заметка*

Будьте осторожны с css-селекторами в квадратных скобках
```
Ошибка: yaml воспримет квадратные скобки как список
- has:
    css: [href="http://ya.ru"]

Правильно: содержимое строки является css селектором
- has:
    css: '[href="http://ya.ru"]'
```

### Виды записи тестов
Один тест можно записать в нескольких нотациях.

**Короткая форма**
```
tests:
  - get_ok [https://ya.ru, Main search page.]
```

**Полная форма**
```
tests:
  - get_ok:
      url: https://ya.ru
      desc: Main search page.
```

**Полная плоская форма**
```
tests:
  - test: get_ok
    url: https://ya.ru
    desc: Main search page.
```

## Глобальные опции
Рассмотрим здесь секцию `options`.

### Список опций
`width`, `height`. Стандартные значения `800, 600`. Размеры страницы браузера в пикселях.

`maximize (bool, default: False)` - разворачиваем окно браузера на весь рабочий стол. Если включена, опции width и height игнорируются.

`devtools (bool, default: False)` - автоматически открываем devtools при старте вкладки браузера. Работает только с Chrome.

`browser` - одно из значений `chrome | firefox`. Браузер, в котором будут выполняться тесты.

`base_url`. url для тестируемой страницы.
Является базовым относительных урлов в тестах загрузки страницы.
Если base_url содержит get-параметры, они автоматически передаются в плагин get_ok.

`selenium_hub_url`. url для selenium remote webdriver.

`timeout`. Стандартное значение `20.0`, тип float. Стандартное время ожидания в секундах.
Тесты используют его если нету своего. Может быть нулевым.

`waiting_step`. Стандартное значение `0.2`, тип float. Время между шагами проверки при ожидании.

`-j, --jobs`. Стандартное значение `1`.
Количество процессов для параллельного запуска.
Один из процессов - это мастер-процесс.
Остальные - воркеры, они исполняют сами тесты.
[Параллельные тесты](#параллельные-тесты).

`skip`. Пропустить тест, если аргументом идёт
[truth value](https://docs.python.org/3/library/stdtypes.html#truth-value-testing) значение.

`list`. Список [вариантов опций](#варианты-опций).

`screenshots`. Настраивает скриншоты.
- `dir`. Директория на локальной машине, в которую будут записываться скриншоты.
- `before` - одно из значений `none | all | fail`. Определяет будут ли сохраняться скриншоты перед запуском теста.
  - `none` - скриншоты не будут сохраняться;
  - `all` - всегда будут сохраняться;
  - `fail` - будут сохраняться только для упавших тестов. (TODO - сейчас сохраняются для всех)
- `after` - одно из значений `none | all | fail`. Смысл каждой опции аналогичен `before`.

#### commands
`commands`. Описывает команды для запуска через плагин [run](#run).
Пример использования см в плагине.

[Подробнее про нутро](#как-работает-dataset) command+run (dataset).

Spec
- `<command>` - любой yaml-ключ, описывает команду.
  - `code` - код запуска команды, например "echo 'hello'"
  - `workdir` - директория запуска команды. Относительна директории запуска тестов.
  - `format` - строка или словарь с ключами: `input`, `output`.
    Правила значений `format/input/output` одинаковы.
    - `input` - то же, что и строковый вариант для "format"
    - `output` - то же, что и строковый вариант для "format"
    - строка формата. Строка может иметь одно из значений: `none, sh, json, yaml`
      - `none` - нет input'а для команды.
      - `sh` - передаёт input/output как есть, простой строкой
      - `json` - кастует input/output в/из json
      - `yaml` - кастует input/output в/из yaml


### Варианты опций
Если через список `list` указать варианты опций, весь набор тестов запустися один раз для каждого варианта.
Поля вариантов переопределяют поля самой секции options.

Пример:
```
options:
  timeout: 5
  base_url: https://ya.ru
  browser: chrome
  list:
    - selenium_hub_url: http://127.0.0.1:4445/wd/hub
    - browser: firefox  # redifines options.browser value
      selenium_hub_url: http://127.0.0.1:4446/wd/hub

tests:
  - get_ok: /
  - has: css:form

# output
1..2
  1..2  # var 1 / chrome 800x600
  ok 1 - Get page from browser
  ok 2 - Check if page contains locator
ok 1 - var 1 / chrome 800x600
  1..2  # var 2 / firefox 800x600
  ok 1 - Get page from browser
  ok 2 - Check if page contains locator
ok 2 - var 2 / firefox 800x600
```

## Переменные окружения
Опции можно задавать через переменные окружения
```
options:
  base_url: env:SITE_URL:http://default.com

tests:
  - get_ok: base.html
  - url: base.html
```

`http://default.com` в примере - стандартное значение.
Оно подставится если переменная окружения SITE_URL не задана или пустая.

## Утилиты

Утилита - функция, которая переиспользуется множеством плагинов.

### Wait

Для wait также реализован отдельный плагин.

У утилиты wait две разных нотации для активных тестов. И одна - для пассивных:
```
tests:
  - get_ok:
      url: https://ya.ru
      wait:  # длинная нотация для активного теста
        timeout: 10
        description: Wait untils page has body
        tests:
          - has: xpath:/html/body
          - has: css:button.button
  - get_ok:
      # NOTE: не реализовано
      wait:  # короткая нотация для активного теста
        - has: xpath:/html/body
        - has: css:button.button
  - has:  # нотация для короткого теста
      xpath: /html/body
      timeout: 10.0  # секунды float типа
  - has:  # нотация для короткого теста
      css: button.button
      timeout: 5.0  # таймаут будет проигнорирован, так как это второй тест после активного
```

Обе нотации для активных тестов содержат сабтесты. Эти сабтесты могут быть только пассивными.
Активные тесты внутри wait'а приведут к ошибке.

Обратите внимание что короткая нотация для активных тестов не содержит описания.
Секция wait возьмёт его у своего первого сабтеста.


#### Справочник для опции wait
**Длинная нотация для активных тестов**
- description - необязательный параметр
- timeout - необязательный, тип: число с плавающей точкой или строка "default".
  Если опция пуста или имеет значение "default", применится значение из options.timeout.
- tests - обязательный. Имеет ту же нотацию что и глобальная секция tests, но с одним исключением:
  *секция wait может содержать только пассивные сабтесты*.

**Короткая нотация для активных тестов**
Тело секции - список сабтестов. См выше опцию tests.
Если у нотации нет описания, она будет взята из первого сабтеста.

**Нотация для пассивного теста**
Принимает одно значение для таймаута. См выше опцию timeout.


### Import
Позволяет включить файл внутрь существующего.

Нотация:
- `import: <file_path>`. file_path - путь до импортируемого yml-файла.
Путь должен быть относителен текущему файлу или директории запуска теста.
- `import: <file_path>` - file_path аналогичен import.

При импорте инструкция `import` заменится на содержимое импортируемого файла.

Примеры
```
# Файл base.yml
options:
  base_url: https://ya.ru
  browser: chrome
  import: options.yml

tests:
  - get_ok: /
  - wait:
      - has: /html/body
  - import: tests.yml
  - has: css:button.button

# Файл options.yml
width: 800
height: 600

# Файл tests.yml
- has: css:.button
- has: /html/body

# Результат импорта
options:
  base_url: https://ya.ru
  browser: chrome
  width: 800  # imported
  height: 600  # imported

tests:
  - get_ok: /
  - wait:
      - has: /html/body
  - has: css:.button  # imported
  - has: /html/body   # imported
  - has: css:button.button
```

#### Особенности импорта
Рассмотрим некоторые неочевидные особенности импорта.

1. Импорт **переопределяет значения** в порядке следования значений.
Следующие значения перезаписывают предыдущие
Переопределяет:
```
# base.yml
options:
  browser: safary
  import: options.yml

# options.yml
browser: chrome

# import result
options:
  browser: chrome
```

Не переопределяет:
```
# base.yml
options:
  import: options.yml
  browser: safary

# options.yml
browser: chrome

# import result
options:
  browser: safary
```

2. Импорт списка в список игнорирует соседние ключи

В примере ниже ключ "some_key" пропадает после импорта
```
# base.yml
tests:
  - get_ok: /
  - import: tests.yml
    some_key: will be thrown

# tests.yml
- has: css:.button
- has: /html/body

# import result
tests:
  - get_ok: /
  - has: css:.button   # no "some_key" there
  - has: /html/body
```


## Активные тесты (плагины)
Активный тест - любой, что может повлиять на результат исполнения
других тестов. Большинство активных тестов отмечены суффиксом *_ok*,
но есть и исключения, например *exec_js*.

### clear_ok
Активный тест. Очищает поля по переданному списку селекторов.

**Полная форма**
- **fields** (обязательное) список \<input selector>'ов
- **description (desc)** (необязательное, тип: текст) - описание.

**Короткая форма**
Состоит из списка \<input selector>'ов

**\<input selector>**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.

**Примеры**
```
options:
  base_url: https://ya.ru

tests:
  - get_ok: /

  # короткая форма
  - exec_js: "$(input#first).val('Some text')"
  - like: [css:input#first, Some text.]
  - clear_ok:
    - css: input#first
    - css: input#second
  - unlike: [css:input#first, Some text.]

  # полная форма
  - exec_js: "$(input#first).val('Some text')"
  - like: [css:input#first, Some text.]
  - clear_ok:
      desc: First / second
      fields:
        - css: input#first
          value: just fill
        - css: input#second
          value: 123
  - unlike: [css:input#first, Some text.]
```

### click_ok
Активный тест. Делает клик на элемент. До клика может заполнить указанные поля.
Клик на некликабельный элемент не приводит к ошибке.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **description (desc)** (необязательное, тип: текст) - описание
- **fill** - список в формате селектор + значение для ввода. См примеры.
Для заполнения есть отдельный тест [fill_ok](#fill_ok).

**Примеры**
```
options:
  base_url: https://ya.ru

tests:
  - get_ok: /
  # короткая форма с xpath селектором
  - click_ok: //button[contains(@class, "button")]

  - sleep: 1
  - get_ok: /
  - wait:
    - clickable: css:button
  # короткая форма с css селектором
  - click_ok: css:button

  - sleep: 1
  - get_ok: /
  - wait:
    - clickable: ['//button[contains(@class, "button")]', Click to button]
  # короткая форма с описанием
  - click_ok: ['//button[contains(@class, "button")]', Click to button]

  - sleep: 1
  - get_ok: /
  - wait:
    - clickable: //*[contains(@class, "button")]
  # полная форма
  - click_ok:
      xpath: //*[contains(@class, "button")]
      description: Click to button

  - sleep: 1
  - get_ok: /
  - wait:
    - xpath: //*[contains(@class, "button")]
  # заполняем и отправляем форму
  - click_ok:
      fill:
        - css: input#text
          value: Foo
      xpath: //*[contains(@class, "button")]
```

### exec_js
Активный тест.
Выполняет в контексте документа код javascript, переданный строковым аргументом.

**Поля**
- **script** (обязательное) - текст javascript кода.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok: /

  # короткая форма
  - exec_js: "console.log('Hello')"
  - log: Hello

  # полная форма
  - exec_js:
      script: "console.log('Hello')"
      desc: Log hello.
  - log: Hello
```

### fill_ok
Активный тест. Заполняет поля по переданному списку формата селектор+значение.
Pah-тест [click_ok](#click_ok) содержит свою опцию заполнения полей.

**Полная форма**
- **fields** (обязательное) список \<form input>'ов
- **description (desc)** (необязательное, тип: текст) - описание.

**Короткая форма**
Состоит из списка \<form input>'ов

**\<form input>**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **value** (обязательное, тип: текст или число) - значение для заполнения.
- **gap** (необязательно, тип: float) - время в секундах для ожидания
  перед вводом каждого символа

**Примеры**
```
options:
  base_url: https://ya.ru

tests:
  - get_ok: /

  # короткая форма
  - fill_ok:
    - xpath: //input[contains(@id, "text")]
      value: just fill
    - css: input#text
      value: 123

  # полная форма
  - fill_ok:
      desc: First and second
      fields:
        - css: input#first
          value: just fill
        - css: input#second
          value: 123

  # заполняем с gap'ом
  - fill_ok:
    - xpath: //input[contains(@id, "text")]
      value: just fill
      gap: 0.1
    - css: input#text
      value: 123
      gap: 0.1

```

### focus_ok
Активный тест. Делает фокус на элемент с переданным селектором.
Фокус на нефокусируемый элемент не приводит к ошибке.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok: /
  # короткая форма с xpath
  - focus_ok: //*[contains(@class, "button")]

  - sleep: 1
  - get_ok: /
  # короткая форма с css
  - focus_ok: css:button.button

  - sleep: 1
  - get_ok: /
  # короткая форма с описанием
  - focus_ok: ['//*[contains(@class, "button")]', Focus to some button.]

  - sleep: 1
  - get_ok: /
  # полная форма с xpath
  - focus_ok:
      xpath: //*[contains(@class, "button")]
      description: Focus to some button.

  - sleep: 1
  - get_ok: /
  # полная форма с css
  - focus_ok:
      css: button.button
      description: Focus to some button.

  - sleep: 1
  - get_ok: /
  # фокус на нефокусируемый элемент не приводит к ошибке
  - focus_ok: css:tr
```

### get_ok
Активный тест. Загружает страницу по заданному url.
http://nginx/test/
**Поля**
- **url** (обязательное, тип: текст) - абсолютный или относительный url (path).
Абсолютный: `http://example.com/my/path`. Относительный (path): `/my/path`.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  # абсолютный url
  - get_ok: https://ya.ru
  - url:
      is: https://ya.ru

  # относительный url (path)
  - get_ok: /
  - url:
      is: https://ya.ru

  # короткая форма без описания
  - get_ok: /

  # короткая форма с описанием
  - get_ok: [/, Базовая страница.]

  # полная форма
  - get_ok:
      url: /
      description: Базовая страница.
```

Рассмотрим отдельно пример с get-параметрами в опции base_url.
Параметр url в тесте get_ok автоматически получает get-параметры опции base_url, если они есть.
Если у get_ok.url собственные get-параметры, get-параметры base_url не учитываются.
```
options:
  # ...
  base_url: https://ya.ru?one=1&two=2

tests:
  - get_ok: /
  - wait:
      - has: /html/body/table
  - url:
      is: https://ya.ru/?one=1&two=2

  - get_ok: https://ya.ru?three=3
  - wait:
      - has: /html/body/table
  - url:
      is: https://ya.ru/?three=3
```


### hover_ok
Активный тест. Размещает курсор над элементом с переданным селектором.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok: /

  # короткая форма с xpath
  - hover_ok: //button[contains(@class, "button")]

  # короткая форма с css
  - hover_ok: css:button.button

  # короткая форма с описанием
  - hover_ok: ['//input[contains(@id, "text")]', Focus to some button.]

  # полная форма с xpath
  - hover_ok:
      xpath: //button[contains(@class, "button")]
      description: Focus to some button.

  # полная форма с css
  - hover_ok:
      css: button.button
      description: Focus to some button.
```

### size_ok
Активный тест. Изменяет размер окна браузера на заданные ширину и высоту.

**Поля**
- **width** (обязательное, тип: int) - натуральное число от 1 до 2**20-1.
- **height** (обязательное, тип: int) - натуральное число от 1 до 2**20-1.
- **description (desc)** (необязательное, тип: текст) - описание.

Короткая форма: `[<width>, <height>]`.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /

  # короткая форма
  - size_ok: [800, 600]

  # полная форма
  - size_ok:
      width: 800
      height: 600

  # полная форма с description
  - size_ok:
      width: 800
      height: 600
      description: Small screen.
```

### set_window_ok
Активный тест. Устанавливает фокус на окне с переданным индексом.
xpath/css селекторы всегда указывают в окно с текущим фокусом.

**Поля**
- **index** (обязательное, значения: first или last) - индекс текущего окна.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /

  - set_window_ok: first  # single window is the first

  - set_window_ok: last  # single window is the last

  - exec_js: "window.open('/window.html', 'new window')"
  - set_window_ok: last  # spawned window is the last
  - eq: [/html/body/h1, Spawned H1]  # checks h1 in the spawned window
  - set_window_ok: first  # main window is the first
  - eq: [/html/body/h1, Main H1]  # checks h1 in the main window

  # полная форма
  - set_window_ok:
      index: first
      desc: Switch to the main window.
```

## Пассивные тесты (плагины)
Пассивный тест - любой что не меняет DOM.

### clickable
Пассивный тест. Проверяет кликабельность элемента.
[По w3c-стандарту](https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event) любой элемент в браузере кликабелен. Но при загрузке страницы есть промежуток времени, когда элемент уже есть в DOM, но ещё не кликабелен.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **description (desc)** (необязательное, тип: текст) - описание.
- **timeout** (необязательное, тип: float) - таймаут ожидания

Короткая форма: `[<xpath|css>, <desc|description>, <timeout>]`.
**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /

  # ожидаем кликабельности элемента
  - wait:
    - clickable: '//*[@class="button__text"]'
```

### visible
Пассивный тест. Проверяет отображение элемента.
Возвращает успех, если все элементы с заданным селектором отображены (visible).

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **description (desc)** (необязательное, тип: текст) - описание.
- **timeout** (необязательное, тип: float) - таймаут ожидания

Короткая форма: `[<xpath|css>, <desc|description>, <timeout>]`.
**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /

  # ожидаем кликабельности элемента
  - wait:
    - visible: '//*[@class="button__text"]'
```

### eq
Пассивный тест. Проверяет равен ли выбранный по селектору элемент переданному значению.
При сравнении обрезает пробелы по алгоритму описанному ниже.
Для строгого сравнения используйте тест [is](#is).

#### Алгоритм сравнения
Для значения элемента из браузера и для переданного значения
все пробельные символы в начале и в конце строки обрезаются.
Все подряд идущие пробельные символы внутри строки приводятся к одному пробелу.
См примеры для подробностей.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **attr / attribute** (необязательное) - атрибут элемента с искомым значением
- **value** (обязательное, тип: текст или число) - значение для проверки.

Короткая форма: `[<xpath|css>, <attr|attrubute>, <value>]`.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /

  # значение из элемента по селектору слева сравниваем с переданным значением справа
  - eq: [/html/body/table, Some table.]

  # для сравнения пробелы обрезаются. Это сравнение тождественно предыдущему
  - eq: [/html/body/table, '  Some table.']

  # пробельные символы в середине строки приводятся к одному пробелу.
  # Это сравнение тождественно предыдущему.
  - eq: [/html/body/table, 'Some table.  	 Some table.']

  # пример с css-селектором
  - eq: [css:table, Some table.]

  # у тега input атрибут id равен "text"
  - eq:
      css: input.input__input
      attr: id
      value: text
```

### ne
Пассивный тест. Полностью повторяет тест [eq](#eq),
но накладывает логическое отрицание на результат.

### has
Пассивный тест. Проверяет содержит ли страница браузера элемент с переданным селектором.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok: /

  # короткая форма с xpath
  - has: /html/body/table

  # короткая форма с css
  - has: css:input#text

  # короткая форма с описанием
  - has: [/html/body/table, Has some div.]

  # полная форма с xpath
  - has:
      xpath: /html/body/table
      description: Has some div.

  # полная форма с css
  - has:
      css: input#text
      description: Has some text.
```

### hasnt
Пассивный тест. Проверяет отсутствие на странице элемента с переданным селектором.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok: /

  # Короткая форма
  - hasnt: /not/existing/path

  # Длинная форма
  - hasnt:
      css: div > .not-existing
      description: Long form
```

### is
Пассивный тест. Проверяет равен ли выбранный по селектору элемент переданному значению.
Проверяет точное совпадение и не обрезает пробелы [в отличие от eq](#eq).

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **attr / attribute** (необязательное) - атрибут элемента с искомым значением
- **value** (обязательное, тип: текст или число) - значение для проверки.

Имеет только короткую форму.

Короткая форма: `[<xpath|css>, <attr|attrubute>, <value>]`.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /

  # значение из элемента по селектору слева сравниваем с переданным значением справа
  - is: ['//*[@class="button__text"]', Найти]

  # пример с css-селектором
  - is: [css:.button__text, Найти]

  # у тега input атрибут id равен "text"
  - is:
      css: input.input__input
      attr: id
      value: text
```

### isnt
Пассивный тест. Полностью повторяет тест [is](#is),
но накладывает логическое отрицание на результат.

### like
Пассивный тест. Проверяет содержит ли выбранный элемент
переданное текстовое значение или паттерн регулярного выражения.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **text** (обязательное или re, тип: текст) - искомое в тексте элемента браузера значение.
- **re** (обязательное или text, тип: текст) - искомый паттерн регулярного выражения.
Используется [ситаксис регулярных выражений](https://docs.python.org/3/library/re.html#regular-expression-syntax)
из стандартной библиотеки Python.

Для короткой формы нотация такая: `[<(xpath | css)>, <like>, <description>]`

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok: /

  # короткая форма с xpath. Делает like по строке "Find me"
  - like: ['//*[@class="button__text"]', Най]

  # короткая форма с css. Делает like по строке "Find me"
  - like: [css:span.button__text, Най]

  # короткая форма с описанием. Делает like по строке "Find me"
  - like: ['//*[@class="button__text"]', Най, Has some text.]

  # полная форма с xpath и like
  - like:
      xpath: //*[@class="button__text"]
      text: Най
      description: Focus to some button.

  # полная форма с css и like
  - like:
      css: span.button__text
      text: Найти

  # полная форма с xpath и re
  - like:
      css: span.button__text
      re: \w
```

### unlike
Пассивный тест. Полностью повторяет тест [like](#like),
но накладывает логическое отрицание на результат.

### log
Пассивный тест. Проверяет содержит ли страница браузера лог
с вхождением переданного сообщения. Перед проверкой лог предварительно фильтруется по переданному уровню.

Лог страницы в браузере очищается после каждого вызова теста log.
Тем не менее мы считаем log пассивным тестом - он не меняет состояние самой страницы.

**Внимание**. Плагин не поддерживает браузер Firefox
из-за [особенностей](https://github.com/mozilla/geckodriver/issues/330) драйвера Gecko.

**Поля**
- **level** (необязательное, тип: строка, по умолчанию "INFO") - уровень нотификации лога (log level).
Поддерживаются такие уровни лога (по убыванию приоритета): `SEVERE, WARNING, INFO, DEBUG`.
like/unlike работает только для логов с переданным и меньшим приоритетами.
Например для level=WARNING тест проверит like для всех логов со статусами SEVERE или WARNING.
Переданная в level строка тест приводит к заглавным буквам.
- **like** (обязательное или [или unlike](#xpath-/-css), тип: текст) - искомое в тексте элемента браузера значение.
- **unlike** (обязательное или [или like](#xpath-/-css), тип: текст) - like с логическим отрицанием на результат.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**
```
options:
  # ...
  base_url: http://example.com

tests:
  - get_ok: base.html

  - click_ok: css:#to-click
  # короткая форма
  - log: Clicked

  - click_ok: css:#to-click
  # короткая форма с фильтром по уровню
  - log: debug:Clicked

  - click_ok: css:#to-click
  # короткая форма с описанием
  - log: [Clicked, Has some div.]

  - click_ok: css:#to-click
  # короткая форма с фильтром по уровню и описанием
  - log: [debug:Clicked, Has some div.]

  - click_ok: css:#to-click
  # полная форма с уровнем лога. log применится для всех записей лога с SEVERE И WARNING
  - log:
      level: warning
      log: Something broken

  - click_ok: css:#to-click
  # полная форма с описанием. Значение level пропущено и по умолчанию равно INFO.
  - log:
      like: Clicked
      description: Button is clicked

  - click_ok: css:#to-click
  # полная форма с unlike
  - log:
      unlike: Clicked
```

### print_log
Пассивный тест. Печатает лог браузера.

Лог страницы в браузере очищается после каждого вызова плагина.
Тем не менее мы считаем log пассивным тестом - он не меняет состояние самой страницы.

**Внимание**. Плагин не поддерживает браузер Firefox
из-за [особенностей](https://github.com/mozilla/geckodriver/issues/330) драйвера Gecko.

**Поля**
- **level** (необязательное, тип: строка, по умолчанию "INFO") - уровень нотификации лога (log level).
Поддерживаются такие уровни лога (по убыванию приоритета): `SEVERE, WARNING, INFO, DEBUG`.
like/unlike работает только для логов с переданным и меньшим приоритетами.
Например для level=WARNING тест проверит like для всех логов со статусами SEVERE или WARNING.
Переданная в level строка тест приводит к заглавным буквам.
- **description (desc)** (необязательное, тип: текст) - описание.

**Примеры**

Код
```
options:
  # ...
  base_url: http://example.com

tests:
  - get_ok: base.html

  - click_ok: css:button#to-click
  - print_log:
      level: debug

  - click_ok: css:button#to-click
  - print_log: debug

  - print_log:
      level: debug

  - click_ok: css:button#to-click
  - print_log:
      level: warning
```

Результат
```
1..8  # print_log chrome 800x600
ok 1 - Get "base.html"
ok 2 - Click on button#to-click
ok 3 - Print browser log
# http://nginx/base.html 17:12 "Window is ready"
# http://nginx/favicon.ico - Failed to load resource: the server responded with a status of 404 (Not Found)
# http://nginx/base.html 46:121 "Clicked"
ok 4 - Click on button#to-click
ok 5 - Print browser log
# http://nginx/base.html 46:121 "Clicked"
ok 6 - Print browser log
# Log is empty
ok 7 - Click on button#to-click
ok 8 - Print browser log
# Log is empty
1..8
```

### ok
Пассивный тест. Заглушка для разработки и изучения утилиты pahtest.
Принимает любые поля в длинной и короткой форме. И не обратывает их, за исключением полей condition и description.

**Поля**
- **condition** (необязательное, тип: boolean, по умолчанию: True) - итоговый статус теста.
Для False тест будет считаться непройденным и утилита вернёт ненулевой код возврата.
- **description (desc)** (необязательное, тип: текст) - описание.
- **<any>** - принимает любые другие поля без обработки.

Короткая форма: `[<condition>, <description>]`.

**Примеры**
```
options:
  # ...
  base_url: http://relative.example.com

tests:
  # короткая форма с condition
  - ok: True

  # короткая форма с condition и description
  - ok: [True, Some ok test.]

  # короткая форма с condition, description и произвольным набором полей
  - ok: [True, Some ok test., One two, 12, False]

  # полная форма
  - ok:
      condition: True
      description: Some ok test.

  # полная форма с condition False. Весь набор тестов вернёт ненулевой код возврата.
  - ok:
      condition: False

  # полная форма с произвольным набором полей
  - ok:
      condition: False
      description: Some ok test.
      name: One two
      surname: 12
      good_guy: False
```

### url
Пассивный тест. Проверяет содержит ли текущая страница url или его элемент.

*Замечание*

При проверке тест игнорирует последний слэш ("/"). Например `http://example.com/`
перед проверкой приводится к `http://example.com`

**Поля**
- **like** (обязательное или [или is](#xpath-/-css), тип: текст) - искомое в url страницы значение.
- **is** (обязательное или [или like](#xpath-/-css), тип: текст) -
значение для сравнения с url страницы. Тест успешен если значение равно url'у страницы.
- **description (desc)** (необязательное, тип: текст) - искомое в тексте элемента браузера значение.

Нотация для короткой формы: `[<(like | is)>, <description>]`

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok: /

  # короткая форма
  - url: ya

  # короткая форма с описанием
  - url: [ya, Check base url.]

  # полная форма
  - url:
      like: ya
      description: Check base url.

  # полная форма c is
  - url:
      is: https://ya.ru
```

### wait
Для wait также реализована [утилита](#утилиты).

```
options:
  # ...
  base_url: https://ya.ru
  timeout: 10

tests:
  - get_ok: /
  - wait:
      - has: xpath://*[@class="button__text"]
      - has: css:input#text
```

Нотация в точности такая же,
[как сокращённая](https://github.yandex-team.ru/andrew-zak/pahtest#short-wait-notation-for-active-test)
для утилиты wait.

### sleep
Пассивный тест. Выполнение тестов останавливается на переданное количество секунд.
Страница браузера при этом продолжает работать.

**Поля**
- **timeout** (обязательное, тип: float) - таймаут засыпания
- **description (desc)** (необязательное, тип: текст) - искомое в тексте элемента браузера значение.

Только короткая форма.

**Примеры**
```
options:
  # ...
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /
  - sleep: 1.0
  - has: /html/body/table
```

### count
Пассивный тест. Считает количество элементов с переданным селектором
и сравнивает его с переданным числом для сравнения.

**Поля**
- **xpath** (обязательное [или css](#xpath-/-css), тип: текст) - xpath до искомого элемента.
- **css** (обязательное или [или xpath](#xpath-/-css), тип: текст) - css-селектор до искомого элемента.
- **value** (обязательное, тип: натуральное число или 0) - ожидаемое кол-во элементов.
- **description (desc)** (необязательное, тип: текст) - описание.

Только короткая форма.

**Примеры**
```
options:
  base_url: https://ya.ru

tests:
  - get_ok:
      url: /

  # Короткая форма
  - count: [/html/body/table, 1]

  # Короткая форма с описанием
  - count: [/html/body/table, 1, With description.]

  # Несуществующий элемент
  - count: [/html/body/not-existing, 0]

  # Длинная форма
  - count:
      css: button.button
      value: 1
      description: With desctiption.
```

### run
Пассивный тест. Запускает команду. На уровне плагина можно установить аргументы для команды.
Результаты выполнения можно сохранить в хранилище "dataset". Хранилище является глобальным на уровне файла тестов.
Команда должна быть предварительно описана в опциях в секции [commands](#commands).

[Подробнее про нутро](#как-работает-dataset) command+run (dataset).

**Поля**
- **command** (необязательное, тип: текст, по умолчанию: "default") -
команда-ключ из секции опций [commands](#commands).
- **args** (необязательное, тип: yaml) - любой yaml, который передастся команде в зависимости от формата.
- **as** (необязательное*, тип: текст) - json path. Должен быть задан или здесь или в опциях в секции commands.
Плагин положит результат работы команды в dataset по этому пути.
Если в dataset по этому пути будут данные, плагин их перезапишет.
Если пути не существует, запуск плагина упадёт с ошибкой.

- **description (desc)** (необязательное, тип: текст) - описание.

Только длинная форма.

**Примеры**
```
options:
  commands:
    echo_form:
      code: echo 'form'
      format:
        input: none
        output: sh
    redirect_json:
      code: tee /dev/null
      format:
        input: json
        output: json

tests:
  - get_ok: ya.ru

  # команда echo сохраняет результат своей работы, строку 'form',
  # по json пути echo.result.
  # Плагин has читает echo.result с помощью префикса dataset.
  - run:
      command: echo_form
      as: echo.result
  - has:
      css: dataset:echo.result:not-existing

  # обращаемся в структуру данных dataset по json path
  - run:
      command: redirect_json
      args:
        one:
          - two
          - three: form
      as: redirect.result
  - has:
      css: dataset:redirect.result.one.1.three:not-existing
```

### print
Пассивный тест. Выводит в tap-коммент переданное значение.
Полезно для строк, значение которых изменяется при запуске тестов.
Например для строк с префиксами `env:` и `dataset:`

**Поля**
- **value** (обязательное [или css](#xpath-/-css), тип: текст) - значение для вывода.
- **description (desc)** (необязательное, тип: текст) - описание.

Только короткая форма.

**Примеры**
```
options:
  commands:
    echo_form:
      code: echo 'my string'
      format:
        input: none
        output: sh

tests:
  - print: plain value
  - run:
      command: echo_form
      as: echo.result
  - print: dataset:echo.result:not-existing
  - print: dataset:echo.wrong:not-existing


# OUTPUT:
1..4  # doc chrome 800x600
ok 1 - Print
# plain value
ok 2 - Run echo_form
ok 3 - Print
# my string
ok 4 - Print
# not-existing
```

- [Для разработчиков](#для-разработчиков)
  - [Как работает dataset](#как-работает-dataset)
## Для разработчиков

### Как работает dataset
Или command+run

Разберём на примере что делает приложение с command+run

```
options:
  ...
  commands:
    redirect_json:
      code: tee /dev/null
      format:
        input: json
        output: json
  ...

tests:
  ...
  - run:
      command: redirect_json
      args:
        one:
          - two
          - three: form
      as: redirect.result
  ...
```

Кратко. Исполняется эта команда
```
echo '{["one": "two", "three": "form"]}' | tee /dev/null
```

Подробно. Шаги исполнения
* Доходит очередь до теста run, он исполняется
* Смотрим в ключ `command: redirect_json`
* Идём в секцию `commands`, находим там подсекцию `redirect_json`
* Исполняем команду из `redirect_json.code`
* Передаём в неё `run.args` как json через linux pipe
  * `format.input == json`, поэтому передаём аргументы как json
* Команда отрабатывает, возвращает json,
  *  потому как `format.output == json`
* Забираем json output через linux pipe
* Сериализуем его в объект `run.as: redirect.result`
* В объекте `redirect.result` итоговые данные
  * Получаем к ним доступ в последующих тестах через json_path


## Общие поля для плагинов
Подробно опишем самые часто встречающиеся поля.

### xpath / css
Каждое из полей явлется селектором, то есть выбирает элемент.
Поэтому строго одно из них обязательно для любого теста, который использует селектор.

```
  # верно - строго один селектор
  - get_ok:
      xpath: /html/body/div

  # верно - сторого один селектор
  - get_ok:
      css: button#to-click

  # не верно - не одного селектора
  - get_ok:
      description: Just get page

  # не верно - два селектора
  - get_ok:
      xpath: /html/body/div
      css: button#to-click
```

Некоторые другие поля обладают схожим поведением: like/re, like/unlike и тд.

### description
Описание теста. Оно отобразится в tap-выводе. Поле всегда необязательно.
Если не задано, будет использовано стандартное описание теста.


## Ожидание в тестах
Для ожидания у нас есть [утилита wait](#wait) и [плагин wait](#wait-1).

### Ожидание пассивного после активного
Первый пассивный тест после активного ждёт успеха максимум timeout секунд. Timeout можно указать в самом тесте.
Если не указан, берётся стандартный из секции options. Пассивный тест,
который идет после другого пассивного, никогда не ждет, даже если таймаут указан.

Пример:
```
options:
  timeout: 15

tests:
  - get_ok: ya.ru
  - has: /html/body/div  # ждёт до 15 сек до появления div'а
  - has: input  # не ждёт
```

Код выше эквивалентен этому:
```
options:
  timeout: 15

tests:
  - get_ok: ya.ru
  - wait:
    - has: /html/body/div  # ждёт до 15 сек до появления div'а
  - has: input  # не ждёт
```

Пример с явно указанными полями timeout:
```
options:
  timeout: 15

tests:
  - get_ok: ya.ru
  - has:
      xpath: /html/body/div  # ждёт до 15 сек до появления div'а
      timeout: 10  # # ждёт до 10 сек до появления div'а
  - has:
      xpath: input
      timeout: 20    # не ждёт, парметр timeout игнорируется, так как предыдущий тест пассивный
```

## Подводные камни

### Ожидание url
Тесты такого вида будут флапать:
```
# wrong example
tests:
  - get_ok: /some/url
  - wait:
    - url: /some/url
  - has: 'css:.some-element'
```

Дело в том, что после действия (активного теста) url в браузере меняется до рендера DOM'а.
Поэтому на момент поиска элемента по has сам элемент может ещё не быть в браузере.
Тест будет то проходить, то нет. Это зависит от мощности и загрузки машины.

```
# correct example
tests:
  - get_ok: /some/url
  - wait:
    - url: /some/url
    - has: 'css:.some-element'
```
