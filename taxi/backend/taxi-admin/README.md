Админка Яндекс.Такси
====================

Админка - это большая панель управления, которая предоставляет обширную отладочную информацию и статистику работы сервиса, а так же позволяет редактировать широкий набор параметров. Доступ осуществляется по внутренним логинам только для избранных пользователей.

*  продакшен: https://ymsh-admin.mobile.yandex-team.ru
*  партнерский тестинг: https://partners-test-admin.mobile.yandex-team.ru
*  наш тестинг: https://ymsh-admin.tst.mobile.yandex-team.ru

Как запустить сервер для разработки
-----------------------------------

Машина для разработки - `taxi.mobile.dev.yandex.net`

Предположим, что репозиторий находится в папке `/home/user/taxi`. Тогда для запуска сервера необходимо:

*  создать симлинк из `/home/user/taxi/debian/manage.py` в `/home/user/taxi/taxi_admin/manage.py`
*  создать симлинк из `/home/user/taxi/debian/djangosettings.development.py` в `/home/user/taxi/taxi_admin/djangosettings.py`
*  создать симлинк из `/home/user/taxi/debian/settings.development.py` в `/home/user/taxi/taxi_settings.py`
*  находясь в каталоге `/home/user/taxi/taxi_admin`, выполнить команду `PYTHONPATH=/home/user/taxi:/home/user/taxi/taxi_admin python manage.py runserver taxi.mobile.dev.yandex.net:8000` (порт можно изменить)

Или, используя макрокоманды:

* `cd taxi_admin`
* `make init`
* `make run_local`

После этого админка будет доступна через браузер по адресу http://taxi.mobile.dev.yandex.net:8000/

В случае разработки на личном сервере
-------------------------------------

Помимо действий описанных выше, необходимо установить django 1.4 (`pip install -i https://pypi.yandex-team.ru/simple/ django==1.4`) и налить минимум данных:

    PYTHONPATH=..:. python manage.py load_initial_data
