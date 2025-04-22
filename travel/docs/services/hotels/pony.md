---
title: ПОНЯбот
---
## ПОНЯбот

### Что это?

ПОНЯбот - это система, обеспечивающая сборку и релиз компонентов сервисов Яндекс.Путешествий (а именно - отелей).

Система состоит из нескольких частей и во многом опирается на базовую инфраструктуру Яндекса.

### Что именно умеет ПОНЯбот?

1. Готовить sandbox-ресурс с результатами сборки цели в аркадии.
2. Запускать такую сборку по изменению самой сборочной цели или её зависимостей (на основе аркадийного графа сборки).
3. Уведомлять о сборке в Slack команды путешествий
4. Генерировать changelog, состоящий из списка коммитов в компонент, произошедших между его релизами (сохраняется на wiki и отправляется в Slack).
5. Запускать релиз ресурса (и следовательно его деплой в няню) по команде из web-интерфейса.
6. Отображать список релевантных компоненту коммитов перед его релизом.
7. Уведомлять о начале релиза и о его завершении.
8. Уведомлять о компонентах, которые имеют давние изменения, всё ещё не попавшие в релиз.

### Как это всё работает?

Сборка ресурсов происходит в sandbox-тасках. Одна задача собирает один компонент из заданной ревизии.
Эти таски - наследники общих тасок YA_MAKE и YA_PACKAGE с некоторыми дополнениями: фильтрацией нерелевантных коммитов и отправкой уведомлений.

Запуск соответствующих задач [реализован](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/travel/TravelBuild.yaml) с помощью testenv.

Для обработки уведомлений от таск и отправки их в Slack, генерации changelog-ов, уведомлений о "потерянных" коммитах и работы web-сервера существует сервис, написанный на питоне и запущенный в няне - [slack_forwarder](https://nanny.yandex-team.ru/ui/#/services/catalog/slack_forwarder/).

### Добавление нового MAKE компонента

**Создать executable в аркадии**

Например, новый скрипт в [`arcadia/travel/hotels/tools`](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/tools/)

**Добавить package для sandbox**

[`arcadia/sandbox/projects/Travel/resources/__init__.py`](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/Travel/resources/__init__.py)

Добавьте себя в список `RELEASERS` если хотите в прод

    class TRAVEL_{NAME}_BINARY(sdk2.Resource):
        """
        {Description}
        """
        auto_backup = True
        releasable = True
        releasers = RELEASERS

[`arcadia/testenv/jobs/travel/TravelBuild.yaml`](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/travel/TravelBuild.yaml?rev=5981996#L396)

    _{NAME}:
      filter_targets:
        - {path_to_dir_of_executable}
      component_name: "{name}"
      targets: "{path_to_dir_of_executable}"
      arts: "{path_to_executable}"
      result_rt: "{executable resource type}"

**Закоммитить изменения**

**Настроить testenv**

Далее зайти в [testenv/travel-trunk] и нажать __Add job__ вверху справа. В списке выбрать `TRAVEL_MAKE_{NAME}` и нажать __Next__. Далее потребуется указать ревизию - укажите ревизию вашего коммита.

Для редактирования нужны права - за ними следует обратиться к людям из списка `WORKING` (вверху слева).

В результате этих изменений запуститься сборка бинарника, за которой можно наблюдать в канале [#понябот-build-notifications](https://app.slack.com/client/T1B8NLW31/C7GNHMHJ9) в Slack. Сборка будет автоматически запускаться при каждом коммите в `{path_to_dir_of_executable}`.

Сборка происходит в задаче [TRAVEL_YA_MAKE], которая создаёт ресурс типа `TRAVEL_{NAME}_BINARY`. Для использования этот ресурс надо зарелизить в testing и/или stable. Для этого надо открыть задачу `TRAVEL_YA_MAKE` и нажать кнопку с "галочкой" справа от заголовка.

[testenv/travel-trunk]: https://beta-testenv.yandex-team.ru/project/travel-trunk/timeline
[TRAVEL_YA_MAKE]: https://sandbox.yandex-team.ru/tasks?children=false&hidden=true&type=TRAVEL_YA_MAKE

### Как понять, почему сборка в поне не начинается и где там что застряло?

Сборка происходит в sandbox, но таски в нём запускает testenv. До запуска таски никаких сообщений в [#понябот-build-notifications](https://app.slack.com/client/T1B8NLW31/C7GNHMHJ9)не приходит, поэтому если testenv тормозит, то непонятно, что происходит.

Testenv тормозит часто, поэтому вот способ поверхностной диагностики проблем:

Вот тут все наши job-ы:
1. Realtime сервисы: https://beta-testenv.yandex-team.ru/project/travel-trunk-services/timeline
2. CPA : https://beta-testenv.yandex-team.ru/project/travel-trunk-cpa/timeline
3. SandboxPlanner: https://beta-testenv.yandex-team.ru/project/travel-trunk-sandbox-planner/timeline
4. Прочее: https://beta-testenv.yandex-team.ru/project/travel-trunk/timeline

Выбираешь нужную тебе, кликаешь на неё (например ORDERS): https://beta-testenv.yandex-team.ru/project/travel-trunk-services/job/TRAVEL_PACKAGE_ORDERS/history?limit=20 \
Тут видны коммиты, на которые job-а запустилась. \
Можно нажать на "**Unchecked revisions**" - появятся ревизии, на которые должен запуститься job, но ещё не запустился. \
Можно ещё нажать на "**Filtered revisions**". Появятся ревизии, на которых testenv решил не запускать эту job-у.

* Соответственно если твоя ревизия в Unchecked, то что-то подвисло, но ещё может запуститься (такое вообще редко бывает). Обычно в этом состоянии job-а очень недолго, если она уже долго так, то скорее всего что-то сломалось.
* Если ревизия в Filtered, значит где-то ошибка в конфигурации фильтрации (TravelBuild.yaml которая).
* Ну и наконец если самый последний коммит в списке (когда включены и Filtered, и Unchecked) старше твоего (меньше ревизия), то значит testenv просто отстаёт и твой коммит ещё в него не подтянулся.

Коммиты для каждого типа job-ов обрабатываются независимо, поэтому коммиты в один компонент могут отставать в то время как в другой будут обрабатываться.
Может даже быть так, что коммит, который два компонента задевает соберется для одного из них, а для другого - отстанет.

Ну и если предпочитаешь старый интерфейс, там всё то же самое: \
https://testenv.yandex-team.ru/?screen=jobs&database=travel-trunk \
https://testenv.yandex-team.ru/?screen=job_history&database=travel-trunk&job_name=TRAVEL_PACKAGE_ORDERS

Ещё иногда бывает удобно смотреть сюда: https://beta-testenv.yandex-team.ru/project/travel-trunk/timeline \
Здесь все наши коммиты во все компоненты. Но отставшие коммиты тут увидеть нельзя.

Если тестенв тормозит, то можно писать сюда: https://forms.yandex-team.ru/surveys/devtools?service=ci&ci_component=ci-testenv , но т.к. testenv deprecated, то всё тлен.


### Технические подробности

#### Testenv

На каждый компонент мы заводим свою job-у в testenv-е в этом [файле](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/travel/TravelBuild.yaml).
Таким образом, на один коммит может быть запущено сразу несколько job-ов: по одному на каждый изменённый коммитом компонент.

Job-ы добавлены в следущие базы:
1. Realtime сервисы: https://beta-testenv.yandex-team.ru/project/travel-trunk-services/timeline
2. CPA : https://beta-testenv.yandex-team.ru/project/travel-trunk-cpa/timeline
3. SandboxPlanner: https://beta-testenv.yandex-team.ru/project/travel-trunk-sandbox-planner/timeline
4. Прочее: https://beta-testenv.yandex-team.ru/project/travel-trunk/timeline

О разделении баз [тут](https://st.yandex-team.ru/DEVTOOLSSUPPORT-2796#5f620fde4d449262c4942854).

Для фильтрации коммитов мы используем опцию filter_targets testenv-а. Она не работает с package-ами, поэтому для компонентов, которые собираются с помощью ya package, создан дополнительный фейковый ya make, повторяющий структуру пакета, либо в конфиге job-а дополнительно используется observed_paths ([пример](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/travel/TravelBuild.yaml?rev=7309709#L42)).

#### Sandbox

Testenv по описанной выше схеме запускает в sandbox одну из следующих тасок для сборки: [TravelYaMake](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/Travel/tasks/TravelYaMake/__init__.py), [TravelYaPackage](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/Travel/tasks/TravelYaPackage/__init__.py).

Эти таски делегируют сборку таскам YaMake и YaPackage, но помимо этого:
1. Дофильтровывают нерелевантные коммиты, т.к. фильтрация в testenv работает плохо.
2. Отправляют уведомления о разных этапах сборки в slack-forwarder, чтобы он всё красиво отправил в Slack (обновил треды, начал следить за выкаткой в няне)
3. Создают в арке ветку вида `users/robot-travel-prod/builds/{component}/{revision}` при сборке и `users/robot-travel-prod/releases/stable/{component}/{revision}` при релизе (понадобятся slackforwarder-у).

*Подробнее про фильтрацию*.
Изменения считаются релевантными для компонента, если список измененённых файлов пересекается со списком зависимостей компонента.
Список зависимостей в свою очередь вычисляется так:
* Для make-компонент:
    * Все source-файлы из поля `graph[].inputs` вывода команды `ya make -j0 -k --dump-json-graph --strict-inputs path/to/component`
    * Все `ya.make`-и зависимостей, полученных командой `ya dump dir-graph --dump-deps path/to/component`
* Для package-компонент:
    * Зависимости каждого таргета по пути `.build.targets`, полученные так же, как зависимости make-компонента
    * Файлы, непосредственно указанные в описании пакета (`.data.source.files` для всех `.data.source` с `type == ARCADIA`)

#### Slack forwarder

##### Что делает?
* Обрабатывает события из сборочных тасок и отправляет уведомления в Slack (либо редактирует уже отправленные)
    * На каждый коммит в [#понябот-build-notifications](https://app.slack.com/client/T1B8NLW31/C7GNHMHJ9) приходит сообщение со списком задетых коммитов
    * Сообщение обновляется по мере изменения статуса сборки
    * В тред отправляются ключевые уведомления (о завершении сборки, деплое и пропуске сборки) - чтобы на тред можно было подписаться
* Строит changelog-и в момент релиза (при получении события от сборочной таски) на основе маркировочных веток, созданных сборочной таской (упомянуты выше). Отправляет его в Slack и [на вики](https://wiki.yandex-team.ru/travel/hotels/dev/changelogs).
* Уведомляет в Slack о коммитах, которые давно не релизились (используя те же маркировочные ветки в арке)
* Хостит [веб-интерфейс](https://ci.travel-dev.yandex-team.ru/components) для релизов
* Отправляет вспомогательные уведомления, не связанные со сборкой:
    * О дежурстве
    * О забытых в override настройках в няне

##### Как делает?

* Поднят в единственном экземпляре в Сасово, а потому не отказоустойчив
* Использует sqlite (а потому может что-то забывать):
    * Для хранения информации о идущих и завершенных недавно сборках
    * Для хранения идентификаторов сообщений в Slack-е (чтобы их обновлять и писать обновления в треды)
* Для построения changelog-а ходит в api arc-а и получает ветки, отмечающие релевантные коммиты (упомянуты выше)
* Для получения списка компонент (для web-интерфейса) из api arc-а достаёт [наш конфиг](https://a.yandex-team.ru/arc/trunk/arcadia/testenv/jobs/travel/TravelBuild.yaml) в testenv-е
* Для релиза из web-интерфейса ходит в api sandbox-а
* Хостит веб-интерфейс на Flask
* Для получения уведомлений от сборочных тасок, хостит ручки, в которые ходят сборочные таски (/build-notifications/*).
