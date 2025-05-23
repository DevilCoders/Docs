# Code linters

### Установка
#### Ubuntu
Для того, чтобы в системе появились/обновились утилиты из этого пакета, надо поставить/обновить
пакет [taxi-deps-py3-2](https://github.yandex-team.ru/taxi/deps-py3/blob/develop/README.md).
```
sudo apt install taxi-deps-py3-2
```

#### MacOS и системы, отличные от Ubuntu
Для установки пакета, можно использовать pip в virtualenv:
```
pip install -i https://pypi.yandex-team.ru/simple/ yandex-taxi-code-linters
```

Для обновления пакета, используйте:
```
pip install --upgrade -i https://pypi.yandex-team.ru/simple/ yandex-taxi-code-linters
```

### Форматтеры
* `taxi-black` - форматтер для python кода
* `taxi-clang-format` - форматтер для c++ кода
* `taxi-eolfmt` - форматтер подстановки \n в конце файлов
* `taxi-jsonfmt` - форматтер для json
* `taxi-initfmt` - форматтер добавления \_\_init__.py для избежания ошибки mypy
* `taxi-yamlfmt` - форматтер для yaml
* `taxi-format` - запуск всех форматтеров (для запуска определнных форматтеров, 
можно использовать опциональный аргумент `-F`, например `taxi-format -F black yamlfmt -- .`)

Особенности использования можно посмотреть через `taxi-<fmt> --help`

Утилитами можно форматировать файлы и директории: `taxi-<fmt> <directory1> <directory2>` 
(код в сабмодулях (относительно переданного на проверку пути) не форматируется)

Для настройки утилит `taxi-<fmt>` можно использовать файл `services.yaml`
в секции `linters/<fmt>`. Допустимые опции:
* `disable-paths-wildcards`: список путей/wildcards, форматирование которых надо по 
  тем или иным причинам игнорировать (для black будет актуально после https://st.yandex-team.ru/TAXITOOLS-2139)


### Функции для работы с объектами
Функции призваны помочь разработчикам форматировать yaml/json/py/cpp/hpp объекты из кода.
Чтобы использовать функции, нужно импортировать соответствующий модуль josnfmt / yamlfmt / black / clang_format:
`from taxi_linters import taxi_<fmt>`

##### black:
* `format_str` – функция принимает на вход строку c python кодом и возвращает отформатированную строку

##### clang-format:
* `format_str` – функция принимает на вход строку c c++ кодом и возвращает отформатированную строку

##### json:
* `load` - функция принимает на вход handle файла c JSON и возвращает Python объект (аналог json.load)
* `loads` – функция принимает на вход строку c JSON и возвращает Python объект (аналог json.loads)
* `dump` – функция записывает переданный на вход Python объект в файловый дескриптор (аналог json.dump)
* `dumps` – функция принимает на вход Python объект и возвращает отформатированную JSON строку
(аналог json.dumps)
* `format_file` – функция принимает на вход файл с JSON (os.PathLike) и форматирует его
* `format_str` – функция принимает на вход JSON строку и возвращает отформатированную JSON строку

##### yaml:
Подробнее об объектах с возможностью редактирования комментариев можно ознакомиться в 
[документации](https://yaml.readthedocs.io/en/latest/detail.html#adding-replacing-comments).
Для возможности изменять комментарии в YAML документах, загружайте документы с помощью taxi_yamlfmt.load*
* `load` - функция принимает на вход handle файла c YAML или YAML строку
и возвращает YAML объект (есть поддержка редактирования комментариев)
* `load_all` – функция принимает на вход handle файла c YAML или YAML строку, содержащие несколько документов, 
и возвращает YAML объект (есть поддержка редактирования комментариев)
* `dump` - функция записывает переданный на вход Python объект в файловый дескриптор. Если дескриптор не был передан,
возвращает YAML строку (аналог yaml.dump). Параметр sort_keys поможет сохранить YAML объект 
c рекурсивно отсортированными ключами словарей, но при этом есть опасность смещения комментариев.
* `dump_all` - функция записывает переданный на вход YAML объект, содержащий несколько документов,в файловый дескриптор. 
Если дескриптор не был передан, возвращает YAML строку. Параметр sort_keys поможет сохранить YAML объект 
c рекурсивно отсортированными ключами словарей, но при этом есть опасность смещения комментариев.
* `format_file` – функция принимает на вход файл с YAML (os.PathLike) и форматирует его
* `format_str` – функция принимает на вход YAML строку и возвращает отформатированную YAML строку


### Как включить линтеры python в PyCharm/CLion
Для CLion надо установить плагин **File Watchers** (в PyCharm он есть из 
коробки). 
[Скачать файл с настройками вотчеров](https://raw.github.yandex-team.ru/taxi/code-linters/develop/watchers.xml)

Потом импортировать вотчеры в 
_File | Settings | Tools | File Watchers_ для Windows и Linux, или
_PyCharm | Preferences | Tools | File Watchers_ для macOS.
Получим вотчер, который можно включать или отключать. Сделать его можно 
глобальным (должен подходить под любые проекты). После отработки вотчера можно будет 
переключаться между проблемами с помощью _F2_ или смотреть список проблем в 
_Inspect Code_, также в _Run_ должен быть вывод непосредственно команды 
`check-pep8` - там будут пути, по которым можно будет переходить к местам 
ошибок. 

Настройки вотчера можно конфигурировать по желанию и под свои нужды, 
подробнее 
[здесь](https://www.jetbrains.com/help/pycharm/using-file-watchers.html)

### Настройка
**Проверка в сабмодулях репозитория не производится**

Для настройки утилиты `check-pep8` можно использовать аргументы командной строки 
и файлы `services.yaml`(глобальные настройки)/`service.yaml`(настройки сервиса)
в секции `linters`. При запуске 
`check-pep8` глобальный конфиг объединяется для каждого сервиса с сервисным конфигом.
Допустимые опции:
* `package-dirs`: пути до каталогов, в которых следует искать пакеты уровня 
  "приложения" для правильной сортировки импортов. 
* `extra-application-package-names`: дополнительные имена пакетов уровня 
  "приложения" для сортировки импортов. Нужно для пакетов, которые нельзя 
  автоматически определить, как питоновские пакеты, например, для 
  автосгенерированных пакетов на C/C++
* `disable-paths-wildcards`: список путей/wildcards, проверку которых надо по 
  тем или иным причинам игнорировать 
* `disable-linters`: список линтеров, которые для проекта/сервиса отключаются 
  (допустимые значения: `pylint`, `flake8`, `mypy`)
* `disable-plugins`: тонкая настройка исключений для каждого линтера. Возможные 
  варианты:
  * `pylint`: 
    * `import-only-modules`
    * `pylint-quotes`
  * `flake8`: 
    * `broken-line`
    * `import-single`
    * `trailing-commas`
    * `import-order`
    * `mccab`
    
  Также для любого линтера можно указать непосредствено коды сообщений 
  этих линтеров
* `enable-plugins`: тонкая настройка включений для каждого линтера - 
по аналогии с `disable-plugins`, но поддерживаются только коды сообщений 
линтеров и пока сделано для `pylint`

Параметры командной строки:
* `--version`: вывод версии и выход
* `-v`, `-vv`: вывод INFO и DEBUG логов
* `-l`: список линтеров, которыми будем проверять 
  (допустимые значения: `pylint`, `flake8`, `mypy`). По-умолчанию - все
* `-t`: вывод в специальном формате для Teamcity
* `-w`: вывод в специальном унифицированном формате для вотчеров PyCharm/CLion
* `-s`: проверить только измененные файлы (смотрит разницу с HEAD)
* `-j`: количество одновременно запущенных процессов с линтерами (по-умолчанию 4)
* список путей до директорий/файлов, которые надо подвергнуть проверке
