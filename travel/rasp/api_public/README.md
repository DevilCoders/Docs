Public API
=====

Публичный API Расписаний
* https://tech.yandex.ru/rasp/raspapi/
* https://wiki.yandex-team.ru/Raspisanija/API/

Запуск dev-сервера на локальной базе:
* git submodule update --init
* ./common/virtualenv-setup.sh --dev
* cp local_settings.example.py local_settings.py  # создаем файл локальных настроек. Можно и нужно менять под себя.
* python manage.py runserver [::]:8001
* curl localhost:8001/ping   # проверяем, что сервис жив и имеет коннект к базе

Использование debug toolbar:
* Cоздать директорию staticfiles в директории проекта.
* Запустить ./common/virtualenv/bin/python manage.py collectstatic.
* Добавить параметр debug=true в запрос.
