## Setup Dev Env

* Install additional Python using Pyenv
    - [Installation instructions](https://github.com/pyenv/pyenv#homebrew-in-macos)
    - Suppress “Could not import the lzma module” error:
      ```console
      $ PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 3.10.2
      ```
* Install Visual Studio Code. And tune it:
    * Set up `$ code .` command: https://www.freecodecamp.org/news/how-to-open-visual-studio-code-from-your-terminal/
    * Install plugins:
        * https://marketplace.visualstudio.com/items?itemName=wholroyd.jinja
        * And you will be prompted to install several other plugins
* Install all required packages for Python:
    ```console
    $ pip install -r requirements.txt
    ```
* Install mongo shell:
    ```console
    $ brew install mongosh
    ```
* Download key projects from team's Google Drive and import them:
    ```console
    $ ./upload_data_to_mongo.py ~/Downloads/1.xlsx Q12022
    ```
* Start the project's Web-UI:
    ```console
    $ ./web_ui.py --debug
    ```


### Dev Exp Checklist
* `$ code .` works from any folder and launches Studio Code. You should see the folder files in Explorer
* Command `$ which python` shows something like `/Users/fantamp/.pyenv/shims/python`. Notice `shims` in the path
* `$ python` from command line launches the correct executeable. Python prints it's version in the first line
* `black` is set as default python code formatter
* Studio Code option "Format on save" is set. Type and check that `print('zzz')` in source code becomes `print("zzz")` after pressing Cmd-S/Ctl-S
* Svn works: you can checkout source code of the project
* Mongo port forwarding works OK: `$ ./forward-mongo-port.sh`. It sould look like you simply logged in via ssh to server `fantamp.sas.yp-c.yandex.net`. You may test it by typing command `$ hostname` and see `fantamp.sas.yp-c.yandex.net` as the result
* WebUI starts OK: `$ ./web_ui.py --debug`
* You can see the main page in your browser: http://localhost:33500/


## Links
* https://flask.palletsprojects.com/en/2.0.x/
* https://wtforms.readthedocs.io/en/3.0.x/
* Mongo:
    * https://docs.mongodb.com/manual/reference/mongo-shell/
    * https://docs.mongodb.com/manual/crud/#std-label-crud
    * https://hub.docker.com/_/mongo
    * https://pymongo.readthedocs.io/en/stable/
    * https://pymodm.readthedocs.io/en/stable/getting-started.html
* https://docs.docker.com/compose/compose-file/compose-file-v3/
* https://yc.yandex-team.ru/


## Backlog
* Темная тема
* Мобильная версия
* Подсвечивать дату обновления в секции Планы отчета "Запуски и Планы" если она какая-то не такая. Например, очень старая
* Добавить в меню пункт для создания тикета на развитие продукта
* Добавить формат отчета для вставки в Телеграм в отчете "Запуски и Планы"
* Добвить в отчет Запусков галочку, которая устанавливает все галочки в таблице
* Использовать WTForms для /reports/delivered-and-promised/mark c hidden_tag
* Добавить примечание уровня всего проекта. Протащить его в основные представления и отчеты
* Добавить архивацию проектов. Проверить, что арихвыне исчезают из всех представлений
* Ввести ранжирование для стадий запуска. Во всех отображениях применять его, чтобы сортировка шла по: проект/стадия/платформа
* Добавить показ обещаных, но не сделанных запусков
* Перейти на правильное формирование url в html-коде. Не вручную, а через route-функции
* Вынести майлстоуны в отдельную коллекцию?
* Транслировать статусы из экселя в машинно-читаемый формат. Поменять в бд, утилите импорта, интерфейсах
* Make the importing code work with the latest excel-table format from Google Spreadsheets
* Enrich teams/tech_lead/etc suggests from the real projects instead of the dedicated collections
* Log every date slide, every edit
* К скриншоту подписи, что это такое


## Backlog (some day later):
* Tests
* Logs
* UWSGI
* Easy app deployment
* Automaticaly update info in/from Startrek tickets
* ABC
* Blueprints
* Rewrite parts of the app in Rust



## Рекапы встреч
### 7.02.2022

Как делается отчет:
Определяется период за которые делается отчет П1
Определяется период в будущем для построеня прогноза запусков П2

По дате запуска Дима находит проекты, которые запустились в П1
Если дата запуска позже даты обновления, то надо уточнить у куратора, правда ли запустилось

Для МВП нужны:
* Список проектов/майлстоунов, которые попадают в П1. Красным подсветить те у кого дата_обновления < даты_запуска
* Список проектов/майлстоунов, у которых дата запуска попадает в П2
* Экспорт в эксель
* Колонка Reported. Отмечать то, что попало в отчет по запускам и будущим запускам. Это нужно для раскраски попадания в обещания

Просто пожелания:
К скриншоту подписи, что это такое
