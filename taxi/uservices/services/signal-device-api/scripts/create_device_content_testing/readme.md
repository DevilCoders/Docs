# How to use

### About

The script creates devices for a partner with events (with photo and video on them), status, device name, driver name, vehicle plate number 

### Prerequisites

1) Install **ya tool** and set its path in `config/static.json` (e.g. "/home/ikudyk/Tool/ya"), details in [wiki](https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife)
2) Install python 3.8 from [official site](https://www.python.org/downloads/)
3) Install requirements **pip3 install -U -r requirements.txt**
4) Write your OAuth token in /config/secret.json, details in [wiki](https://wiki.yandex-team.ru/users/ikudyk/notes/#yandexteam)
5) Put some images / videos up to 1 MiB in `helpers/images` and `helpers/videos` respectively

### How to run

1) Set necessary params in `config/dynamic.json` 
2) Run **python3.8 main.py**

### Extra notes

1) Use script with caution, do not add huge files for media or create hundreds of devices you do not need
2) After 5 minutes your devices will go offline regardless of script parameters 
