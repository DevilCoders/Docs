## Автоматическое управление нагрузкой на локации aka Avtomatika (formerly MonsysDC)

* Документация к системе: https://wiki.yandex-team.ru/jandekspoisk/sepe/stability/projects/avtomatika
* Основано на monsys (proxy_monsys): https://wiki.yandex-team.ru/regionproxy/monsys

#### Разработкa

* `virtualenv .venv && source .venv/bin/activate`  # создать виртуальное окружение
* `pip install --no-deps -r requirements/development.txt`  # установить зависимости
* `vagrant up`  # установить и запустить ZooKeeper; установить NodeJS, установить зависимости, собрать js bundle
* `make tests`  # проверить тесты
* `(cd misc/ && ./fakeserver.py) &`  # запустить сервер-заглушку 
* `./app.py -c configs/development.yaml -v nanny_token=XXX -v switter_token=XXX`  # запустить приложение
* http://127.0.0.1:8888/

#### Тестирование

* `MONSYS_CONF=testing.yaml python -m pytest tests/`
* `MONSYS_CONF=testing_functional.yaml python -m pytest tests_functional/`

То, что написано выше может не работать или работать не полностью.
