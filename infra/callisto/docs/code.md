## Код

**Архитектура**

Интерфейс контроллера находится в `controllers/sdk/ctrl.py`.
Контроллеры объединяются в деревья (более точно – в ациклические ориентированные графы).
Чтобы добавить связь родитель-сын, контроллер должен использовать метод `register(*child_ctrls)`
Процесс работы программы – обход этого дерева в бесконечном цикле и вызов специальных методов (указаны в порядке вызова):
* `set_context(context)` – восстановление внутреннего состояния контроллера
(актуально, например, для билдера – ему нужно помнить, кто что строит). 
Для использования этого метода нужно реализовать свойство `id`.
Вызывается только на первой итерации или неудавшейся предыдущей итерации (если было выброшено исключение).
* `update(reports)` – метод призван обновить внутреннее состояние контроллера, выполняется от листьев к корню. 
Если контроллер реализовал свойство `tags`, то через аргумент `reports` передаются отчеты агентов из сборщика отчетов
(смотри `docs/api.md`).
* `execute()` – здесь можно описать некоторые действия над дочерними контроллерами. Выполняется от корня к листьям.
* `gencfg()` – здесь генерируются новые конфиги для агентов.
* `get_context()` – парный метод для `set_context()`.

Помимо указанных методов есть еще несколько полезных:
* `json_view()` – текстовый "viewer" контроллера. 
Доступен по адресу `<url корневого контроллера>/path/to/ctrl`,
где `path/to/ctrl` формируется при спуске к контроллеру от корня конкатенацией свойства `path` его предков.
* `set_handler(path, handler)` позволяет добавить пользовательское api к контроллеру. 
Такая ручка будет доступна по адресу `<url корневого контроллера>/path/to/ctrl?handler=<путь, переданный в set_handler>`
* `html_view()` – html "viewer" контроллера. Доступен по том же урлу, что и json_view(), но с параметром &viewer=da.
* `notifications()` – способ контроллеру передать в соломон произвольный сигнал, показать во вьюере "баннеры" с важной информацией или сделать и то и другое сразу.
Нотификации бывают 4-х уровней: IDLE, INFO, WARNING, ERROR. Вьюер показывает все, кроме IDLE.
Из метода нужно вернуть наследника `TextNotification` или `ValueNotification` из [controllers.sdk.notify](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/controllers/sdk/notify.py?rev=3941415)
Смотри [пример](https://a.yandex-team.ru/arc/trunk/arcadia/infra/callisto/controllers/build/innerbuilder.py?rev=3941415#L102)

Если в процессе обхода дерева выбрасывается исключение, то гарантируется, что конфиги агентов не будут изменены.
Кроме того гарантируется, что конфиги могут быть опубликованы только все сразу.
Не может быть ситуации, что они были обновлены частично.
Конфиги подписываются unix-таймстемпом, а агент применяет только более новые конфиги, отбрасывая старые.
Таким образом не может быть ситуаций, когда агент откатывается на более старый конфиг.

**Вьюеры**
* У контроллера есть встроенный вьюер на пути `/`, в котором можно посмотреть на дерево контроллеров, их json/html вьюеры, список пользовательских api.
[Пример](https://ctrl.clusterstate.yandex-team.ru/web/prod/)
[Пример2](https://ctrl.clusterstate.yandex-team.ru/callisto/man/)
* По пути `/timeline` можно посмотреть статистику работы контроллера и последние пойманные исключения.

**Остальное**
ya make && ./runner/runner
Для отладки следует использовать параметр `--readonly`.
Соломоновские сигналы [можно найти тут](https://solomon.yandex-team.ru/?project=cajuper)
