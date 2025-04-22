## Startrek Graph

Позволяет рисовать графы зависимостей между задачами в Трекере и встраивать их прямо в трекер.

### Установка и настройка

* Установите модуль
```bash
pip install --user -i 'https://pypi.yandex-team.ru/simple/' yandex-startrek-graph
```
* Получите [токен Стартрека](https://wiki.yandex-team.ru/users/katsimoto/how-to-change-field-value/#how-to-get-a-token)
* Сохраните токен в удобное место (файлик `~/.st-token` отлично подойдет)

### Примеры использования 

```python
from startrek_graph import RequirementsGraphInjector

injector = RequirementsGraphInjector(token=STARTREK_TOKEN)

# Добавить комментарий с графом зависимостей
injector.append_as_comment("TEST-32856")

# Вместо "Description Graph" можно передать другой текст, в атрибут title:
injector.append_as_comment("TEST-32856",  title="Прогресс на 14.02.2020")

# Встроить граф зависимостей в описание тикета:
injector.inject_into_description("TEST-32856")

# Обновить граф зависимостей в описании тикета:
injector.inject_into_description("TEST-32856")

# Вернуть граф зависимостей в виде строки, в синтаксисе BlockDiag
injector.compile("TEST-32856")
```

Когда граф зависимостей встраивается в описание тикета в первый раз, в тикете должна быть строка `//DEPS_HERE`.
Повторное встраиваение в описание приведет к обновлению графа - это удобно.

При наведении порядка в зависимостях удобно пользоваться `injector.compile()`,
т.к. эта функция не вызывает изменений в трекере и не засоряет историю подписчикам.


## Как всё сейчас устроено

В данный момент StartrekGraph собирается в докер контейнер и выкладывается в QLOUD.
Небольшая схема как лежит в QLOUD'е:
![Небольшая схема по сервису:](https://jing.yandex-team.ru/files/pshevtsov/2020-09-03_20.44.10-Pc5GT.png)

## Сборка.
Сборка производится командой:
```
sudo docker build --cgroup-parent docker -f Dockerfile -t registry.yandex.net/taxi-dwh/startrek_graph_test:pshevtsov .
```

## Отправка в докер-репозиторий
Отправить в докер-репозиторий Яндекса:
```
sudo docker push registry.yandex.net/taxi-dwh/startrek_graph_test:pshevtsov
```

## Локальный запуск
Запустить контейнер локально:
```
sudo docker run --cgroup-parent docker -p 5000:80 registry.yandex.net/taxi-dwh/startrek_graph_test:pshevtsov
```

## Выкладка
1. Собрать докер образ через sandbox, предварительно настроив нужные параметры (ветка в гите, версия образа и тд):
  1. Sandbox таска для выкладки докер образа на тестовое окружение: https://sandbox.yandex-team.ru/task/849700843/view
  2. Sandbox таска для выкладки докер образа на продовое окружение: https://sandbox.yandex-team.ru/task/849704943/view
2. Зайти по ссылке: https://platform.yandex-team.ru/projects/taxi-tools/taxi-dwh-idm-integration/{testing, stable} и нажать там Update, выбрав нужную версию для раскатки.
3. Выбрать нужную версию образа и нажать Update

## Логи.
1. yabs-graphite-client
    + ```/var/log/yandex/graphite-client/graphite-client.log```
    + ```/var/log/yandex/graphite-client/graphite-sender.log```
2. Веб-приложения
    + ```/var/log/yandex/startrek_graph/startrek_graph.tskv```
3. Логи работы контейнера:
    + ```tail -f -n 10 run/qloud/app.stderr```
4. Docker logs: 
    + ```/var/log/upstart/docker.log```
5. Логи из контейнеров также пишутся ещё в PGaaS. Таблица log.python_log
6. Логи приложения в тестовой кибане: индекс = taxi-dwh-* https://kibana7.taxi.tst.yandex-team.ru/
7. Логи приложения в продовой кибане: индекс = taxi-dwh-qloud-* https://kibana.taxi.yandex-team.ru
    + чтобы найти в продовой кибане логи приложения, нужно поставить фильтр ```application: startrek_graph```

Логи внутри контейнера хранятся 14 дней (используется стандартный log-rotate). Если выложили новую версию контейнера - то все записанные ранее логи теряются.
  
## Дашборды и графики
1. Дашборд по работе сервиса: 
2. Дашборд по просмотру состояния SQS-очереди: 
    + Тест: https://solomon.yandex-team.ru/?project=kikimr&cluster=sqs&service=kikimr_sqs&host=cluster&dashboard=SQS&l.queue=startrek_graph&l.user=taxidwh-test&b=1h&e=
    + Прод: https://solomon.yandex-team.ru/?project=kikimr&cluster=sqs&service=kikimr_sqs&host=cluster&dashboard=SQS&l.queue=startrek_graph&l.user=taxidwh&b=1h&e=

## Конфиги.
Используется секретница для хранения паролей, логинов и тд.
1. Для продакшен окружения:
    + https://platform.yandex-team.ru/secrets/secret.taxi-dwh-idm-sqs-token
    + https://platform.yandex-team.ru/secrets/secret.taxi-dwh-startrek-graph-token
2. Для тестового окружения:
    + https://platform.yandex-team.ru/secrets/secret.taxi-dwh-idm-sqs-token-test
    + https://platform.yandex-team.ru/secrets/secret.taxi-dwh-startrek-graph-token-test

## Что проверять после релиза
1. Проверить логи в Кибане, что всё хорошо
2. Курлануть пару методов, например:
Прод: ```START_TIME=$SECONDS && curl -X GET https://dwh-idm-integration.taxi.yandex-team.ru/startrek_graph/ && echo $(($SECONDS - $START_TIME))```
```curl -X POST https://dwh-idm-integration.taxi.yandex-team.ru/startrek_graph/task-status/TABL-121```

Тест: ```START_TIME=$SECONDS && curl -X GET https://dwh-idm-integration.taxi.tst.yandex-team.ru/startrek_graph/ && echo $(($SECONDS - $START_TIME))```
```curl -X POST https://dwh-idm-integration.taxi.tst.yandex-team.ru/startrek_graph/task-status/TABL-121```

## Используемые переменные окружения
1. STARTREK_TOKEN
2. SQS_TOKEN

## Реализованные методы
1. '/dependency-graph/task/<task_code>', methods=['GET', 'POST']
   + POST тут кладёт задание в очередь селери
2. '/dependency-graph/query', methods=['GET']
3. '/task-status/<task_code>', methods=['GET', 'POST']
   + POST тут кладёт задание в очередь селери
4. '/task-status/<task_code>/from/<year>/<month>/<day>', methods=['GET', 'POST']
5. '/sprint-presentation/<board_id>/sprint/<sprint_id>', methods=['GET']
6. '/sprint-presentation/<board_id>/sprint/from/<sprint_from_id>/to/<sprint_to_id>', methods=['GET']

Также можно посмотреть все эти методы в файле: https://github.yandex-team.ru/jkermakov/startrek-graph/blob/master/app.py

### Подключиться к bash'у контейнера
```
sudo docker exec -it label_of_running_container bash
```
