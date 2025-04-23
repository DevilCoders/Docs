Кабинет партнера Яндекс.Такси
=============================

Кабинет - это небольшая панель управления, которая позволяет партнеру редактировать профиль своей компании и смотреть отладочную информацию. Доступ осуществляется по логинам на большом Яндексе, которые прописываются через профиль таксопарка в админке. Для суперпользователей открыта возможность смотреть кабинет любого партнера.

*  продакшен: https://taxi-cabinet.mobile.yandex.ru
*  партнерский тестинг: https://partners-test-cabinet.mobile.yandex.ru
*  наш тестинг: https://taxi-cabinet.tst.mobile.yandex.ru

Ещё у кабинета есть API. Прочитать о нем можно [на вики](https://wiki.yandex-team.ru/taxi/backend/api/cabinet).

Как запустить сервер для разработки
-----------------------------------

Машина для разработки - `taxi.mobile.dev.yandex.net`

Предположим, что репозиторий находится в папке `/home/user/taxi`. Тогда для запуска сервера необходимо:

*  создать симлинк из `/home/user/taxi/debian/manage.py` в `/home/user/taxi/taxi_cabinet/manage.py`
*  создать симлинк из `/home/user/taxi/debian/djangosettings.development.py` в `/home/user/taxi/taxi_cabinet/djangosettings.py`
*  создать симлинк из `/home/user/taxi/debian/settings.development.py` в `/home/user/taxi/taxi_cabinet/taxi_settings.py`
*  находясь в каталоге `/home/user/taxi/taxi_cabinet`, выполнить команду `PYTHONPATH=/home/user/taxi:/home/user/taxi/taxi_cabinet python manage.py runserver taxi.mobile.dev.yandex.net:8000` (порт можно изменить)

Или, используя макрокоманды:

* `cd taxi_cabinet/`
* `make init`
* `make run_local`

После этого кабинет партнера будет доступен через браузер по адресу http://taxi.mobile.dev.yandex.net:8000/
