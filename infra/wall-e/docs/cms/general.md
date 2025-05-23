![wall-e_and_eve](../_assets/wall-e_and_eve.jpg)

Цель CMS, как и цель Wall-E, состоит в обеспечении доступности кластера. В отличие от Wall-E, CMS знает и может принимать во внимание топологию кластера, текущую загруженность, доступность шардов и хостов. Задача CMS – обладая этими зананиями, обеспечить работы на кластере без его деградации.

Что означает "без деградации" – зависит от кластера, но в основном речь идёт про то, чтобы быстро отдать в ремонт сломанный хост, если его состояние мешает кластеру работать, или увести нагрузку с работоспособных хостов и не позволить Wall-E разломать кластер, забрав слишком много хостов в работы. Перед выполнением каждой команды на ребут/редеплой/whatever (вне зависимости от того, кем она была инициирована - человеком или автоматикой) Wall-E будет запрашивать разрешения у CMS проекта, которому принадлежит хост.

API сделано предельно простым, чтобы его можно было реализовать с минимальными усилиями со стороны разработчика CMS. В процессе развития Wall-E оно, скорее всего, будет расширяться (к примеру, будут добавляться новые информационные поля, которые могут понадобиться CMS) - для нормальной поддержки несовместимых изменений сделано версионирование CMS API. В данном документе описана CMS API v1.4, историю можно посмотреть [в описании изменений](versions.md). Мы считаем приемлемым, чтобы ваша CMS-API поддерживала любую описанную версию, не обязательно самую последнюю. Например, [default CMS](#default-cms) – собственная имплементация, предоставляемая Wall-E, поддерживает версию v1.0.

При создании проекта для него будет назначена [дефолтная CMS](#default-cms).

Для любого проекта можно задать любое неограниченное число cms, но есть ограничения:
- нельзя задать две и более дефолтных cms
- каждая кастомная cms должна иметь свои уникальный URL

При задании 2 или более cms, Wall-e будет запрашивать разрешение на задачи следующим образом:
- если все cms вернули в ответ на запрос 'OK', то задача будет принята к выполнению
- если хотя бы одна cms вернула 'IN_PROGRESS', то задача продолжит ожидать решения cms
- если хотя бы одна задача вернет 'REJECTED', то задача будет отменена

В cli можно заменить настройки cms так:
`$ wall-e projects modify-project-cms replace $id --cms $url -v v1.4 --tvm-app-id $tvm_app_id`
Добавить еще одну cms:
`$ wall-e projects modify-project-cms add $id --cms $url -v v1.4 --tvm-app-id $tvm_app_id`

В качестве `$url` должен выступать URL, через который Wall-E будет взаимодействовать с вашей CMS. Чтобы Wall-E мог обратиться по заданному URL, необходимы дырки от макроса `_GENCFG_ALL_WALLE_`. Wall-E будет ходить в cms-api с tvm-тикетом от tvm-app-id `2010518`.


## Описание протокола взаимодействия {#description}
Основным примитивом взаимодействия является `task` – задача, которую Wall-E хочет выполнить над хостом. Задача может быть автоматической или ручной, деструктивной или недеструктивной, долгой или короткой, все эти параметры Wall-E передаёт в параметрах задачи.

Когда Wall-E запускает операцию, он создаёт задачу в CMS-API. Когда операция завершена или требуется выполнить другую операцию, Wall-E удаляет старую задачу и создаёт новую.

Получив запрос на создание задачи, CMS может сразу позволить или запретить операцию, но в основном CMS сохраняет задачу, выполняет все необходимые действия, требуемые для сохранения кластера, и после этого позволяет выполнение операции.

CMS имеет возможность отклонять выполнение операции, но пользоваться этой возможностью стоит разумно, потому что отказ в выполнении операции означает, что сервер останется сломанным или регламентная операция не будет проведена.

В протоколе предусмотрен `dry-run` – Wall-E отправляет "пробный запрос" с параметрами задачи и CMS может сразу ответить отказом. В таком случае Wall-E не будет запускать операцию над хостом. Если операция была инциирована пользователем, то отказ будет сразу виден в API или UI, Wall-E покажет пользователю сообщение от CMS.

На стороне Wall-E работает GC, который сравнивает список задач в CMS со списком операций, запущенных в Wall-E. Если в CMS есть задачи, которые уже должны быть завершены, GC их удаляет.

При запуске любой задачи (кроме предзаказов) владелец хоста может указать опцию `--ignore-cms`. Предполагается, что он знает, зачем он это делает. Если указывать эту опцию, CMS уведомлений не получит.

### Workflow взаимодействия Wall-E и CMS {#workflow}
Перед тем, как запустить операцию, Wall-E создаёт в CMS-API соответствующую задачу, указывая параметры операции и список хостов. CMS-API сохраняет эту задачу в своей БД. В ответ на создание задачи CMS может сразу позволить выполнение или отклонить операцию, но это не обязательно делать. CMS должна проверить наличие флага `dry-run`, прежде чем сохранять задачу.

Wall-E периодически приходит и запрашивает состояние задачи – поллит задачу в CMS-API. Когда задача переходит в статус "позволено" или "отклонено", Wall-E либо отменяет операцию, либо выполняет её.

Если CMS отклоняет операцию, Wall-E переводит хост в статус `dead` и удаляет задачу из CMS. Если операция позволена, Wall-E выполняет операцию и после её завершения удаляет задачу из CMS-API. Если операция не привела хост в работоспособное состояние, Wall-E может сразу запросить следующую операцию.

GC периодически поллит список задач в CMS-API и сравнивает их со списком выполняемых операций. Любую задачу, для которой нет соответствующей операции, Wall-E удалят, независимо от её статуса в CMS-API. Wall-E рассчитывает, что удалённая задача пропадёт из списка.

### Соглашения и гарантии {#t&c}
Значение `$task_id` уникально среди всех проектов, в т.ч. для задач с флагом `dry-run`. Если у вас несколько проектов (например, разбиты по локациям) и вы используете одну и ту же CMS, то можно расчитывать на то, что в неё никогда не придут два запроса одновременно с одним и тем же id но разными хостами.

В данный момент в качестве таймаута на API-запрос к CMS используется 10 секунд, поэтому обработка всех запросов должна укладываться в этот таймаут. Следует считать, что это SLA.

Задача, которую Wall-E удалил из CMS-API, должна быть удалена из выдачи `GET /tasks/` и `GET /tasks/$task_id`. В противном случае Wall-E попытается удалить задачу снова.

Если CMS отклонила задачу, она всё равно сохраняет её. Удаляет задачу Wall-E, после того, как обработает её статус.

### (Не)Уникальность задач для хостов {#multiple-tasks}
Технически протокол предусматривает, что в одной задаче может быть запрошен список из нескольких хостов, и CMS может позволить работы над всеми сразу или отклонить все сразу. На практике, при обработке группы хостов Wall-E создаёт задачу на каждый хост отдельно и указывает идентификатор группы, который позволяет CMS понять, что задача выполняется для нескольких разных хостов. Разные CMS разных проектов получат один и тот же идентификатор группы, но разные `$task_id`.

Когда Wall-E запускает операцию, он создаёт задачу в CMS-API. Когда операция завершена или требуется выполнить другую операцию, Wall-E удаляет старую задачу и создаёт новую. Из-за распределённой природы сервиса, может возникнуть ситуация, когда для одного хоста в CMS-API существует больше одной задачи. Как правило, это означает, что Wall-E не смог удалить старую задачу, прежде чем создал новую – внутри Wall-E всегда существует только одна задача для каждого хоста. Но возможно и такое, что Wall-E запустил несколько разных групповых задач и хочет получить разрешение на проведение какой-то из них.

{% note warning %}

CMS должна корректно работать в ситуации, когда задачи имеют пересекающееся множество хостов. Корректность определяется требованиями к кластеру, это внутренняя логика CMS. С точки зрения Wall-E любой валидный результат будет корректным. Безопасная рекомендация: позволять выполнение задач в порядке их создания, не отклоняя их просто из-за того, что они были созданы позже.

{% endnote %}

### Задачи и действия
Ниже приведены команды CMS на освобождение указанных хостов для того, чтобы Wall-E мог произвести над ними какое-либо действие. Действие задается полем `action` и может иметь следующие значения:
* [prepare](../guide/hosts.md#host-preparing) (для протокола версии 1.1 и позднее)
* [deactivate](../guide/hosts.md#project-switching) (для протокола версии 1.1 и позднее)
* [power-off](../guide/hosts.md#host-powering-off)
* [reboot](../guide/hosts.md#host-rebooting)
* [profile](../guide/hosts.md#host-profiling)
* [redeploy](../guide/hosts.md#host-deploying)
* [repair-link](../automation/algorithm.md#automatic-link-repairing)
* [change-disk](../automation/algorithm.md#automatic-disk-changing)
* temporary-unreachable -- поступило уведомление о плановых работах, приводящих к временной недоступности хоста по сети, без выключения хоста. Обычно это работы на свитче. (для протокола версии 1.4 и позднее)

### Добавление и удаление хоста {#add-and-remove}
Замечание про удаление и добавление хоста: CMS уведомляется о введении хоста в эксплуатацию, а не просто о добавлении в Wall-E. В проект может быть добавлен хост, который выведен из эксплуатации. Если хост добавляется в статусе `free` или переводится из другого проекта с опцией "освободить хост" (`--release`), то CMS не будет уведомляться о добавлении хоста. CMS будет уведомляться только о введении хоста в эксплуатацию и выведении хоста из эксплуатации.

Возможно, один короткий абзац выше выглядит запутанно, поэтому вот длинная, простая и понятная шпаргалка:
* Владелец добавляет в Wall-E хост в статусе `free` (`wall-e hosts add $inv -S free`): CMS не уведомляется
* Владелец добавляет в Wall-E хост в статусе `assigned` (`wall-e hosts add $inv`): создаётся задача с `action: "prepare"`
* Из предзаказа добавляется хост, предзаказ создан без опции `--prepare`: CMS не уведомляется
* Из предзаказа добавляется хост, предзаказ создан с опцией `--prepare`: создаётся задача с `action: "prepare"`
* Для хоста запускается процедура ввода в эксплуатацию (`wall-e hosts prepare $inv`): создаётся задача с `action: "prepare"`
* Владелец проекта переводит хост в другой проект без опции `release`: *CMS не уведомляется* (предполагается, что это "связанные" проекты). Хост не выводился из эксплуатации и не вводился в эксплуатацию, поэтому CMS не уведомляется.
* Владелец проекта переводит хост в другой проект с опцией `release`: создаётся задача с `action: "deactivate"`. Задача создаётся в CMS проекта-источника, хост переходит в статус `free` и либо пройдёт подготовку позднее, либо будет удалён из Wall-E.
* Владелец проекта переводит хост в статусе `free` в другой проект: CMS не уведомляется. В процессе операции хост не выводится из эксплуатации и не вводится в эксплуатацию.
* Владелец проекта удаляет хост в статусе `free` из wall-e: CMS не уведомляется
* Владелец проекта удаляет хост в статусе `assigned` из wall-e: создаётся задача с `action: "deactivate"`

Конечно, надо помнить, что при запуске любой задачи (кроме предзаказов) владелец проекта может указать опцию `--ignore-cms`. Предполагается, что он знает, зачем он это делает. Если указывать эту опцию, CMS уведомлений не получит.


## Известные проблемы протокола, не решённые в текущей версии {#known-issues}
* CMS не имеет информации о том, что починка хоста прошла неуспешно и хост переведён в dead. В качестве решения в данный момент предлагается использовать информацию о статусе хоста из wall-e и использовать при распределении ресурсов только сервера в статусе ready.
* В процессе починки сервера Wall-E может создать новую задачу взамен старой, например, если перезагрузка не помогла, Wall-E создаст задачу на переналивку. При этом старая задача будет удалена из CMS, после этого будет добавлена новая задача. В промежутке CMS может успеть назначить ресурсы сервера какой-то задаче. В качестве решения в данный момент предлагается использовать информацию о статусе хоста из wall-e и использовать при распределении ресурсов только сервера в статусе ready.
* CMS не получает уведомления о переходе сервера в статус invalid (при переименовании сервера). В качестве решения в данный момент предлагается использовать информацию о статусе хоста из wall-e и использовать при распределении ресурсов только сервера в статусе ready.
* CMS получает уведомления только о запущенных в Wall-E задачах. Это значит, что в следующих ситуациях CMS не получит уведомлений о том, что сервера недоступны и не должны учитываться при распределении ресурсов кластера:
  * В Wall-E отключена автоматика (в проекте или глобально). Предполагается, что отключение автоматики происходит при достаточно крупных проблемах, и перераспределение ресурсов при этом может сделать хуже.
  * Для хоста задано ограничение на автоматику в Wall-E (например, запрет на автоматическую перезагрузку). Предполагается, что автоматическое перераспределение ресурсов для таких серверов недоступно.
  * Недоступна вся стойка или более крупный сетевой узел. Для этого сценария требуется проработка.

## Дефолтная CMS {#default-cms}
Дефолтная CMS разрешает любые операции со всеми хостами проекта, но с ограниченной "пропускной способностью" – не более `N` хостов за раз. То есть если ограничение стоит в 5, то Wall-E будет обрабатывать (ребутать/переналивать) не более 5 хостов одновременно.

`N` устанавливается для каждого проекта в отдельности при задании для него дефолтной CMS:
`$ wall-e projects modify-project-cms replace $id --cms default --max-busy-hosts $n`, где `$n` > 0.
Значения < 1 не являются валидными, т.к. CMS тогда не сможет отдавать хосты в работу Wall-E.

`max-busy-hosts` является обязательным параметром для дефолтной CMS. Если при создании проекта не указывать CMS, то будет выбрана дефолтная с `max_busy_hosts = 5`.

Можно рассматривать default CMS в качестве референсной реализации CMS API v1.0:
* [API](https://bb.yandex-team.ru/projects/NANNY/repos/wall-e/browse/walle/views/cms/cms_api.py)
* [модели](https://bb.yandex-team.ru/projects/NANNY/repos/wall-e/browse/walle/cms_models.py)
* [логика](https://bb.yandex-team.ru/projects/NANNY/repos/wall-e/browse/walle/default_cms.py)
* [сборка мусора](https://bb.yandex-team.ru/projects/NANNY/repos/wall-e/browse/walle/cms.py)

## Диагностика проблем {#diagnostics}
Если CMS-API не отвечает на запросы или выдаёт ответы, не соответствующие схеме, приведённой ниже, то Wall-E стремится уведомить об этом владельцев проекта. Уведомления можно получать по нескольким каналам: Juggler (рекомендуемый способ) и почта.

Wall-E отправляет на почту нотификацию с подробным описанием проблемы. Уведомления получат получатели, подписанные на [оповещения с severity error](../guide/notifications.md).

На каждое обращение в CMS-API, успешное и неуспешное, отправляется событие в Juggler. Владельцы сервисов CMS-API могут найти события по своим сервисам [на этой странице](https://juggler.yandex-team.ru/raw_events/?query=service%3Dwall-e-cms-request). Несколько подсказок: Wall-E подставляет в поле `service` значение `wall-e-cms-request`. В поле `host` подставляется имя cms-api, которое создаётся на основе URL, указанного в настройках проекта, нормализованного для того, чтобы соответствовать требованиям к полю host, с префиксом `wall-e.cms.`. Если в вашем проекте указан URL `http://cms.qloud.yandex-team.ru/project/qloud-ext-mtn`, то он превратится в `wall-e.cms.cms.qloud.yandex-team.ru-project-qloud-ext-mtn`. Дополнительно, Wall-E указывает в тегах события:
 * действие, которое Wall-E пытался произвести, например, `tag=wall-e.cms.get_tasks`
 * проект, которому принадлежал хост, для которого производилось действие, например `tag=wall-e.cms.qloud-ext-mtn`
 * имя CMS-API, то же самое, которое попадает в поле host, например, `tag=wall-e.cms.cms.qloud.yandex-team.ru-project-qloud-ext-mtn`
 * версия протокола CMS-API, указанная в настройках проекта, например `tag=wall-e.cms.version.v1.1`

Все эти параметры могут использоваться [для настройки джагглерного агрегата](https://docs.yandex-team.ru/juggler/aggregates/basics), рекомендуемый вариант – использовать `host` и `service`. Настроить агрегат – это просто, вот простейший пример, который можно скопировать в UI (придётся изменить `namespace`, `host` и, опционально, `service` в параметрах верхнего уровня):
```yaml
namespace: my-juggler-namespace
host: my-cms-service
service: wall-e-cms-request
aggregator: logic_and
children:
    -
        host: wall-e.cms.cms.qloud.yandex-team.ru-project-qloud-ext-mtn
        service: wall-e-cms-request
```

Добавить сюда уведомления в telegram, почту, смс или звонком по телефону – можно [по этой инструкции](https://docs.yandex-team.ru/juggler/notifications/basics).
