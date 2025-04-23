# lavka-woody

Woody - система для хранения сведений о закупках товаров и их поставках на
лавки. Построена на основе проекта [Odoo](https://www.odoo.com/documentation/14.0/).

## Настройка окружения

0. Установить докер и залогиниться. Для этого:
 - Установить docker с помощью Self Service
 - Получить [токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1) для авторизации
 - Авторизоваться с помощью команды

`sudo docker login -u <login> -p <token_body> registry.yandex.net`
- Выполнить команды (chown - для Lunex, chrown - для MAC)

`sudo chrown -R $USER:$USER_GROUP ~/.docker`

 `sudo chrown -R $USER ~/.docker`

1. Создать venv и активироать его
2. Скачать Odoo в какую-нибудь папку ВНЕ этого проекта(ПОКА ЛУЧШЕ 14 версия):
   `git clone --single-branch --branch 14.0 --depth 1 https://github.com/odoo/odoo/`
   `git clone --single-branch --depth 1 https://github.com/odoo/odoo/`

3. Установить зависимости:

   ```shell
   sudo apt install python3-dev libxml2-dev libxslt1-dev libldap2-dev \
    libsasl2-dev libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev \
    libfreetype6-dev liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev \
    libxcb1-dev libpq-dev libreoffice
   ```
4. Найти экземпляр python связанный с Libreoffice. Для этого можно использовать скрипт:

   ```
   curl -o find_uno.py https://gist.githubusercontent.com/regebro/036da022dc7d5241a0ee97efdf1458eb/raw/find_uno.py
   python3 find_uno.py
   ```
5. Для этого экземпляра установить модуль unoserver:
   ```
   /path/to/python -m pip install unoserver
   ```
6. В папке с Odoo выполнить:

   ```
   pip install -r requirements.txt
   ```
7. Перейти в lavka-woody и выполнить:

   ```
   pip install -r requirements.txt
   ```

8. Указать PYTHONPATH, чтобы python находил пакеты odoo:
   ```
   export PYTHONPATH=<каталог, в котором лежит odoo>
   ```

9. Создать конфиг для локального запуска:
   ```
   cp config/host-local.yml.example config/host-local.yml
   ```
   В --addons-path указать через запятую путь до каталога с аддонами в Odoo и
   путь до каталога с аддонами в этом проекте.

    В --data-dir указать какую-нибудь папку. В ней woody создаст свои каталоги.

   В libreoffice.path_to_python указать путь к python из пп. 4-5.

11. Запустить базу
    ```shell
    make start_db
    ```

12. Выполнить инициализацию:
    ```
    python woody/initialize.py
    ```

13. Настроить direnv (не обязательно).
   При cd в папку проекта direnv будет сам подгружать env vars, указанные в .envrc
   ```
   cp .envrc.example .envrc
   # edit env vars on your taste
   nano .envrc

   # install direnv. ubuntu way
   sudo apt install direnv

   # allows direnv to load env vars automatically
   direnv allow
   ```

## DB Backup and Restore
```
# put file like dump_26-10-2021_11_38_34.sql
make backup_db

# restore db from file
make restore_db SQL_DUMP_PATH=dump_26-10-2021_11_38_34.sql
```


## Docker way
Чтобы не возиться с настройкой окружения прямо на ОС,
можно запустить его в докер-контейнере.

Из списка "Настройка окружения" нужно выполнить только пункт 0.

```
# start containers
# alias: start_c
make start_container

# enter to bash shell in the container
# alias: bash_c
make bash_container

# stop and delete all containers
# alias: down_c
make down_container
```

## Локальный запуск

1. Запустить базу:
   ```shell
    make start_db
    ```
2. Для работы генерируемых отчетов необходимо запустить Libreoffice используя библиотеку unoserver:
   ```
   <path/to/python из п.4 Настрйки оружения> -m unoserver.server --executable=soffice --daemon
   ```
3. Запустить Odoo:
   ```
    python woody/main.py
    ```
   Приложение будет доступно по URL http://localhost:8069/.

## Прочие команды
Остановить базу: `make stop_db`

Запустить woody локально в докере: `make start_back`

Остановить woody: `make stop_back`

Запустить psql: `cd woody && make psql-woody`

## Полезные ссылки
* Сайт: [production](http://woody.lavka.yandex.net) [testing](http://woody.lavka.tst.yandex.net)
* [PGaaS](https://yc.yandex-team.ru/folders/aku1kigsssp1v27aivhh/)
* [Wiki](https://wiki.yandex-team.ru/woody/)
