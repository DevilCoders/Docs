# lavka-hire
Сервис найма линейного персонала в Яндекс.Лавке

## Настройка окружения

1. Создать venv и активироать его
2. Скачать Odoo в какую-нибудь папку ВНЕ этого проекта:

   `git clone --single-branch --branch 14.0 --depth 1 https://github.com/odoo/odoo/`
 
3. Установить зависимости:
   
   ```shell
   sudo apt install python3-dev libxml2-dev libxslt1-dev libldap2-dev \
    libsasl2-dev libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev \
    libfreetype6-dev liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev \
    libxcb1-dev libpq-dev
   ```
   
4. В папке с Odoo выполнить:

   ```
   pip install -r requirements.txt
   ```
5. Перейти в lavka-hire и выполнить:
  
   ```pip install --index-url https://pypi.yandex-team.ru/simple/ -r requirements.txt```

6. Указать PYTHONPATH, чтобы python находил пакеты odoo:
   ```
   export PYTHONPATH=<каталог, в котором лежит odoo>
   ```

7. Создать конфиг для локального запуска:
   ```
   cp config/host-local.yml.example config/host-local.yml
   ```
   В --addons-path указать через запятую путь до каталога с аддонами в Odoo и
   путь до каталога с аддонами в этом проекте.
   В --data-dir указать какую-нибудь папку. В ней woody создаст свои каталоги.

8. Запустить базу
   ```shell
   make start_db
   ```

9. Выполнить инициализацию:
   ```
   python hire/initialize.py
   ```

## Локальный запуск

1. Запустить базу:
   ```shell
    make start_db
    ```
2. Запустить Odoo:
   ```
    python hire/main.py -u hire
    ```
   Приложение будет доступно по URL http://localhost:8069/.

## Прочие команды
Остановить базу: `make stop_db`

Запустить woody локально в докере: `make start_back`

Остановить woody: `make stop_back`

Запустить psql: `cd hire && make psql-woody`

