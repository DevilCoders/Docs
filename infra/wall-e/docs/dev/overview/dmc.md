# DMC
DMC (Decision Making Center) - подсистема принятия решений в Wall-E.

## Общее описание

Основная задача - на основании данных мониторинга, уже имеющихся в базе данных, принять решение о каком-либо действии в отношении хоста и сохранить эту информациюю обратно в базу.

Сам DMC никак не общается со внешними системами и, тем более, хостами. Он состоит из двух частей, которые соответственно выполняют screening и triage.

Код находится [здесь](https://bb.yandex-team.ru/projects/NANNY/repos/wall-e/browse/walle/expert).

### Screening

Использует данные мониторинга для обновления статуса о здоровье хостов, которое возвращается во внешнем API и отображается в GUI. Реализовано шардирование.

### Triage

Использует данные мониторинга для запуска процесса принятия решения. Шаридирование не применяется.

## Данные

DMC использует данные, которые в Wall-E поставляет Juggler через [juggler-api](https://wiki.yandex-team.ru/infra-cloud/rfc/juggler/draft-022/). На стороне Juggler данные агрегируются по стойкам.

Инстансы Wall-E с juggler-api только сохраняют поступающие данные в базу и более не выполняют никакой полезной работы.

## Процесс принятия решения

После получения данных мониторинга они проходят [цепочку проверок](https://docs.yandex-team.ru/wall-e/automation/algorithm), по результатам каждой из которых выносится решение, здоров хост или необходимо совершить какое-либо действие для его восстановления.

Если сработало несколько проверок, к исполнению принимается первое принятое решение.

### Реализация

Каждая проверка представляет собой реализацию интерфейса `CheckRuleInterface`, который описывается единственным методом `apply`, принимающим хост и данные мониторинга, а возвращающего объект типа `Decision`, в котором содержится необходимое действие, его параметры, а так же другая информация.

Если с хостом все хорошо, вернется `Desicion` с `action=HEALTHY`. Все возможные варианты представлены в классе `WalleAction`.

Инициализация цепочки правил и процесс их перебора реализован в одном из наследников класса [AbstractDecisionMaker](https://bb.yandex-team.ru/projects/NANNY/repos/wall-e/browse/walle/expert/decisionmakers.py).





