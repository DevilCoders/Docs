# Точки входа

## noc.yandex-team.ru (прод)

Веб-интерфейс располагается тут [https://noc.yandex-team.ru](https://noc.yandex-team.ru)

Алгоритм работы в нем таков

* Чекбоксами выбирается список устройств и нажимаем **Create**, чтобы создать джобы
* Выбирается **Job type** (kind) сценария и тикет по которому она будет выполняться
* Для каждого устройства (джобы) можно выставить дату когда она должна начать выполнение (run after). В противном случае она начинает выполнение сразу.

У веб-интерфейса параметр **ticket** обязателен поэтому его необходимо создать заранее. Обычно это тикет в очереди NOCRFCS либо NOC.

## noc-ck-cli

При помощи cli можно делать все то же что есть в вебе и более.

Подробнее об использовании cli можно почитать тут: [{#T}](cli.md)

## Локальный dev-инстанс
Локальный инстанс может быть развернут на машине для разработки дополнительной функциональности, например для добавления новых типов экшенов или починки багов.

Его запуска используется скрипт [init-dev.sh](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck/-/blob/master/scripts/init-dev.sh).  Подробная инструкция находится в [README](https://noc-gitlab.yandex-team.ru/nocdev/noc-ck#установка-локального-цк) noc-ck.

Пример запуска:

```
# Разворачиваем venv и скачиваем python-зависимости
% ./scripts/init-dev.sh init
# Запускаем бекэнд
% ./scripts/init-dev.sh start
...
======== Running on http://localhost:5000 ========
(Press CTRL+C to quit)
INFO session:167: Got session id 0x1000000b00c0006
INFO session:168: Negotiated timeout: 4.0 seconds
DEBUG states:50: Session transition: lost -> connected
DEBUG session:178: Await for repairable state
DEBUG exec:19: No jobs found
```

В локальном инстансе присутсвует только бекенд, и нет веб-интерфейса. Таким образом единственный способ взаимодействия с ним `noc-ck-cli --local`:

```
azryve@azryve-osx noc-ck % noc-ck-cli --local list
609e64678bccccf1cdf57f63 created Job for ce8850-test
```

## Тесты

Для запуска юнит-тестов локально понадобится развернуть локальный dev-инстанс. После этого запуск тестов выполняем через `scripts/init-dev.sh`

```
# Разворачиваем venv и скачиваем python-зависимости
% ./scripts/init-dev.sh init
# Запускаем тесты
% ./scripts/init-dev.sh pytest
```

Скрипту можно передать имя конкретного теста

```
% ./scripts/init-dev.sh pytest tests/test_action.py
```
