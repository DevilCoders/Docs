## Описание

Это монорепа DMP. Перед тем, как что-либо делать стоит узнать что такое DMP и как оно работает: [вики](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform). Для большинства задач нужно уметь пользоваться [dmp_suite](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform/core)

Также в данной монорепе содержатся правила сервиса репликации. Если вы пришли настроить репликацию,
переходите [сюда](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules).

Для всех рабочих вопросов есть [чат в телеграм](https://t.me/joinchat/BAEPiR0CPGvciZY2OZocxQ)
и [канал в Slack](https://yndx-go.slack.com/archives/C01E8KXKV55).

Основной сценарий использования DMP - решать задачи [DWH](https://wiki.yandex-team.ru/taxi/dwh).

## Разработка в виртуальном окружении

До начала разработки следует прочитать [Getting Started Guide](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform/getting-started).
Краткая выжимка про настройку окружения ниже.

Для работы нужно выбрать и настроить себе [окружение](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform/getting-started/#env).
Это можно быть:
- [Jupyter](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform/getting-started/jupyter)
- [личная вируталка](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform/getting-started/dev-on-vm/)
- свой ноутбук, для настройки следует ориентироваться на личную виртуалку -
готовой инструкции нет

Так же скорее всего потребуется доступ к YT и Greenplum.

### Добавление новых зависимостей

Новые зависимости следует добавлять в `dmp_deps/Pipfile`.
Старайтесь не фиксировать в нём версии библиотек, без необходимости – ставьте просто `*`.
А если уж по каким-то причинам версия должна быть зафиксирована, то эта причина должна быть изложена
в комментарии над зависимостью.

`Pipfile` содержит секцию packages куда следует прописывать зависимости, которые потребуются при разработке и в продакшене.

(`deprecated`) dev-packages – библиотеки нужные только при разработке, тестах и сборке.

Команда `tox -e dev` ставит всё, что указано в обоих этих секциях.

**Важные примечания:**

1. В `Pipfile` надо прописывать лишь те библиотеки, от которых зависит наш код.
2. После того, как ты поменял что-то в `Pipfile`, запусти `tox -e update-deps`. Он обновит `Pipfile.lock`,
   зафиксировав в нём номера и того, что прописано в `Pipfile` и всего, от чего эти библиотеки зависят.
   `Pipfile.lock` надо коммитить в репозиторий вместе с изменениями в `Pipfile`.
3. Изменение либ нужно делать отдельным ПР. Выкатывать dmp_deps в прод.
   Только потом сливать ПР с кодом использующим эту либу.

## Настройка PyCharm
Для того чтобы PyCharm подхватил все импорты, необходимо пометить корневые директории `dmp_suite`, `*_etl` и все верхнеуровневые директории внутри `submodules` как `Sources root`:
<details><summary>Гифка на добавление `Sources root`</summary>

  ![Run standard loader](https://jing.yandex-team.ru/files/amleletko/Peek%202019-08-09%2012-42.gif)

</details>

Есть достаточно подробная инструкция по настройке [PyCharm](https://wiki.yandex-team.ru/taxi/dwh/tools/pycharm/)

## Pull Request

1. Делаем ветку от ``trunk`` по названию тикета, например, ``TAXIDWH-XXXX``
2. Читаем про то, как мы оформляем `Pull Request`-ы и `commit message`-и на
[вики](https://wiki.yandex-team.ru/taxi/dwh/dmpasplatform/getting-started/#deploy)
3. Назначаем ревьюеров (при большинстве изменений ревьюеры будут назначены
автоматически: см. описание ``Code Review`` ниже). Подробнее про ревью на
[вики](https://wiki.yandex-team.ru/taxi/dwh/development/convention/codereview)
4. После ревью, отбежавших тестов и тестирования кода сливаем `Pull Request` в
`develop`.

## Code Review
Правила ревью настраиваются через `a.yaml`.
Инструкция: https://docs.yandex-team.ru/arcanum/pr/ship_policy

## Про код
1. [PEP-8](https://www.python.org/dev/peps/pep-0008/)
2. [PEP-257](https://www.python.org/dev/peps/pep-0257/)
3. Аннотации типов: [mypy](http://mypy-lang.org/)

## Cython
Иногда упираемся в производительность python (и иногда даже не осонзнаем).
Также можно дешево делать биндинги к C/C++ библиотекам (ну а вдруг).

Сейчас cython генерирует C++ код, который компилируется под с++17

В прецессе создания расширения генерятся .cpp и .so файлы. Лучше настроить rsync
не затирать .so, чтобы не билдить их после каждого синка.

Если пишите cython расширение, используйте абсолютные импорты, т.к. cython
несколько более требователен к путям.
Когда расширение написано в `service.yaml` нужно добавить информацию про него
(см. `dmp_suite/service.yaml`, `dmp_suite/setup.py` для примера)

Билдить .so файлы можно так:
```python setup.py build_ext --inplace --force```

`tox` эту команду выполняет автоматически. Если у вас насыпет ошибок,
tox все равно соберет окружение, но без speedup-ов, в этом случае напишите,
 пожалуйста, @igsaf.

## Nile на Python3

1. Если используете `parsed_log_line` в qb2 - ключи будут там bytes всегда (py3 `{b'key': 'val'}.get(u'key') == None`)
2. Если py3 лоадер наткнется на бинарный мусор он завалится весь. Есть ряд способов решения данной пробелемы, обращайтесь к @igsaf.
