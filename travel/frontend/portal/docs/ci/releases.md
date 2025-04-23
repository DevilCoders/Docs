## Releases

### Create new release

Чтобы создать релиз, нужно перейти в наш проект [по прямой ссылке](https://a.yandex-team.ru/projects/portalvteam/ci/releases/timeline?dir=travel%2Ffrontend%2Fportal&id=regular-release),
либо найдя наш проект [в списке проектов в Arcanum](https://a.yandex-team.ru/projects/all?text=Travel%20Portal).

В списке проектов выберите `Portal release`, ветку `trunk`

![search project.png](https://jing.yandex-team.ru/files/isaven/Untitled%202.251646c.png)

На странице вы видите список задач, которые попадают в релиз

![tasks](https://jing.yandex-team.ru/files/isaven/Untitled%204.e93dea6.png)

Нажмите кнопку `Run release`.

![create release modal](https://jing.yandex-team.ru/files/isaven/Untitled.dd06ed0.png)

В окне все выбирается автоматически, нужно только нажать `Run release`.

_Но можно изменить коммит из которого создается релиз (поле commit),
отменить предыдущие незавершенные релизы (чекбокс `Cancel other releases`),
выбрать другой релизный флоу, про него ниже (поле `Release flow`),
оставить произвольное описание, которое будет на странице релиза (поле `Description`)_

### Process

После создания релиза будет создана новая ветка.
По клику на имя ветки можно провалиться на страницу ветки.
Со страницы ветки можно провалиться на страницу flow релиза, где виден текущий процесс (flow).
Ссылка на flow также есть в релизном тикете.

На странице flow, с кубиков прогона тестов, можно открывать отчет о прохождении тестов `Hermione GUI report` и скипать тесты через Testcop.
Смотри [документацию о e2e тестах на PR](../tests/pr-e2e-tests.md) и о [скипе тестов через Testcop](../tests/testcop.md).

Запускать шаги с ручным подтверждением, сейчас это

1. Перевод статуса в протестировано и выкатка в prestable
2. Выкатка в прод
3. Закрытие релизного тикета
4. Пропуск e2e тестов

Примеры ручных шагов

![manual](https://jing.yandex-team.ru/files/isaven/Untitled.fbe35d0.png) ![Skip e2e](https://jing.yandex-team.ru/files/isaven/Untitled.38e782c.png)

Можно переходить в ST в релизный тикет или на stage в Y.Deploy.

![ST link](https://jing.yandex-team.ru/files/isaven/Untitled.2d86e5f.png) ![Deploy link](https://jing.yandex-team.ru/files/isaven/Untitled%202.5e5a82e.png)

При падении каких-то кубиков, например e2e тестов, можно кубики перезапускать стрелочкой в правом нижнем углу.

### Fix in release

Исправления в релизе.
Если в релизе требуются внести исправления нужно:

1. сделать коммит с фиксом в `trunk`
2. перенести коммит в релизную ветку (`Cherry pick`), можно через UI - кнопка `Cherry pick`, а можно локально через arc
3. запустить новый релиз со страницы релиза с отменой предыдущих `Cancel other releases`

### Hotfix

Исправление версии в проде.

Если в проде требуются внести исправления уже выкаченной версии:

1. найти ветку предыдущего релиза в списке слева
2. сделать коммит с фиксом в `trunk`
3. перенести коммит в релизную ветку версии, которая в проде из пункта 1 (`Cherry pick`), можно через UI - кнопка `Cherry pick`, а можно локально через arc
4. запустить новый релиз с отменой предыдущих `Cancel other releases` со страницы релиза из пункта 1, который сейчас в проде, с хотфиксным флоу: `hotfix-release-flow`
5. если в процессе хотфикса был релиз, то нужно перенести фикс из `trunk` и запустить новый релиз из соответствующей релизу ветки.
   Чтобы фикс появился и в релизе тоже.

### Release flows

Для выкатки изменений можно использовать разные последовательности действий.
Сейчас у нас добавлены следующие варианты:

![release flows](https://jing.yandex-team.ru/files/isaven/Untitled.2edc533.png)

#### regular-release-flow

Штатный релиз (полный релизный цикл).
Выкатка на testing, прогон e2e тестов и прочих проверок.
Выкатка на prestable через ручное подтверждение.
Выкатка на production через ручное подтверждение

(Можно использовать для штатных релизов и медленных хотфиксов)

#### hotfix-release-flow

Быстрая выкатка изменений сразу на prestable и через ручное подтверждение в прод.
Без автоматических проверок.

## Links

-   [Документация CI о релизах](https://docs.yandex-team.ru/ci/release)
