# Подключение автоматизации релизов

## Терминология
* **<сервис>** - имя вашего сервиса в package.json после префикса `@yandex-int/`;
* **<версия>** - семвер с префиксом `v`;

## Релизные префиксы
В гите, в качестве релизных веток использовали формат `release/<сервис>/vX.Y.Z`. Любой пользователь с правами на запись мог создать релизную ветку для любого сервиса в frontend. Релизные ветки ничем не отличались от обычных веток, на них нельзя точечно ограничить права. В арке это решено на уровне vcs. Через IDM можно выдавать права на доступы к релизным веткам и создание тегов в арк.

Релизный префикс для сервисов в frontend имеет формат `releases/frontend/<сервис>/`. При отведении релизной ветки к префиксу будет добавлена версия и название ветки будет `releases/frontend/<сервис>/vX.Y.Z`.

> :warning: Важно: Роль **Prefix admin** стоит запросить руководителю сервиса. Будьте избирательны, не выдавайте права админа большой группе людей и роботам.

### Права на релизные ветки
1. [Запросите в IDM][branch-prefix-admin] роль **Prefix admin** на префикс `releases/frontend/<сервис>/`. Эта роль позволяет управлять правами на все ветки в префиксе и выдавать права разработчикам и роботам;

При необходимости можете выдать роль **Create** и **Fast-forward push** дежурным разработчикам, это может понадобиться для черипика или реверта коммитов в релизе.

### Права на релизные теги
Релизные теги живут в префиксе `tags/releases/frontend/<сервис>/` и права на них настраиваются отдельно.

1. [Запросите в IDM][tag-prefix-admin] роль **Prefix admin** на префикс `tags/releases/frontend/<сервис>/`;

> :x: Важно: Обратите внимание, что в арке релизные ветки и теги не удаляются!

[Документация][arc-branches] арка про релизные ветки.


## Конфиг a.yaml
В корне вашего сервиса должен быть файл a.yaml. Откройте его и проверьте, что название вашего сервиса (поле `title`) и шаблон для релизного тикета (поле `ci.flows.release-flow`).
Если файла нет, то вам необходимо его создать:
1. Скопируйте [services/stub/a.yaml] в свой сервис;
1. В `title`: __Стаб для новых проектов__ переименуйте, можно на название вашего сервиса;
1. В `ci.releases.release.title`: __Стаб для новых проектов__ переименуйте, можно на название вашего сервиса;
1. В `ci.flows.release-flow` заполните релизные префиксы и шаблон релизного тикета:
    1. В `path_in_arcadia` укажите путь до вашего сервиса в арке, путь указываем от корня Аркадии;
    1. В `release_branch_prefix` укажите префикс релизных веток;

> :warning: Важно: Обратите внимание, что релизные префиксы должны заканчиваться слэшом `/`!


## Перенос релизного тега из гит в арк
Для бесшовной миграции релизов нам нужно перенести из GitHub в Аркадию последний релизный тег. Это нужно для правильной сборки changelog и увеличения версии релиза. Наш релизный конвейер завязан на релизные теги. Они являются неким идентификатором или печатью, что коммит на который указывает тег протестирован и отправлен на продакшен. Ещё служат опорной точкой для построения changelog, мы получаем changelog сравнением последнего релизного тега и trunk `arc log <релизный тег>...trunk | grep тикеты`.

Релизный тег из GitHub в Аркадию вам нужно перенести руками. Данная операция делается **один раз** перед переключением релизов.

1. Найдите последний релизный тег вашего сервиса в GitHub. Релизный тег в гите имеет формат `<сервис>/<версия>`:
    ```console
    git fetch --tags
    git for-each-ref refs/tags/<сервис> --sort=-committerdate --format="Тег: %(refname:lstrip=2) версия: %(refname:lstrip=3) коммит: %(objectname)" --count=1
    ```
1. Скопируйте коммит из предыдущего пункта и найдите сопутствующую ревизию в арке:
    > :warning: Важно:  \<upstream\> должен указать на апстирим search-interfaces/frontend, а не на форк!
    > Доступные удалённые репозитории можно посмотреть запустив команду `git remote -v`.

    ```console
    git fetch <upstream> refs/notes/vcssync:refs/notes/vcssync
    git notes --ref refs/notes/vcssync show <коммит>
    ```

1. Создайте релизный тег в арке с версией из п1. Для пуша вам понадобится роль **Create** на префикс `tags/releases/frontend/<сервис>/`. Запросите по аналогии с `Prefix admin`, смотрите раздел про релизные теги:
    ```console
    arc push r<ревизия>:tags/releases/frontend/<сервис>/<версия>
    ```
    Например, `arc push r123456:tags/releases/frontend/my-service/v1.234.0`

    > :warning: Обратите внимание, что у ревизии есть префикс `r`!


## Настройки Морти
[Морти][morty] - сервис для автораскатки релизов в Няне. Пропустите если он у вас не используется.

В настройках [Морти][morty] для автодеплоя релиза используется поиск по заголовку релиз-реквеста, который совпадает с заголовком релизного тикета. В новом флоу у нас поменяется формат заголовка, вместо `report-templates/search-interfaces/frontend@ydo/v2.2049.0` будет `releases/frontend/ydo/v2.2049.0`.

1. Найдите ваш конфиг в [Морти][morty];
1. Откройте конфиг для редактирования, можно через шорткат ⌥3;
1. Найдите в конфиге массив `titleRegexp`, обычно он содержит одну строку
    ```
    "titleRegexp": [
        "^report-templates/search-interfaces/frontend@<сервис>/[0-9v\\.]+( \\(hotfix\\))?"
    ]
    ```
1. Добавьте в массив `"^releases/frontend/<сервис>/[0-9v\\.]+( \\(hotfix\\))?"`. В итоге он должен выглядит так
    ```
    "titleRegexp": [
        "^report-templates/search-interfaces/frontend@<сервис>/[0-9v\\.]+( \\(hotfix\\))?",
        "^releases/frontend/<сервис>/[0-9v\\.]+( \\(hotfix\\))?"
    ]
    ```
:warning: Не забудьте заменить **<сервис>** на название вашего сервиса!

> Историческая справка:
> * `report-templates` - Префикс  нужно было когда-то давно для шаблонов репорта, репорт ушёл от нас в лучший мир;
> * `search-interfaces/frontend` - Отражает организацию и репозиторий в GitHub, в Аркадии нет организаций.


## ABC
Добавьте вашу команду разработчиков и тестировщиков а ABC сервис [frontend][abc-frontend].


## Автоотведение релизов
В CI вы можете настроить автозапуск релиза в a.yaml файле. Простой пример конфига автозапуска:

```yml
auto:
  conditions:
    - schedule:
        days: MON, WED
        time: 04:00 - 04:30 MSK
        day-type: workdays
      since-last-release: 30m
```

Про различные настройки подробно написано в [документация][ci-autorelease] про автозапуск релизов в CI, пример настройки автозапуска можете посмотреть в конфиге [services/messenger/a.yaml].


## Гитовый релизный конфиг
Удалите гитовый релизный конфиг `services/<сервис>/.config/release.json` и закоммитите изменения.


## Отведение релиза из CI
1. Перейдите по ссылке `https://a.yandex-team.ru/projects/frontend/code/frontend/services/<сервис>`;
1. Перейдите на вкладку CI;
    ![stub-project]

1. На вкладке **Releases** найдите название вашего сервиса. Ранее в разделе про a.yaml вы переименовали __Stub release__, надо искать именно то, что написано в `ci.releases.release.title`;
1. Нажмите на кнопку _Run release_;
    ![stub-ci]

1. Выберите флоу, который хотите запустить. **release-flow** - для регулярных релизов, **hotfix-flow** - для хотфиксов;
    ![stub-release]

1. CI запустит таску для отведение релиза и создаст плашку, перейдя на которую можно посмотреть на пайплайн и найти ссылку на Sandbox таску.
    ![stub-release-flow]

[Документация][ci-ui] про пользовательский интерфейс CI.




[branch-prefix-admin]: https://idm.yandex-team.ru/#rf=1,rf-role=awbb1uIw#arc-vcs/prefix-admin(fields:(ref-prefix:releases/frontend/%3Cservice%3E/)),f-status=all,sort-by=-updated,rf-expanded=awbb1uIw
[tag-prefix-admin]: https://idm.yandex-team.ru/#rf=1,rf-role=awbb1uIw#arc-vcs/prefix-admin(fields:(ref-prefix:tags/releases/frontend/%3Cservice%3E/)),f-status=all,sort-by=-updated,rf-expanded=awbb1uIw
[arc-branches]: https://docs.yandex-team.ru/devtools/src/arc/branches#acl
[services/stub/a.yaml]: https://a.yandex-team.ru/arc_vcs/frontend/services/stub/a.yaml
[morty]: https://wiki.yandex-team.ru/morty/
[services/messenger/a.yaml]: https://a.yandex-team.ru/arc_vcs/frontend/services/messenger/a.yaml
[ci-autorelease]: https://docs.yandex-team.ru/ci/release#usloviya-avtozapuska-relizov
[release-faq]: https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/release.md
[abc-frontend]: https://abc.yandex-team.ru/services/frontend/
[stub-project]: https://jing.yandex-team.ru/files/zumra6a/2021-09-01T10:54:41Z.643429a.png
[stub-ci]: https://jing.yandex-team.ru/files/zumra6a/2021-09-01T10:58:33Z.493f617.png
[stub-release]: https://jing.yandex-team.ru/files/zumra6a/2021-09-01T10:59:33Z.edaa461.png
[stub-release-flow]: https://jing.yandex-team.ru/files/zumra6a/2021-09-01T11:00:08Z.9e7851d.png
[ci-ui]: https://docs.yandex-team.ru/ci/ui
