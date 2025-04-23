# Как подключить проект к Тесткопу?

Подключение проекта сводится к описанию конфигурации через [UI](https://testcop.si.yandex-team.ru/config/new) Тесткопа.

Ниже описывается для чего и что нужно сделать, чтобы в проекте появилась возможность скипать или мьютить тесты, вручную и автоматически.

## Обязательная часть конфигурации

### Чтобы Тесткоп мог получать необходимую информацию о проекте

а именно:
- имена активных веток, если проект находится в Гитхабе, или последние релизные теги, если проект находится в Аркадии – чтобы отображать и сохранять скип-листы для конкретных веток *(например, для релизов);*

- названия пулл-реквестов – чтобы извлекать из них информацию о тикетах заскипа при раскипе тестов;

а также, чтобы сохранять в истории Тесткопа ссылки на пулл-реквесты, в которых тесты были починены.

Нужно указать имя проекта на вкладке **General**:
![](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-general.png)

А на вкладке **VCS** выбрать тип системы контроля версий – `github`, `arc` или `arc-from-github` – и заполнить соответствующие поля.

#### Если проект находится в Github'е

Нужно указать владельца *(owner)*, репозиторий *(repo)* и главную ветку *(main branch)* проекта:

![скриншот: vcs github](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-vcs-github.png)

#### Если проект находится в Аркадии

Нужно выбрать в селекте *arc* и указать путь к проекту *(project path)* и *(releases tags path)*:

![скриншот: vcs arc](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-vcs-arc.png)

Путь к проекту можно задавать в абсолютном виде, например: `https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4`, или в относительном: `frontend/projects/web4` – это не имеет значения, так как система автоматически вырезает базовую часть пути вида `https://a.yandex-team.ru/arc/trunk/arcadia/` и оставляет только относительную часть (в данном примере это будет `frontend/projects/web4`).

#### Если проект мигрировал из Github'а в Аркадию

И был при этом уже подключен к Тесткопу, пока еще находился в Github'е, то нужно выбирать в селекте `arc-from-github`.

![скриншот: выбор vcs arc-from-github](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-vcs-select.png)

При этом в настройках будут сохранены старые данные из вкладки `github`: *owner*, *repo* и *main branch*. И поменять их нельзя, так как в базе данных все записи о прогонах тестов в этом проекте все ещё содержат эти данные.

![скриншот: vcs arc-from-github](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-vcs-arc-from-github.png)

В будущем все проекты, которые мигрировали из Гитхаба в Аркадию и выбрали *vcs* `arc-from-github`, будут переведены на тип *vcs* `arc` прозрачным для разработчиков образом (в рамках тикета [FEI-24505](https://st.yandex-team.ru/FEI-24505)).

### Чтобы Тесткоп мог создавать тикеты заскипа

Выполните следующие действия:

- [дайте](https://doc.yandex-team.ru/tracker/external/manager/queue-access.html#queue-access__section_bvq_dc3_3z) доступ роботу `robot-testcop` (он же [Растин Коул][robot-testcop]) к очереди проекта:

  - откройте раздел **Доступ** на странице настроек вашей очереди;

  - введите в поле ввода `robot-testcop`;

  - поставьте галки на **Создание / Просмотр / Редактирование задач**:

    ![скриншот: выдача доступа к очереди роботу robot-testcop](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.queue-add-robot-testcop.png)

  - нажмите кнопку **Сохранить**:

    ![скриншот: кнопка сохранить](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.queue-save-robot-testcop.png)

- [добавьте](https://doc.yandex-team.ru/tracker/external/manager/components.html#components__section_zrt_szk_xz) в своей очереди компоненту, по которой вы сможете отфильтровать тикеты заскипа, например, `hermione_fix_skip`;

- [создайте](https://doc.yandex-team.ru/tracker/external/user/create-template.html) шаблон в Стартреке для тикетов заскипа под свой проект и [дайте](https://doc.yandex-team.ru/tracker/external/user/share-template.html#share-template__section_nmn_prs_zz) роботу `robot-testcop` права доступа к нему:

  ![скриншот: права доступа к шаблону](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.st-template-access.png)

  ![скриншот: выдача доступа к шаблону роботу robot-testcop](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.st-template-add-robot-testcop.png)

- перейдите в [режим редактирования](https://doc.yandex-team.ru/tracker/external/user/edit-template.html#edit-template__section_xwm_41t_zz) вашего шаблона;

- откройте инспектор кода и найдите ID (номер) вашего шаблона:

  ![скриншот: где взять номер шаблона](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.template-id.png)

- если шаблона не будет, или вы забудете дать к нему доступ, то Тесткоп будет использовать [шаблон по умолчанию][default-template];

  *в тикетах заскипа, которые будут создаваться на основе [шаблона по умолчанию][default-template], будет проставляться тег (а не компонента) `hermione_fix_skip` (почему тег? – потому что шаблон по умолчанию существует вне очереди и задать в нём компоненту невозможно); данный тег позволит разработчикам найти все тикеты заскипа в своей очереди, если они были созданы на основе [шаблона по умолчанию][default-template]:*

  ![скриншот: шаблон по умолчанию](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.template-default-one.png)

- заполните вкладку **Startrek**, выбрав существующий шаблон для **FEI** или пустой (**Empty**):
  С параметрами - очередь (Queue ID), её компоненты (components) и номер шаблона (Template ID).
  ![](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-startrek.png)

### Чтобы гермиона могла пропускать заскипанные тесты

Добавьте в своем проекте в настройках [гермионы][hermione] плагин [@yandex-int/hermione-muted-tests][hermione-muted-tests].

### Чтобы разработчик мог скипать или мьютить тесты из sandbox-задачи

Тесткоп должен знать какие тесты упали в гермионе. Для этого выполните следующие действия:

- убедитесь, что ресурсы html-отчетов hermione, которые должны обрабатываться Testcop, соответствуют требованиям:

  - ресурсы успешно публикуются и в итоге оказываются в состоянии `READY`

  - ресурсы имеют тип `SANDBOX_CI_ARTIFACT`

  - у ресурсов выставлен атрибут `collect_stats='true'` (true - строка)

  - у ресурсов выставлены атрибуты `build_context`, `commit_sha` и `branch`.

- добавьте в своем проекте в настройках [гермионы][hermione] плагин [json-reporter][json-reporter];

  *Примечание: как правило, этот плагин сразу отключают, выставляя его опцию `enabled` в значение `false`, так как заскипать тесты из локальных запусков невозможно. А в CI, откуда разработчик может скипать тесты, плагин включают, выставляя переменную окружения `json_reporter_enabled` в значение `true`. Например, [так](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/task/test_task/BaseTestTask.py?rev=r8189558#L309).*

- настройте публикацию его ресурсов;

  _[Пример](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/frontend-ci/legacy/trendbox/run-job.js?rev=r8228988#L109), как это делается в монорепозитории `frontend`._

- добавьте ссылку на Тесткоп в sandbox-задачу, ссылка должна выглядеть так:

  `https://testcop.si.yandex-team.ru/task/{task-id}`

  или так:

  `https://testcop.si.yandex-team.ru/task/{task-id}?project={project}`

  если в рамках одной sandbox-задачи запускается несколько гермион для разных проектов.

  Значение query-параметра `project` должно совпадать с атрибутом `project` ресурса, в который упаковывается отчет плагина [json-reporter][json-reporter].

  Здесь и выше `{task-id}` – номер sandbox-задачи.

  *Примеры:*

  - _в [sandbox_ci][sandbox-ci] ссылка на Тесткоп добавляется [так](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/task/test_task/BaseTestTask.py?rev=r8230869#L373)._

  - _а в проекте frontend это [реализуется](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/frontend-ci/legacy/trendbox/run-job.js?rev=r8230884#L118) с помощью публикации отчета с `index.html`, в котором указан редирект на страницу [Testcop][testcop] с необходимыми параметрами:_

  ![скриншот: пример ссылок на Тесткоп в проекте frontend](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.testcop-link-in-sb-task.png)

## Опциональная часть конфигурации

К опциональной части конфигурации относятся настройки, которые разрешают ручные мьюты и активируют механизмы автомьютов и автозаскипов.

А также настройки, которые позволяют разработчикам с помощью Тесткопа правильно приоритезировать и делегировать работу над починкой заскипанного (или замьюченного) теста.

Например:

- разработчик скипает какие-то тесты;

- при заскипе тестов Тесткоп создает тикеты, в рамках которых эти тесты будут чиниться;

- раз тесты скипаются, значит, какая-то функциональность проекта перестает покрываться этими тестами;

- эта функциональность из-за чьих-то изменений *может* сломаться, и никто этого не заметит;

- при этом функциональность может быть критичной, или наоборот – совсем не критичной;

- Тесткоп может автоматически выставлять нужный приоритет тикетам заскипа – в зависимости от критичности тестов, которые отключаются разработчиком;

- критичность *(priority)* тестов Тесткоп может узнать в Testpalm'е.

Далее:

- над проектом может работать множество виртуальных команд *(так называемые, v-teams);*

- соответственно, починкой заскипанных тестов должны заниматься те команды, которые отвечают за эти тесты (или точнее, за фичи, работоспособность которых покрывается этими тестами);

- Тесткоп может автоматически присваивать тикетам заскипа компоненты тех *v-teams,* которые отвечают за скипаемые тесты;

- к какой команде *(v-team)* относится скипаемый тест Тесткоп тоже может узнать в Testpalm'е.

### Чтобы Тесткоп брал приоритеты для тикетов заскипа из Testpalm'а

Заполните вкладку **Testpalm**:
![](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-testpalm.png)
  - заполните поле **Project ID**, указав идентификатор вашего проекта в Testpalm'е.

  - опишите словарь `Priorities` для конвертации приоритетов из Testpalm в Startrek: поля **Testpalm** и **Startrek** – приоритеты в одноименных сервисах *(используйте английские версии названий);* обратите внимание, что поля нужно заполнять, даже если у вас совпадают названия приоритетов в сервисах Testpalm и Startrek.

#### Чтобы Тесткоп брал v-team для тикетов заскипа из Testpalm'а

  - для начала убедитесь, что в вашей очереди, где будут создаваться тикеты заскипа, есть соответствующие компоненты *v-teams;* компоненты должны начинаться с восклицательного знака и пробела, например: `! Suggest` или `! Objects and media`;

  Заполненного поля **Project ID** уже достаточно для того, чтобы Тесткоп автоматически проставлял компоненту *v-team* для тикета заскипа.

  Компонента для Стартрека формируется Тесткопом согласно шаблону `! some-v-team-from-testpalm`, то есть восклицательный знак и пробел к названию команды из Testpalm'а добавляются Тесткопом автоматически.

  Однако, бывают проекты, в которых названия компонент в Стартреке отличаются от соответствующих компонент в Testpalm'е.

  В таком случае:

  - заполните подраздел `V-teams`, для конвертации названий команд из Testpalm в компоненты Startrek. Поле **Testpalm** – имя команды, а **Startrek** – компонента в Startrek *(без восклицательного знака и пробела).*

### Чтобы активировать механизм автомьютов

Заполните вкладку **AutoMute**:

![](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-automute.png)

- нажмите "Add tool" и добавьте инструмент из шаблона. Можно добавить несколько инструментов. Если нужно, откорректируйте параметры.

- раздел **Rules** содержит правила с параметрами **Number of runs** (коэф. успешности теста)  и **Minimal success rate** (число запусков теста). Правила описывают минимальный требуемый коэффициент успешности теста на заданном количестве запусков.

Подробнее про механизм автомьютов читайте в разделе «[Автомьюты][auto-mutes]».

### Чтобы активировать механизм автозаскипов

Заполните вкладку **AutoSkip**:
![](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-autoskip.png)

  - нажмите "Add tool" и добавьте инструмент из шаблона. Можно добавить несколько инструментов. Если нужно, откорректируйте параметры.

  - `Mute rate limit` - определяет предельно допустимый процент прогонов теста, в которых тест мьютится; при превышении данного значения, система автоматически заскипает тест;

    *Примечание: тесты заскипываются автоматикой не сразу, а раз в сутки, поэтому на момент заскипа теста его mute rate (коэффициент замьюта) может уже значительно превышать данный параметр.*

  - `Run count to analyze` - определяет число запусков, по которым вычисляется *mute rate*.

Подробнее про механизм автозаскипов читайте в разделе «[Автозаскипы][auto-skips]».


### Настройки отображения статистики
Статистика по тестам видна на главной странице сервиса Testcop под катом **Show tests statistics**.

 - настройки всех параметров можно заполнить из шаблона, нажав **Fill from template** и выбрав ваш вариант, основываясь на имени ветки, которая используется на вашем проекте. В поле **Gather for last** можно указать период, за который необходимо собирать статистику. Ниже можно указать список веток + зарезервированное имя - **all** для статистики по всем веткам.

![](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-statistics.png)


## Деплой конфигурации
Убедитесь, что все поля заполнены корректно и нажмите **Save**. В открывшемся окне можно посмотреть на результирующий JSON, который будет отправлен на сервер. Проскрольте JSON и нажмите **Deploy**. Готово – теперь используется обновленная версия конфига.

![](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.how-to-add-project.config-deploy.png)

## Наши планы

В будущем мы планируем [упростить подключение проектов к Тесткопу](https://st.yandex-team.ru/FEI-22059) так, чтобы разработчик мог подключить свой проект без создания ревью-реквеста в код инфраструктуры, и, соответственно, без обращения к дежурным инфраструктуры.

[github-enterprise]: https://github.yandex-team.ru/
[testcop]: https://testcop.si.yandex-team.ru/
[testcop-config]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/testcop-config/index.js
[robot-testcop]: https://staff.yandex-team.ru/robot-testcop
[hermione]: https://doc.yandex-team.ru/si-infra/hermione/hermione.html
[hermione-muted-tests]: https://doc.yandex-team.ru/si-infra/tests-stability/hermione-muted-tests.html
[json-reporter]: https://github.com/gemini-testing/json-reporter
[default-template]: https://st.yandex-team.ru/settings/templates/issues?name=Testcop%3A%20починка%20hermione-теста%20(шаблон%20по%20умолчанию)&owner=1120000000073856
[sandbox-ci]: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci
[infraduty]: https://wiki.yandex-team.ru/infraduty/form/
[auto-mutes]: https://doc.yandex-team.ru/si-infra/tests-stability/testcop/testcop-auto-mutes.html
[auto-skips]: https://doc.yandex-team.ru/si-infra/tests-stability/testcop/testcop-auto-skips.html
