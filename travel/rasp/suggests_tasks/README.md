# suggests2
Новые саджесты Расписаний.

Девелоперская веб-морда здесь http://suggests.rasp.dev.yandex.net/


## Для дев стенда

запуск саджестов:
:~/work/suggests2$ common/virtualenv-setup.sh --dev
:~/work/suggests2$ virtualenv .env
:~/work/suggests2$ . .env/bin/activate
(.env) :~/work/suggests2$ pip install -r suggests/requirements.txt | grep -vi "Requirement already satisfied"
(.env) :~/work/suggests2$ export PYTHONPATH=$(pwd)
(.env) :~/work/suggests2$ export DJANGO_SETTINGS_MODULE=local_settings_app
(.env) :~/work/suggests2$ gunicorn suggests.search.wsgi -c suggests/search/gunicorn_conf.py $@

генерация файлов:
:. ./common/virtualenv/bin/activate
:export PYTHONPATH=$(pwd)
:export DJANGO_SETTINGS_MODULE=local_settings_gen
(virtualenv):python suggests/generate/ytwork/search_stat.py '/home/ganintsev/data/suggests/gen' --days 20 $@ # это генерация stat.msgpack из yt, возможно лучше скопировать этот файл с прода
(virtualenv):python suggests/generate/generate.py '/home/ganintsev/data/suggests/gen' -sr -sm $@
