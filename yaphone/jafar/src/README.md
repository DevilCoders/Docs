jafar
=======

![img](https://jing.yandex-team.ru/files/tktabolov/Jafar.jpg "Do I look like I care?")

jafar (визирь, он же советник, он же "just another freakin' awesome recommender") - это маленькая рекомендательная система для нужд команды mobserver.

Установка
=========
Устанавливаем компоненты для развёртывания виртуального окружения 
```
sudo apt-get install python-dev python-setuptools python-pip python-virtualenv virtualenvwrapper python-all cython debhelper dh-virtualenv python-central
```


Устанавливаем зависимости из deb_requirements.txt
```
Необходимо поставить пакеты, указанные в deb_requirements.txt
```


Создаём virtualenv
```
mkvirtualenv jafar
workon jafar
```

Заходим в папку с проектом и устанавливаем зависимости питона
```
pip install -r requirements.txt -i https://pypi.yandex-team.ru/simple/
```


Компилируем cython
```
python setup.py build_ext --inplace
```
(необходимо выполнять при каждом изменении модулей на cython)


Собираем колёса (pip wheels) для nile коммандой
```
python make_nile_wheels.py
```

Готово

Скачать последний актуальный снапшот с моделями
=========
```
python manage.py update_snapshot
```


Создание датасета
=========
```
# лучше выполнять в скрине, т.к. процесс занимает несколько часов
python manage.py train update_dataset --country RU --proceed
```


Обучаем рекомендеры (необязательно, если скачали снапшот)
=========
```
python manage.py train train_recommenders --pipeline kano --
```

Запуск сервера и отправка запроса
=========

Заходим в корень проекта и поднимаем сервер
```
python manage.py runserver
```
(по умолчанию поднимается на 5001 порту)

В соседнем окне терминала отправляем запрос
```
curl  -X POST "https://jafar.<domain-name>.mobile.yandex.net/recommend/<experiment-name>" -d '<request-parameters>' -H 'Content-type: application/json' | python -m json.tool
```

например
```
curl  -X POST "https://jafar.test-int.mobile.yandex.net/recommend/sheeva" -d '{"country": "RU", "current_country": "RU", "group_size": 4, "country": "RU", "promo_count": 1, "group_count": 4, "user": "a539ecfe-b950-759d-1403-db2f59456ef7", "history": ["com.CedarFair.CedarPointVR", "in.fulldive.shell", "com.vkontakte.android", "com.exideas.cp.words.russian", "com.sillens.shapeupclub", "com.homido.vrcatalog", "je.fit", "com.getsomeheadspace.android", "com.yandex.launcher", "com.bambuna.podcastaddict", "org.coursera.android", "com.google.android.gm", "ru.yandex.taxi", "com.exideas.mekb", "com.google.android.apps.maps", "bm.velobike.droid", "org.videolan.vlc", "ru.yandex.metro", "ru.yandex.music", "com.facebook.lite", "com.github.jamesgay.fitnotes", "com.idamob.tinkoff.android", "com.Slack", "org.mozilla.firefox", "com.adobe.reader", "com.hemispheregames.osmos", "com.audible.application", "com.imgur.mobile", "com.neuralprisma", "ru.dublgis.dgismobile", "ru.raiffeisennews"]}' -H 'Content-type: application/json' | python -m json.tool
```

Известные ошибки
================
если при запуске получаем ошибку:
```
ImportError: /home/user/.virtualenvs/jafar/local/lib/python2.7/site-packages/M2Crypto/__m2crypto.so: undefined symbol: SSLv2_method
```

лечим так
```
sudo apt-get install --reinstall swig
pip uninstall m2crypto
pip install m2crypto --no-cache-dir
```
