## Airflow холодный старт

0. Расчитано на ubuntu focal 18 минимум
1. Установка пакетов. Тут dev и pip для python3, redis для airflow и crhome для отчетов покрытия
    ```
    sudo apt update
    sudo apt install python3-pip
    sudo apt-get install nano
    sudo apt-get install libpq-dev python-dev python3-dev 
    sudo apt-get install redis
    sudo apt-get install xvfb

    sudo apt-get update
    sudo apt-get install software-properties-common
    sudo add-apt-repository ppa:canonical-chromium-builds/stage
    sudo apt-get update
    sudo apt-get install chromium-browser 
    sudo apt install chromium-chromedriver
    ```
2. Установвка и запуск redis
    ```
    sudo systemctl enable redis-server
    sudo systemctl start redis-server
    ```
3. Установка arc
    ```
    sudo apt -y install yandex-arc-launcher
    systemctl --user enable --now arc-update.timer
    ```
4. Питоновские пакеты
    ```
    sudo pip3 install psycopg2-binary
    sudo pip3 install celery
    sudo pip3 install Redis
    sudo pip3 install python-telegram-bot
    sudo pip3 install tqdm
    sudo pip3 install selenium
    sudo pip3 install splinter
    sudo pip3 install pyvirtualdisplay
    sudo pip3 install bs4
    sudo pip3 install langdetect
    sudo pip3 install xvfbwrapper
    sudo pip3 install multiprocess
    sudo pip3 install -i https://pypi.yandex-team.ru/simple/ metr_utils --ignore-installed PyYAML
    sudo pip3 install apache-airflow
    sudo pip3 install mmh3
    ```
5. Базовя ннастройка airflow
    ```
    sudo adduser airflow
    mkdir airflow
    cd airflow
    mkdir logs
    export AIRFLOW_HOME=~/airflow 
    sudo chmod 4755 /etc/cron.allow
    echo airflow > /etc/cron.allow
    
    # После счекаутить аркадию
    arc mount ~/arcadia

    # Запустить обновление aiflow
    ~/arcadia/metrika/analytics/airflow_metrika/arc_update.sh

    # Потом добавить токены metr_utils и yt по инструкции
    
    # Инициализация бд для airflow
    airflow db init

    # Запуск airflow
    ~/airflow/airflow_start.sh
    ```
