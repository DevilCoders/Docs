# Pod Agent

Компонент сервиса Яндекс Деплой
Запускает пользовательские ворклоды в поде и следит за их состоянием

[TOC]

## Пользователю

https://wiki.yandex-team.ru/deploy/docs/podstack/

## DevOps

Бинарник pod_agent: daemons/pod_agent/pod_agent --help

### Окружение

#### Ресурсы

##### Диск
Необходимые гарантии по диску `1 GiB`:

1) `66 MiB` на бинарник pod_agent
2) `200 MiB` на логи
3) `570 MiB` на образ системы в распакованном виде https://sandbox.yandex-team.ru/resource/1116544606/view

Тест на размер бинарника:

https://ci.yandex-team.ru/test/e1d199cdb1e65637fffce6cccd1eaff1#disk_usage

https://a.yandex-team.ru/arc/trunk/arcadia/infra/pod_agent/daemons/pod_agent/ut/pod_agent_ut.cpp?rev=5061874#L210-215

##### Память
Для большинства пользователей необходимые гарантии по памяти: `200 MiB`

Более точная оценка: `(77 + 1.15 * N + 30) MiB` (на апрель 2020 https://st.yandex-team.ru/DEPLOY-1516 https://st.yandex-team.ru/DEPLOY-1517)
  1. 77 MiB на mlocked код
    Если памяти в поде недостаточно, код не лочится. В лог пишется ошибка TServiceMemoryLockError. pod_agent продолжает работать
  2. 1.15 MiB на каждый объект
  3. 30 MiB (максимум) на доставку логов - память настраивается через TLogsTransmitterConfig

##### CPU

Для большинства пользователей необходимые гарантии по CPU: `0.1s`

По оценке из https://st.yandex-team.ru/DEPLOY-1516#5ddfd912122154001d7df85e

#### Porto

Для работы pod_agent нужен установленный пакет yandex-porto не ниже версии 5.0.4

Для прогона тестов необходимо добавить пользователя в porto группу: `sudo usermod -a -G porto $USER`

Не забудьте настроить portod.conf для поддержки core_command. Пример portod.conf:
```
$ cat /etc/portod.conf
core {
    enable: true
    default_pattern: "/coredumps/%e.%p.%s"
    space_limit_mb: 102400
    slot_space_limit_mb: 10240
}
```

#### Утилиты

```
bash    для оборачивания набора команд в одну команду
sky     для скачивания rbtorrent ресурсов
wget    для скачивания http ресурсов
tar     для архивирования raw файлов, чтобы их можно было импотрировать в porto как layer
find, sort, xargs, cat, cut, awk, md5sum, sha256sum    для вычисления хеша закаченного ресурса
cd, cp, ls, mkdir, mv, rm, echo, base64, ln            для составления команд для загрузки ресурсов
```

### Чтение логов

#### Как читать логи

pod_agent использует infra/libs/logger для записи логов в бинарном (proto) формате

Для чтение логов есть два мода:
 * `./pod_agent print_log`
    Выводит логи в консоль в человеко-читаемом виде.
    Пример, вывод последних 20 сообщений: `./pod_agent print_log public_volume/eventlog -n 20`
    Читай больше по ключу `-h`.
 * `./pod_agent interactive_log`
    Красиво форматирует логи от behavior trees.
    Управление:
      * переключение между сообщениями - Enter, Backspace
      * скролл: page up, page down, arrows
      * выход: Esc, q

    Пример, с фильтром по id объекта: `./pod_agent interactive_log -i TBehaviourTreeTickV2 -p Workload_MainWorkload public_volume/eventlog`
    Читай больше по ключу `-h`.

#### Что такое behaviour trees

Behaviour дерево — дерево состоящее из двух типов вершин: листовые вершины и композитные вершины.

Листовые вершины не имеют детей и выполняют какие-то действия, например создают контейнер или проверяют наличие файла.

Композитные вершины имеют хотябы одного ребенка и позволяют cтроить логику, основанную на результатах их детей. Дети у таких вершин всегда обходятся **в одном и том же порядке**.

#### Как выполняется обход дерева

Вершины дерева могут быть в одном из четырех состояний, листовые вершины получают это состояние из результата действия, композитные выводят из результатов детей:
  1. `Success` означает что действие выполнено успешно или что какая-то проверка прошла (Контейнер создался успешно, был вызван `FileExist` на существующий файл).
  2. `Failure` означает что действие выполнено не успешно (но без критических ошибок) или что какая-то проверка не прошла (был вызван `FileExist` на несуществующий файл).
  3. `Running` означает что вершина работает асинхронно и действие сейчас выполняется.
  4. `Idle` вершина не имеет результата, такие вершины не должны выводиться в логе.

Поскольку есть асинхронные вершины, дерево может выполнять одну итерацию не за один его обход.

Когда корень дерева переходит в состояние `Success` или `Failure`, считается, что одна итерация дерева выполнена, и следующая итерация будет запущена с начала (все результаты вершин будут сброшены).

Так же каждая вершина дерева может вернуть `Error`, этот результат означет что произашла какая-то критическая ошибка. Этот результат сразу доходит до корня дерева и прекращает текущую итерацию.

#### Виды композитных вершин

Для удобства все композитные вершины в pod\_agent являются асинхронными.

##### MemSelector

Обходит своих детей пока не встретит первого ребенка с результатом `Success`, после этого возвращает результат `Success` и не рассматривает следующих детей.

Если ни один из детей не вернул `Success`, возращает `Failure`.

##### MemSequence

Обходит своих детей пока не встретит первого ребенка с результатом `Failure`, после этого возвращает результат `Failure` и не рассматривает следующих детей.

Если ни один из детей не вернул `Failure`, возращает `Success`.

##### Switch и Case

По результату вершины выбирает в какой `Case` пойти.

Результатом может быть состояние вершины (в таком случае под условием может быть целое дерево), а также значение какого-то enum (например по состоянию контейнера).

`Case` вершина ведет себя как `MemSequence`.

##### StaticSwitch

Аналог Switch для случая, когда результат условия известен на стадии построения дерева.

У такой вершины всегда остается один сын, и она возвращает его результат без изменений.

##### Inverter

Всегда имеет ровно одного ребенка и инвертирует его результат (из `Success` в `Failure` и обратно).

`Error` и остальные результаты возвращает без изменений.

##### TimedCache

Всегда имеет ровно одного ребенка и запускает его с timeout между запусками.

Если ребенок вернул `Error`, то ожидание timeout не будет, и ребенок будет заново запущен на следующем тике.

Если предыдущий результат не `Error`, и timeout между запусками не прошел, вершина возвращает предыдущий результат ребенка.

Если timeout между запусками прошел, запускается ребенок, его результат возвращается без изменений.

##### TryLock

Вершина, которая пытается захватить лок для синхронизации разных деревьев, возвращает `enum` для `Switch` вершины.

Всегда имеет ровно одного ребенка, которого запускает под локом.

Если лок захватить удалось, в зависимости от результата своего ребенка возвращает `child_success` или `child_failure`, иначе возвращает `try_lock_fail`.

`Error` своего ребенка возвращает без изменений.

#### Пример трейса дерева в interactive_log

```
RR> Root:LayerTree:MemSequence [SUCCESS]
  --> SwitchLayerPrivate(ELayerPrivate) [SUCCESS]
    --> PortoGetLayerPrivate(pod_agent_b4f0da8e41cccb97a045bc2520cf1278) [SUCCESS : failure]
    --> Case(failure) [SUCCESS]
      --> Switch(EConditionReturn) [SUCCESS]
        --> PortoLayerExists(pod_agent_b4f0da8e41cccb97a045bc2520cf1278) [FAILURE : Layer not found]
        --> Case(failure) [SUCCESS]
          --> MemSelector [SUCCESS]
            --> FileExists(/pod_agent/resources/layer/b4f0da8e41cccb97a045bc2520cf1278) [SUCCESS]
          --> Switch(EConditionReturn) [SUCCESS]
            RR> Root:TreeCheckAndCreateContainer:MemSelector [SUCCESS]
              --> PortoGetAndCheckProperties(pod_agent_layer_b4f0da8e41cccb97a045bc2520cf1278_download) [SUCCESS]
            --> Case(success) [SUCCESS]
              --> SwitchDownload(EPortoContainerState) [SUCCESS]
                --> PortoGetContainerState(pod_agent_layer_b4f0da8e41cccb97a045bc2520cf1278_download) [SUCCESS : running]
                --> Case(running) [SUCCESS]
                  --> FeedbackLayerState(b4f0da8e41cccb97a045bc2520cf1278, ELayerState_DOWNLOADING) [SUCCESS]
","Status":"SUCCESS","Tick":3,"TreeId":"ResourceGang_b4f0da8e41cccb97a045bc2520cf1278"}
```

В рендере дерева указаны вершины, которые обходились на текущем тике, а также их состояния.

`Status` означает состояния корня на момент завершения тика.

`Tick` означает сколько раз обходилось дерево с начала его создания.

`TreeId` означает id дерева. Обычно оно связано из id объекта из спеки, за исключением деревьев скачивающих ресурсы, в них это **внутренний** хеш ресурса.

### Чтение статуса из сокета pod_agent

pod_agent принимает запросы по grpc socket.
Можно использовать этот интерфейс для дебага проблем.
Например, вот так можно подменить спеку / посмотреть статус:
```
root@man2-9399-1:/# /pod_agent/pod_agent client 'unix:/pod_agent/pod_agent.socket' /ping
pong
root@man2-9399-1:/# /pod_agent/pod_agent client 'unix:/pod_agent/pod_agent.socket' /get_pod_agent_status
...
root@man2-9399-1:/# /pod_agent/pod_agent client 'unix:/pod_agent/pod_agent.socket' /update_pod_request --request-data-file /pod_agent/public_volume/human_readble_current_spec.json
{
    ...
    "id": "tadqrfro2eglqr7g",
    "ready": {
        "last_transition_time": {
            "nanos": 659042000,
            "seconds": 1580825351
        },
        "reason": "WORKLOADS_READY",
        "status": 1
    },
    "revision": 69,
    "spec_timestamp": 1697284544673088221,
    ...
}
```

## Разработчику

CI: https://ci.yandex-team.ru/project/693
TestEnv: https://testenv.yandex-team.ru/?screen=manage&database=pod_agent-trunk

### Release practice

Через ReleaseMachine: https://rm.z.yandex-team.ru/component/pod_agent

Чат с релизами: https://t.me/joinchat/BOQIc0-Ah_UABsYoRMNVKw

Чтобы выкатить pod_agent в Y.Deploy, надо в интерфейсе выбрать нужную ветку и зарелизить ее с нужным атрибутом.

Сейчас доступны следующие варианты релиза, желательно всегда кактить сверху вниз:

| Тип релиза | Атрибут                  | Ссылка на релизы |
| :--------: | :----------------------: | :--------------------------------------------------------------------------------------------------------------------------------------- |
| testing    | released_sas_test        | https://sandbox.yandex-team.ru/resources?type=POD_AGENT_BINARY&limit=20&attrs=%7B%22released_sas_test%22%3Atrue%7D&created=14_days       |
| prestable  | released_man_pre         | https://sandbox.yandex-team.ru/resources?type=POD_AGENT_BINARY&limit=20&attrs=%7B%22released_man_pre%22%3Atrue%7D&created=14_days        |
| prestable  | released_xdc_acceptance  | https://sandbox.yandex-team.ru/resources?type=POD_AGENT_BINARY&limit=20&attrs=%7B%22released_xdc_acceptance%22%3Atrue%7D&created=14_days |
| stable     | released_xdc             | https://sandbox.yandex-team.ru/resources?type=POD_AGENT_BINARY&limit=20&attrs=%7B%22released_xdc%22%3Atrue%7D&created=14_days            |

### Behavior trees

Бо́льшая часть "бизнес" логики pod_agent написана в парагидме "behavior tree"

Для просмотра редактирования деревьев необходимо настроить tools/behavior3editor

Деревья в json формате хранятся в libs/behaviour/trees
Содержание some_tree.json можно импортировать/экспортировать в behavior3editor.

На нашей стороне json деревья парсятся в libs/behaviour/loaders
Если хочется посмотреть список доступных нод или добавить новую, надо начинать смотреть оттуда

Несколько правил разработки деревьев:
1. Слишком сложные деревья стоит разбивать на несколько: корень дерева и под-деревья в отдельных json
2. Ветви селектора должны быть независимы (коммутативны)
3. Почти везде MemSelector, а не Selector; MemSequence, а не Sequence. Если не дожидаться porto нод, дерево начнет крутиться по бесконечному циклу.
4. В коде нод не должно быть условных операторов - такая логика должна быть в BT
