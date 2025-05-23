# Информация для разработчиков и дежурных renderer-бет

_Документация для пользователей находится [здесь](https://doc.yandex-team.ru/si-infra/renderer-betas/general.html)._

## Как реагировать на проблемы

Оценить масштаб, если проблема хотя бы в некоторой степени массовая и не предполагает решаться в ближайшие минуты, следует [завести infra-инцидент](https://wiki.yandex-team.ru/search-interfaces/infra/duty/incidents/#zavedenieincidentov), что позволит проинформировать разработчиков интерфейсов об имеющейся проблеме, поможет предотвратить наплыв обращений в infraduty, и создаст единую точку коммуникации.

## Алерты

Все алерты для сервиса беток и их состояние можно посмотреть на juggler-панели [Renderer Betas Checks](https://juggler.yandex-team.ru/dashboards/renderer-betas).

Источниками сигналов являются renderer-betas-cli, отправляемые в solomon, а также сигналы по статусам тасок sandbox_ci и сигнал из yappy по свободному объему квоты, которые мы берем из yasm. Для последних заведены [шаблоны в infratest](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/infra-yasm-templates/alerts/renderer-betas/template.jinja2).

Часть алертов настроена на заведение SPI при переходе в `CRIT`. Это алерты на [ошибки деплоя](https://juggler.yandex-team.ru/check_details/?host=renderer_betas&service=renderer_betas_cli_create_errors&query=&last=1DAY) и на [размер оставшихся свободных слотов квоты](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drenderer_betas%26service%3Dquota-*).

На данный момент заведение SPI и даже оповещение дежурных при ошибках остановки бет отключено. Причина - [SPPROBLEM-480](https://st.yandex-team.ru/SPPROBLEM-480). Это не влияет на пользователей, но не позволяет полагаться на этот мониторинг. На данный момент решено дождаться переезда покоммитных проверок на new CI, и понять появятся ли простые варианты исправления ситуации в новом мире.

[Проверки уровня статуса тасок](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drenderer_betas%20%26%20service%3Dsandbox_ci_*) служит как last-resort механизм оповещения, когда до вызова нашей утилиты renderer-betas-cli дело не доходит. По ним SPI не заводятся, поскольку они скорее сигнализирует о проблемах в вышестоящей инфре, но при их массовом возгорании, следует ознакомиться с причиной.

## Разбор SPI

Беты находятся в тире C. Это означает, что от них ожидается определенный уровень надежности, который определяется высокой долей "решенности" возникающих инцидентов. Решенными в терминах warden считается инцидент, по которому заведен хотя бы один action item, а также высокая доля закрытых среди них (следует целиться как минимум в показатель 50%).

В конце каждого семестра по накопленному за его время отчету выносится вердикт, соответствует ли сервис присвоенному ему тиру. Показатели за текущий семестр можно смотреть на [страничке с отчетом в warden](https://warden.z.yandex-team.ru/components/renderer-betas/report?filter_type=incidents&filter_status=total&filter_period=&filter_ignored_status=&custom_metric=&filter_resolved=false&text_filter=).

Исходя из вышесказанного, необходимо стремиться каждый SPI разбирать. Заводить по нему релевантные action item'ы или линковать существующие. Для каждого SPI обязательно заполнять раздел `Описание`. Для беток мы не считаем YDT, поскольку они являются внутренним сервисом. Дежурному следует решать возникающие action item'ы, если они не мешают поддержке прода и нет более приоритетных action item'ов и задач.

## Диагностика проблем

### Ошибки поднятия беты

#### 1. Узнать идентификаторы упавших sandbox-тасок

Первым шагом диагностики проблем поднятия беты является определение идентификаторов упавших тасок.

На странице [алерта](https://juggler.yandex-team.ru/check_details/?host=renderer_betas&service=renderer_betas_cli_create_errors&query=&last=1DAY) в правом верхнем углу есть ссылка на ["График мультиалерта"](https://solomon.yandex-team.ru/?project=fei&cluster=sandbox&service=renderer_betas&sensor=beta-create-error&graph=auto&interpolate=none&l.task=*)

##### Интерфейс solomon

![Default solomon interface](https://jing.yandex-team.ru/files/slava-b/2021-05-25T13%3A08%3A03Z.png)

Под графиком в табличке можно увидеть список идентификаторов упавших тасок. У тасок в выбранный на графике период будет sum > 0.

![task id](https://jing.yandex-team.ru/files/rmdm/task-id.png)

Если solomon не может отобразить график, это может означать, что слишком много точек доступно для отображения, в этом случае можно попробовать дополнительно пофильтровать сигналы по метке task, указав префикс sandbox-идентификаторов интересного периода. Обычно достаточно первых 3-х цифр, например:

![task label prefix](https://jing.yandex-team.ru/files/rmdm/task-label.png)

##### Интерфейс monitoring
Если [включить новый интерфейс](https://solomon.yandex-team.ru/admin/preferences), то графики solomon будут редиректить на monitoring.
![monitoring interface](https://jing.yandex-team.ru/files/slava-b/2021-05-25T13%3A16%3A27Z.png)

Переключаемся на "Легенду", сортируем по Last, выбираем нужные task id
![task id](https://jing.yandex-team.ru/files/slava-b/2021-05-25T13%3A18%3A36Z.png)

##### Sandbox
Переходим в таски для дальнейшей диагностики: `https://sandbox.yandex-team.ru/task/<id>`.

#### 2. Получить идентификатор беты

В зависимости от запускавшей таску системы CI вид странички может отличаться, но в любом случае на ней можно будет найти идентификатор ветки/пулл-реквеста, по которому собиралась таска. Берем этот идентификатор, и находим по нему релевантную бету в [yappy](https://yappy.z.yandex-team.ru/b):

![Beta by id](https://jing.yandex-team.ru/files/rmdm/beta-id.png)

Если бета не нашлась, это тоже промежуточный результат дебага, который может понадобиться нам в дальнейшем.

#### 3. Найти причину

Следует зайти в логи деплоя в sandbox, здесь можно увидеть разное:

- В логах сразу может быть видна очевидная причина проблемы, тогда все понятно.
- Если таска упала по таймауту с 404-и при опросах статуса - вероятно это [SPPROBLEM-480](https://st.yandex-team.ru/SPPROBLEM-480), следует удостовериться, что при этом беты нет в yappy, а связанный пулл-реквест уже закрыт/вмержен.
- Если таска упала по таймауту и при опросах видны только статусы `OUTDATED` - это верный повод идти в чат [Priemka support](https://t.me/joinchat/Gof_DRYqECUTxO2mUn4ytQ).
- Если таска упала по таймауту со статусами `INCONSISTENT` - здесь не все так однозначно, проблема может быть и в yappy и в nanny, а может и в чем еще. Здесь следует пойти на страничку беты в yappy и ознакомиться с ошибками. Если по ним причина проблемы не очевидна, можно перейти по ссылкам на fqdn слотов данной беты, и посмотреть на состояние няни, не завис ли деплой в ней и нет ли сообщений об ошибках. Одной из причиной зависаний в няне может быть и битый архив, это еще один [SPPROBLEM-472](https://st.yandex-team.ru/SPPROBLEM-472), проблема возникает редко, поэтому сейчас ее приоритет понижен. Если проблема с зависанием не в битом архиве (можно понять по логам курьера), возможно потребуется писать в [RTCSUPPORT](https://t.me/joinchat/Be0kOD50fVxMoi_8hPvG6Q). Если в няне проблем не видно, это повод обратиться за помощью в чат [Priemka support](https://t.me/joinchat/Gof_DRYqECUTxO2mUn4ytQ).
- Если ничего не понятно, стоит сходить в чат [Priemka support](https://t.me/joinchat/Gof_DRYqECUTxO2mUn4ytQ).

По результатам диагностики следует [разобрать](#razbor-spi) связанные SPI.

### Закончилась квота

Алерт загорается при достижении критического значения в 5 свободных слотов, чтобы у дежурного был некоторый запас на реагирование и уменьшение последствий для пользователей. В первую очередь необходимо понять характер расходования квоты. Узнать об этом можно из графиков, служащих источниками для [соответствующих алертов](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Drenderer_betas%20%26%20service%3Dquota-*).

Если квота кончилась достаточно быстро, нужно определить источник повышенного потребления квоты и устранить его. Следует ориентироваться на свежие деплои, и из них выделить идентификаторы ревью-реквестов (по ид беты) / сэндбокс ресурсов (по патчам в изменениях) с релевантным источником потребления. В качестве экстренных мер может потребоваться ручное удаление бет в проблемной квоте, для которых ttl в ближайшее время и так истечет.

Если квота кончилась не одномоментно, а постепенно снижалась до критических значений, это признак того, что рост органический и требуются дополнительные ресурсы. Здесь может потребоваться связаться с представителями релевантного квоте сервиса и договориться о выделении железа. Если квота общая, еще одной возможной причиной может быть заезд крупного потребителя, который не рассказал о своем уровне потребления. В этих случаях также может потребоваться ручное удаление бет, которые близки к исчерпанию своего ttl, либо бет релевантного сервиса.

Известным потребителем, который выделял железо для покрытия части расхода квоты своих бет, является ydo ([тикет](https://st.yandex-team.ru/FEI-22843)). В случае потребности дальнейшего расширения квоты следующим по объему потребителем являются новости (news + sport), у которых, например, есть квота nerpa, которая, похоже, сейчас не используется. Возможно, это может быть следующим источником для расширения.

Также причиной могут быть ошибки в конфигурации сервисов, например, если на уровне сервиса забыли прописать скрипты остановки бет при закрытии пулл-реквеста. О таком догадаться можно по большому числу пулл-реквестов от совсем свежего сервиса (определить можно по [подобному графику](https://solomon.yandex-team.ru/?project=fei&cluster=sandbox&service=renderer_betas&graph=auto&interpolate=none&l.task=-&l.sensor=beta-create-ok&l.quota=report-renderer-templates&l.component=renderer-ydo-erp*&b=2021-06-08T12%3A00%3A35.000Z&e=2021-06-28T18%3A00%3A35.000Z), подменяя необходимым образом квоту и компонент).

Альтернативой удалению наиболее старых бет из квоты может быть заведение нового слот-сервиса под этой квотой, возможно, на временном железе. Для этого потребуется провести сходные действия из пунктов 5-7 раздела [про создание новой квоты](#sozdanie-novoi-kvoty), только в генераторе потребуется просто поправить число слот-сервисов, а также в яппи не заводить новую квоту, а обновлять существующие (основная + реплика, при наличии).

Если отвалился механизм удаления бет для закрытых PR, то можно запустить [скрипт для очистки](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/yappy-garbage-collector) вручную:
```shell
npx @yandex-int/yappy-garbage-collector --quota report-renderer-templates --owner search-interfaces --repo frontend
```
Не забудь указать правильную квоту. Если для проекта нет github, то соотвтствующие опции указывать не нужно.

По результатам диагностики следует [разобрать](#razbor-spi) связанные SPI.

### Деплой прошел, а бета недоступна

На такой случай у нас на данный момент не заведено алертов, и сигнал о такой проблеме, вероятно, может поступить из infraduty.

Следует ознакомиться с логами аппхоста, добавив к запросу `dump_eventlog_only=1`. Если читать сырой лог затруднительно, здесь же можно взять из него reqid и перейти в [setrace](https://setrace.yandex-team.ru).

Ряд примеров:

- [Бета недоступна из-за особенностей графа](https://st.yandex-team.ru/INFRADUTY-13948#5fc4cc8c23d4752cbe2349f2)
- [У конкретного пользователя состояние кук повлияло на доступность беты](https://st.yandex-team.ru/INFRADUTY-15848#606704ea2e469c397d913ffe)

### Ошибка `components have different parent ids`

Необходимо некоторое вступление. Яппи для каждой беты хранит указание, в какие компоненты (и, соответственно, квоты) бета должна быть выложена, а также, из каких конфиг-сервисов брать базовую конфигурацию для каждого компонента ([пример](https://yappy.z.yandex-team.ru/b/renderer-web4-dev/json), здесь у каждого компонента указана квота, и у каждого патча - конфиг-сервис из которого берется конфигурация). В случае, если появляются такие беты, в которых соответствие квот и конфиг-сервисов отличается от уже существующих, в интерфейсе яппи на главной странице беты появляется указанная ошибка и беты перестают приезжать в указанные квоты.

Пример сломанной беты: ![Broken beta](https://jing.yandex-team.ru/files/rmdm/2022-02-10T12:51:25Z.fb6da5a.png)

Ее сломанность определяется именно тем, что есть другие беты, которые имеют другое соотношение квота - конфиг-сервис. В данном случае отличается от остальных бет то, что для квоты `report-renderer-serp` в остальных бетах используется конфиг-сервис `betas-configuration-serp`, а с конфиг-сервисом `betas-configuration` обычно разворачивают беты в квоте `report-renderer-templates`.

Как лечить - необходимо найти зловредные беты, которые неожиданным образом поменяли это соотношение, и остановить их через кнопку stop внизу в левом меню в интерфейсе яппи в каждой бете (на скриншоте выше видно, что бета deallocated, т.е. была остановлена), тогда яппи перестанет пытаться заливать конфигурацию из 2 конфиг-сервисов в слоты одной квоты, и ошибки постепенно пройдут (яппи разгребает операции с бетами в рамках очередей). Также необходимо найти источник таких изменений и необходимым образом устранить их появление.

Раньше такая ошибка возникала из-за того, что в renderer-betas-cli такая ситуация никак не обрабатывалась, но после [FEI-24732](https://st.yandex-team.ru/FEI-24732) вероятность возникновения таких ошибок существенно сокращена.

## Создание новой квоты

Пользователи могут к нам прийти с пожеланием завести новую квоту, основываясь на [данной доке](https://doc.yandex-team.ru/si-infra/renderer-betas/quotas.html). В таком случае, нам нужно провалидировать обращение, удостоверившись, что общая квота `report-renderer-templates` для команды не подходит. Здесь также следует учитывать, что переиспользовать общую квоту вне рамок [монорепы frontend](https://a.yandex-team.ru/arc_vcs/frontend) нельзя из-за [текущей реализации шедулера](https://st.yandex-team.ru/FEI-16587#5f1739a97326c13370bc1420), который в таком случае будет удалять беты других реп. Вероятно, стоит пофиксить шедулер, но пока не требовалось.

Если принято решение, о необходимости заведения новой квоты:

1\. Создаем в няне новый конфигурационный сервис.

 Для этого сервиса не нужно железо, он используется яппи для референсной конфигурации слот-сервисов. Рекомендуется скопировать существующий конфиг-сервис, например [betas-configuration](https://nanny.yandex-team.ru/ui/#/services/catalog/betas-configuration):

 - Имя - `betas-configuration-<smth>`
 - Категорию - `/search-common/renderer/betas`
 - abc - [сервис бет](https://abc.yandex-team.ru/services/report-renderer-betas/).
 - Описание - `RR Betas Configuration Service for <smth>`
 - Не забываем установить флажок `Copy authorization attrs`

 После создания сервиса следует подменить файл для `push-client.yml`, на сходный с таковым для прода данного сервиса, но подменить в нем префикс топиков на `hamster/`.

 Поскольку для данного сервиса не предполагается наличие подов, и он никогда не будет переходить в `online`, в какой-то момент вам придет тикет о неиспользуемом сервисе, который при отсутствии реакции будет удален. Следует в тикет отписать, что сервис нужен для конфигурирования yappy-бет.

 Убедитесь, что в `Scheduling policy` стоит `Service scheduling policy` `Maintain active trunk` и не стоит `Force active trunk`, так как при последней политике на большом количестве снепшотов вытесняется тот, в котором есть active-под.

 Все настройки Files и Instance Spec следует производить только в конфигурационном сервисе, а не слот-сервисах. Например, права доступа придётся выдавать на каждый слот-сервис отдельно. При этом и в Instance Spec находились кусочки, которые не синхронизировались. Будьте аккуратны и несите баг-репорты в yappy.

2\. Идем в [соответствующий раздел генератора](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/renderer-service-generator/src/services/betas), и заводим для новой квоты необходимую конфигурацию конфигурационного сервиса.

 Из нетривиальных вещей:

 - Опцию push-client `topicSecret` устанавливаем как в продакшене соответствующего сервиса.
 - Если необходимо более 40 контейнеров потребуется завести обращение, [типа такого](https://st.yandex-team.ru/RTCSUPPORT-9453), с просьбой поднять лимит и на конфиг сервис и на сервисы со слотами.
 - Дополняем конфигурацию кастомизациями, которые запросили пользователи, при необходимости.
 - Не забываем в конфигурации указать необходимое количество слот-сервисов, оно понадобиться в дальнейшем при конфигурации yappy-квот, а также название квоты, что-то типа `report-renderer-<smth>`.

 Количество слотов определяется так - в среднем на 20-30 бет без репликации требуется 1 ядро, 40 Гб памяти, 175 Гб hdd и 15 Мб/с hdd io. Соответственно, нужно понять, какие максимальные возможные значения активного потребления (с учетом ttl) ожидаются от сервиса и добавить сверху хотя бы четвертинку;

3\. Обновляем конфиг-сервис генератором с помощью свежесозданной конфигурации.

 В случае необходимости кастомизировать переменные окружения из секретницы это может потребоваться сделать более итеративно: сначала обновить без секретов, затем пойти в сервис и вручную прописать в каждый контейнер, прописать в генератор и еще раз обновить.

4\. Заводим новый сетевой макрос для квоты

 Руководствуемся [инструкцией](https://wiki.yandex-team.ru/NOC/newnetwork/hbf/projectid/project-id-allocation/#opisanieformy). Все макросы для всех квот можно посмотреть в [racktables](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_RENDERER_BETAS_NETS_).

5\. Далее заводим необходимое число слот-сервисов и их реплик.

 Каждый из слотов должен заканчиваться на его номер, начиная от 1. Можно скопировать существующие, все равно яппи для слот-сервисов стащит конфигурацию у соответствующего конфиг сервиса, поэтому усердстововать с ручными действиями здесь не следует.

 Реплики следует называть следующим образом: если основной слот-сервис называется, например, `renderer-betas-1`, то реплика будет называться `renderer-betas-replica-1`. На это соглашение полагается генератор.

 Если вы хотите отличать сервисы от остальных, не забудьте поменять теги инстансов, в частности prj.
 Если вы поменяли prj, не забудьте внести его в [мониторинги](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/infra-yasm-templates/alerts/report-renderer/template.jinja2?rev=r8127778#L1456) и добавить [панель](#paneli-sostoianiia-razlichnykh-kvot).

6\. В каждом сервисе заводим по поду.

 Наши беты живут в `SAS`, `MAN` и `IVA`, и, пожалуй, заводить в других ДЦ без веских причин не следует. Обязятельным условием является отсутствие подов из одного и того же ДЦ между всеми подами слот-сервисов основной квоты и слот-сервисов квоты-реплики. Для всех подов не забываем указать свежесозданный сетевой макрос. С заведением дырок заинтересованному сервису можно сразу же посодействовать.

 Если потребуется добавить сервис с подами в новом ДЦ, придется этот ДЦ прописать в [infra](https://infra.yandex-team.ru/services/2467/environments) бет, а также в сервисе [uchenki](https://uchenki.yandex-team.ru/settings/service/renderer-betas).

 Не забываем прописать новый под в instances и активировать сервис.

7\. Заводим квоты (основная + реплика) в яппи.

 Для этого вызываем команду генератора:

 ```sh
    npm run --silent cli -- slots -s <название конфигурационного сервиса> > slots.json
 ```

 В `slots.json` под ключем, соответствующим конфигурационному сервису будет массив из 2-х элементов, каждый элемент - отдельная квота, являющаяся репликой для второй. Копируем каждую из квот в форму создания квоты на [странице квот](https://yappy.z.yandex-team.ru/q) в интерфейсе yappy:

 ![New quota](https://jing.yandex-team.ru/files/rmdm/new-quota.png)

Готово! Можно сообщать сервису о названии квоты, сетевом макросе. Дальше уже их дело прописать это в конфиг, возможно, прописать нужные доступы, и начать поднимать беты.

## Изменение квоты

Пользователи могут прийти в infraduty с просьбой поменять квоту для своих бет.

В случае, если требуется новая квота, то предварительные шаги аналогичны [созданию новой квоты](#sozdanie-novoi-kvoty).

Когда у нас есть исходная квота, из которой проект хочет выехать, и новая, необоходимо проделать следующие шаги:

1. В конфиге проекта поменять квоту на новую. Для примера допустим, что [квоту `report-renderer-templates` в проекте jobs](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs/.config/deploy/config.json?rev=r8765230#L8) решили поменять на `report-renderer-jobs`. Желательно, чтобы второй шаг выполнился сразу после этого (влития правки квоты в основную ветку проекта, тогда у существующих пулл-реквестов сразу будет возможность отребейзиться, когда они начнут видеть у себя ошибки несовпадения квоты).
2. В конфигурации шаблона в yappy, который определяется по [id из конфига](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs/.config/deploy/config.json?rev=r8765230#L7) - в примере это был бы [renderer-jobs](https://yappy.z.yandex-team.ru/templates/renderer-jobs), необходимо поменять упоминания квот в компонентах на нужные. В нашем случае это были бы `report-renderer-jobs` и `report-renderer-jobs-replica`.
3. После смены квоты ожидаемы падения бет в пулл-реквестах, до которых изменения в конфиг еще не проросли. Необходимо силами разработчиков сервиса либо отребейзиться, либо внести необходимые правки в пулл-реквесты.

## Учения по закрытию локаций

Бетам renderer присвоен тир C, который подразумевает проведение регулярных сервисных учений. Для бет из ряда различных видов учений имеет смысл проводить учения на закрытие локаций средствами hbf.

Для renderer-betas в сервисе uchenki заведен [сервис](https://uchenki.yandex-team.ru/settings/service/renderer-betas), который сопоставляет в каких ДЦ присутствуют беты, какому warden-компоненту он соответствует, а также какой тип учений для него проводится.

Тип учений также заведен кастомный - [renderer_betas_closing](https://uchenki.yandex-team.ru/settings/type/renderer_betas_closing). Здесь определяется частота, длительность и прочая конфигурация окружения учений.

Периодичность автоматических учений - Раз в две недели, по вторникам с 13:30 по 14:30. Изменять периодичность следует на [странице учений](https://uchenki.yandex-team.ru/settings/type/renderer_betas_closing) (после изменений стоит проверить что ссылка на телеграм чат сохранилась: [Баг: При изменении учений в ученьках слетает ссылка на tg-чат](https://st.yandex-team.ru/UCHENKI-305)). Возможно ручное проведение учений через создание события на [странице событий renderer-бет](https://infra.yandex-team.ru/services/2467/events) и [ручное закрытие макроса HBF](#ruchnoe-zakrytie-makrosa-hbf).

### Как проводить учения

1\. Беты должны находиться в стабильном состоянии, не должны гореть, общеяндексовых учений/работ в этот момент не должно происходить. Узнать о них можно в [соответствующем чате](https://t.me/joinchat/PaZhvX5pm5phcPFN). Если в данный день проходят общеяндексовые учения в том же ДЦ, допустимо учения отменить.

2\. В стартреке в очереди FEI будет заведен тикет с тегом [`closing:renderer-betas`](https://st.yandex-team.ru/issues/?tags="closing%3Arenderer-betas"), в котором будет указан ДЦ, в котором следует проводить учения. Исполнителем будет назначен [текущий дежурный](https://abc.yandex-team.ru/services/reportrenderer/duty/) сервиса reportrenderer. Также, появится событие в infra на [странице событий renderer-бет](https://infra.yandex-team.ru/services/2467/events). В телеграм канал [RRReactions](https://t.me/joinchat/SLACGcw7eWuNt_8G) придет предложение закрыть макрос HBF в конкретном ДЦ.

3\. Дежурный имеет право подвинуть учения в любой момент, в том числе и до получения нотификации в телеграм. Для этого можно попросить перенос [у дежурных ученек](https://supportboard.yandex-team.ru/SPISUPPORT?search=[uchenki]), либо провести вручную.

4\. Перед началом нужно зайти в [yappy](https://yappy.z.yandex-team.ru/b), и на странице бет пофильтровать беты, начинающиеся с `renderer-`. Запомнить количество тех, которые висят в `INCONSISTENT` (желтый кружочек).

5\. Для начала учений нажать "Подтвердить" на сообщении бота в телеграм-канале [RRReactions](https://t.me/joinchat/SLACGcw7eWuNt_8G), либо [закрыть макрос HBF вручную](#ruchnoe-zakrytie-makrosa-hbf). Потенциальные баги ученек, с которыми можно столкнуться: [не закрывается infra событие](https://st.yandex-team.ru/UCHENKI-308), [Повторное оповещение о подтверждении показывает неправильное время старта учений](https://st.yandex-team.ru/UCHENKI-306)

6\. Подождать 5 минут, пока правило доедет до хостов.

7\. Пронаблюдать за поведением бет:

 - Вернуться в [yappy](https://yappy.z.yandex-team.ru/b) и сравнить количество бет (начинающихся с `renderer-`) в состоянии `INCONSISTENT` с их количеством до начала учений. Количество может несколько увеличиться при начале учений, но затем (в течении 10 минут) должно вернуться к изначальному.
 - Определить затронутые проекты по [списку сервисов в ДЦ](https://nanny.yandex-team.ru/ui/#/services), отфильтровав сервисы по строке `betas` и сгруппировав по метке `geo`:

![Beta replicas](../renderer-betas/images/beta-replicas.png)

 - Найти среди бет для затронутых проектов такую, для которой одна из реплик размещается в закрытом ДЦ, она должна быть покрашена в красный, а вторая - в зеленый, при этом статус беты должен быть `CONSISTENT`, вкладка [components](https://yappy.z.yandex-team.ru/b/renderer-web4-dev/components):

 ![Beta replicated components](https://jing.yandex-team.ru/files/rmdm/comps.png)

 - Убедиться, что компонента, прокрашенная в красный, имеет неуспешную проверку `hashring.CheckHashringConfig` с текстом ошибки `ConnectionError`. На это завязана [такая проверка](https://a.yandex-team.ru/svn/trunk/arcadia/frontend/projects/infratest/packages/renderer-betas-cli/src/betas.ts?rev=r9670412#L248) при деплое бет. Также новые деплои в условиях потери ДЦ будут триггерить [такой алерт](https://juggler.yandex-team.ru/project/report-renderer/aggregate?host=renderer_betas&service=renderer_betas_cli_dc_outage_deploy&project=report-renderer).

 ![Beta main page on dc outage](https://jing.yandex-team.ru/files/rmdm/2022-07-06T14:08:25Z.9aa9905.png)
 ![Beta component check page on dc outage](https://jing.yandex-team.ru/files/rmdm/2022-07-06T14:07:16Z.4f4c17e.png)

 - Если обе компоненты красные, убедиться, что эта бета просто только что начала обновляться. Для этого зайти в историю беты, там должны быть события, которые повлияли на передеплой беты.
 - Если последнее событие было более часа от текущего момента, и бета все равно в `INCONSISTENT`, следует [продиагностировать причину проблемы](#3-naiti-prichinu), и, если причина проблемы не становится понятной, написать о проблеме в чат [Priemka support](https://t.me/joinchat/Gof_DRYqECUTxO2mUn4ytQ).
 - Попробовать позаходить на беты, в которых одна из компонент красная. Соответствующий пулл-реквест можно найти по урлу беты, в нем должен быть указан номер ревью-реквеста, который следует прописать в ссылку `https://a.yandex-team.ru/review/<id>`. На странице описания пулл-реквеста должны быть инструкции по заходу на бету. Попробовать снять трейс запроса, в сетрейс должны быть видны перезапросы:

 ![Beta reask](../renderer-betas/images/beta-reask.png)

8\. Если начался пожар, учения следует прекратить, для этого нужно выполнить одно из двух:

- Нажать кнопку "Прервать" в сообщении бота в случае автоматического закрытия HBF.
- Если предыдущий пункт не сработал, либо HBF закрывался вручную - зайти на [страничку заведения учений](https://firewall.yandex-team.ru/drills), на строчке наших учений нажать edit и в открывшейся форме нажать "Cancel drills":
  ![Cancel drills](https://jing.yandex-team.ru/files/asterx/hbf-cancel.png).

9\. Если все выглядит хорошо, дожидаемся окончания учений, hbf открывается автоматом по истечении времени.

10\. По окончании учений отчитаться через [форму](https://forms.yandex-team.ru/surveys/46647/) с описанием проблем и указанием связанных тикетов, если были, [пример тикета](https://st.yandex-team.ru/DRILLS-405).

11\. На следующий день результат должен будет прорасти на [общий дашборд учений](https://datalens.yandex-team.ru/inks4xbmmnwid-dashbord-po-ucheniyam?tab=98).

### Ручное закрытие макроса HBF

1\. Пройти по [ссылке](https://firewall.yandex-team.ru/drills/add).

2\. Заполнить форму: указать макрос (в поле "Projects") `_RENDERER_BETAS_NETS_`; ДЦ, в котором проводятся учения, взять из тикета; длительность проведения учений, около 60 минут, чтобы заканчивалось через час от нотификации в телеграм; в качестве времени начала указываем текущую дату и текущее время. В поле "Тикет" указать тикет из очереди FEI. ![Schedule new hbf](https://jing.yandex-team.ru/files/asterx/hbf.png)

3\. Нажать Submit. После этого можно продолжать с 5\. пункта [инструкции учений](#kak-provodit-ucheniia).

## Разное

### Панели состояния различных квот

- [frontend](https://yasm.yandex-team.ru/panel/flack.betas-compaction)
- [serp](https://yasm.yandex-team.ru/panel/flack.betas-compaction-serp)
- [serp vip](https://yasm.yandex-team.ru/panel/flack.betas-compaction-serp-vip)
- [fiji](https://yasm.yandex-team.ru/panel/flack.betas-compaction-fiji)
- [nerpa](https://yasm.yandex-team.ru/panel/flack.betas-compaction-nerpa)
- [turbo](https://yasm.yandex-team.ru/panel/flack.betas-compaction-nerpa)
- [chat](https://yasm.yandex-team.ru/panel/flack.betas-compaction-chat)
- [pcode](https://yasm.yandex-team.ru/panel/rmdm.betas-compaction-pcode)

### Логи в yt

Пример - https://yql.yandex-team.ru/Operations/XjQUxp3udj6-Lr8GveYUt4O-Gazr8vgCW_JN9iO55PU=

### Stoker-запись для 404 страницы

https://stoker.z.yandex-team.ru/TAGGED/00020-regexp-renderer

Если запись не сработала: посмотрите в SETrace, как называются источники с шаблонами в графе.
Возможно, таких имён пока нет в stoker-записи: проверьте JSON в заголовке %%X-Yandex-Internal-Flags%%.

![](https://wiki.yandex-team.ru/search-interfaces/infra/new-betas/.files/2020-01-1016-30-33.png)

Сервис в няне, который отдаёт 404 шаблоны: https://nanny.yandex-team.ru/ui/#/services/catalog/betas-404/
