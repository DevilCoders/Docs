Telepony
================
## Описание проекта
[Wiki](https://wiki.yandex-team.ru/vertis/telepony/)

С помощью этого сервиса можно получить в аренду подменный номер.

Какие задачи решает:
 - Защита пользователей от смс- и телефонного-спама. Защита от парсеров
 - Получение статистики звонков
 - Получение аудио записей звонков

## Для пользователя
### Адреса сервиса
 - [тестинг](http://telepony-api-int.vrts-slb.test.vertis.yandex.net/swagger/?url=/api/2.x/)

### Поддержка
 - [чат в telegram](https://t.me/joinchat/CwwAr03KRoqmmqrFn-nRPA)

### Ответственные за сервис
 - список ответственных - [группа инфры](https://staff.yandex-team.ru/departments/yandex_personal_vertserv_comp_infra_bigdata/)
 - очередь для создания задач - https://st.yandex-team.ru/TELEPONY

## Для разработчика
### Используемые базы данных/хранилища
 - MySQL - основное хранилище. Содержит звонки, номера оператора и историю редиректов.
 - Kafka - пишем операторские события звонков, сырые собранные звонки, команды на touch редиректа, события о созданных редиректах.
 - CouchBase - храним время последнего звонка.

### Полезное
 - [Как мы выбираем номер для редиректа](https://github.com/YandexClassifieds/telepony/blob/master/docs/number_choose.md)
 - [Как заводить новый домен](https://github.com/YandexClassifieds/telepony/blob/master/docs/new_domain.md)


### Процесс разработки и тестирования
#### Для тех кто в первый раз работает с этим репозиторием
 - Не забудь подтянуть сабмодули
   ```
   git submodule update --init
   ```
#### Организация веток в GIT
 1. Хочешь сделать какие-то изменения - ответвляйся от `master`. Хорошо использовать id тикета из [Startrack'а](https://st.yandex-team.ru/) в связке с кратким комментарием о сути изменений для названия ветки. Например, `TELEPONY-123_add_verbose_flag_for_script_running`
 2. Мерджим в `master` **ТОЛЬКО** изменения, которые будут в ближайшее время выкачены в прод (особенно это касается скриптов vox'а). Все версии нужных пакетов выкатились в тестинг - мердж и кати в прод
 3. Собирать релизы можно из любой апрувнутой ветки. Не забудь вмерджить ветку в `master` после выкладки в прод
 4. Ты ответственный за актуальность данных в твоей ветке

#### Форматирование кода
В проекте для этой цели используется [Scalafmt](https://scalameta.org/scalafmt/).
Для использования scalafmt в Idea следуй инструкциям [тут](https://www.jetbrains.com/help/idea/work-with-scala-formatter.html#scalafmt_config), но в `Configuration` нужно указать `infra-common-resources/.scalafmt.conf`.
Если такого файла нет, то нужно [подтянуть сабмодули](#для-тех-кто-в-первый-раз-работает-с-этим-репозиторием)

Если по какой-то причине не получилось настроить форматирование через Idea, то всегда можно использовать `make format` в корне проекта 

#### Как запустить локально
 - Клонируем репозиторий:
   
   `git clone git@github.com:YandexClassifieds/telepony.git`
 - Запускаем скрипт для подготовки локальных конфигов (из корневой директории)
   
   `./preparing_for_local_start.sh`   

 - Про конфиги (Они сгенерятся)
 
   В проекте есть ряд файликов с именем `x.template.conf`, при первом запуске они послужат примером для создания собственных файликов `x.conf`
 - что запускать?
 
   Для запуска локально в каждом компоненте есть файлик Main.
 
#### Как скомпилировать проект
 
  `sbt compile`

#### Как запустить тесты локально

  `sbt test`

  Могут возникнуть проблемы с `Mockito`. Починить проблему можно использовав опцию `-Djdk.attach.allowAttachSelf=true` для запуска тестов. Можно облегчить себе жизнь добавлением этой опции в шаблон для запуска тестов 
 
#### Как выкатить свою ветку в тестинг
0. Ты должен [занять тестинг](#процесс-занятия-тестинга-разработчиком-телепони) для выкатки своих изменений перед тем как делать дальнейшие шаги
1. Находим билды в teamcity с пометкой `[release new]` для нужных компонентов. Пример для [telepony-api](https://t.vertis.yandex-team.ru/viewType.html?buildTypeId=VerticalsBackend_Telepony_ReleaseNewApi)
2. Нажимаем на `...` рядом с `Run`
3. Нажимаем на вкладку `Changes` и выбираем на ней свою ветку в поле `Build branch`
4. Переходим на вкладку `Parameters` и ставим галочку на опции `transient`
5. Нажимаем кнопку `Run build`

После удачного завершения билда будет запущен процесс деплоя твоих изменений в тестинг.
За этим процессом можно наблюдать в jenkins на странице модуля, который ты забилдил. Пример для [telepony-api](https://j.vertis.yandex-team.ru/job/Deploys/job/Telepony/job/testing/job/yandex-vertis-telepony-api/)

#### Как собрать релиз
Для этого необходимо в своей ветке поднять версии у нужных модулей. 
Пример для `telepony-controller`:
```bash
cd telepony-controller 
../infra-common-resources/changes.sh "<release message>"
```
После этого можно пушить свои изменения. Билды в teamcity с пометкой `[release new]` подхватят изменения версии, соберут новую версии и запустят процесс выкатки в тестинг

#### Как выкатить в прод
На странице билда модуля в тестинг в jenkins нужно выбрать необходимую версию (выбрать одну из строчек в `Build History`), нажать `Promotion Status`, нажать `Force Promotion` и все билд в продакшн запущен.
Страница билда для [telepony-api](https://j.vertis.yandex-team.ru/job/Deploys/job/Telepony/job/testing/job/yandex-vertis-telepony-api/)

#### Подготовка скриптов к тестированию
Нужно создать файлы с измененными скриптами из ветки в админке вокса и создать для них свой [роутинг](https://voximplant.com/docs/introduction/introduction_to_voximplant/basic_concepts/programmable_voice_and_video/routing).
Имена файлов должны иметь вид `{script-name}_{ticket-id}_{custom-suffix}`, а имя у правила роутинга должно иметь вид `{ticket-id}_{custom-suffix}`, 
где `script-name` - имя скрипта в котором произошли изменения, `ticket-id` - id тикета из [Startrack'а](https://st.yandex-team.ru/), `custom-suffix` - опциональный суффикс (на случай если по одному тикету не одна ветка).
`app2app_TELEPONY-123_test_first_version` - хорошее имя для скрипта.

#### Процесс занятия тестинга разработчиком телепони
 1. Заходишь в [чат](https://yndx-classifieds.slack.com/archives/C02H2CTGRTJ)
 2. Смотришь не было ли за сегодня сообщений вида `займу тестинг телепони`. Если есть и человек уже освободил тестинг, то идешь следующий шаг. Иначе ждешь когда человек освободит тестинг
 3. Пишешь в чат `займу тестинг телепони`. Лучше пару минут подождать вдруг кто-то будет сильно против
 4. Все ты можешь занимать тестинг, **НО** не забудь после того как закончишь проверять обновить сообщение в чате добавив пометку, что можно занимать тестинг
 
#### Процесс внесения изменений в проект разработчиком команды телепони
 1. Создаешь отдельную ветку. Рекомендации [тут](#организация-веток-в-git)
 2. Делаешь свои изменения в этой ветке
 3. Создаешь pr из своей ветки. Вся команда телепони автоматически будет призвана на ревью
 4. Можно тестировать свои изменения без апрува, **НО** делай это с умом. Лучше спросить по поводу мест в которых сомневаешься чем тестировать, то что придется переписывать. Изменения схемы таблиц лучше оформлять в отдельные pr'ы чтобы можно было быстро их посмотреть и остановить если твои изменения могут что-то сломать.   
 5. [Занимаешь тестинг](#процесс-занятия-тестинга-разработчиком-телепони)
 6. [Подготовь скрипты к тестированию](#подготовка-скриптов-к-тестированию) если это необходимо
 7. Проверяешь изменения. Если нужно что-то исправить, то освобождаешь тестинг, исправляешь и переходишь на 4 шаг. Иначе следующий шаг
 8. Чистишь за собой тестинг если это необходимо - удаляешь созданные роутинг и скрипты
 9. [Занимаешь тестинг](#процесс-занятия-тестинга-разработчиком-телепони) с пометкой, что катишь через него до прода изменения в коде
 10. [Собираешь релиз](#как-собрать-релиз)
 11. [Выкатываешь в прод](#как-выкатить-в-прод)

#### Процесс внесения изменений в проект для остальных
 1. Если нужно протестировать **ТОЛЬКО** изменения скриптов Вокса:
    1. Создаешь отдельную ветку. Рекомендации [тут](#организация-веток-в-git) 
    2. Делаешь свои изменения в этой ветке
    3. Создаешь pr из своей ветки. Вся команда телепони автоматически будет призвана на ревью
    4. Можно тестировать свои изменения без апрува, **НО** делай это с умом. Лучше спросить по поводу мест в которых сомневаешься чем тестировать, то что придется переписывать
    5. [Подготовь скрипты к тестированию](#подготовка-скриптов-к-тестированию) если это необходимо
    6. Проверяешь изменения. Если нужно что-то исправить, то освобождаешь тестинг, исправляешь и переходишь на 4 шаг. Иначе следующий шаг
    7. Чистишь за собой тестинг - удаляешь созданные роутинг и скрипты
    8. После апрува создаешь тикет на выкатку в прод используя [шаблон](https://st.yandex-team.ru/createTicket?queue=TELEPONY&_form=82173). Далее будет создан тикет в котором можно отслеживать статус процесса. Такими тикетами будет заниматься дежурный
 2. Если нужно протестировать изменения скриптов Вокса и внести изменения в код проекта телепони:
    1. Вы скорее всего не хотите делать изменения в коде телепони своими руками, а возможно и в скрипте. Лучше поговорите об этом [чате поддержки телепони](https://t.me/joinchat/kndMVExWzUI4Njcy)

### [Сcылка на тимсити](https://t.vertis.yandex-team.ru/project.html?projectId=VerticalsBackend_Telepony)

### Метрики
[Основной дашбор в Grafana](https://grafana.vertis.yandex-team.ru/dashboard/db/telepony-monitor)

### Алерты
 - [Ссылка на дашборд с алертами в графане](https://grafana.vertis.yandex-team.ru/dashboard/db/telepony-monitoring)
 - [Чатик](https://t.me/joinchat/XjmHOKMbjhcwNmI6), куда падают алерты

### Где смотреть логи

#### ClickHouse
 - [Подробно про условия хранения горячих логов](https://docs.yandex-team.ru/classifieds-infra/logs/quick-start#holodnye-logi)
 - [Пример для telepony-api используя YQL](https://yql.yandex-team.ru/Operations/YVXc25fFtzcrhxq2lUXsTeblC4NIuZOMlMSosYTC848=)
 - [Пример для telepony-api используя Grafana](https://nda.ya.ru/t/a-AdKEe94K6hwH)
 - [Примеры основных запросов логов](https://docs.yandex-team.ru/classifieds-infra/logs/yql-ch)

#### YT
 - [Подробно про условия хранения холодных логов](https://docs.yandex-team.ru/classifieds-infra/logs/quick-start#holodnye-logi)
 - [Пример для telepony-controller используя YQL](https://yql.yandex-team.ru/Operations/YVXdFdjKS6LSKsnvwBX9Q5c0JA20vmZnFmcuUB1MtLs=)
 - [Примеры основных запросов логов](https://docs.yandex-team.ru/classifieds-infra/logs/yql-yt)

### Slow логи mysql
#### Используя yc
Нужно установить и настроить [yc](https://doc.yandex-team.ru/cloud/managed-mysql/quickstart.html)

В проде получить slow логи можно вот так:

``yc managed-mysql cluster list-logs mdbqvo6t466galvh3e2j  --service-type=mysql-slow-query``

Ну или если нужны только сами запросы:

``yc managed-mysql cluster list-logs mdbqvo6t466galvh3e2j  --service-type=mysql-slow-query | jq '.[] | .message.query'``

#### Используя страницу инстанса базы в облаке
На страницы инстанса в облаке есть специальный [раздел с логами](https://cloud.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-mysql/cluster/mdbqvo6t466galvh3e2j?from=1633014360907&to=1633017960907&shortcut=1h&serviceType=MYSQL_SLOW_QUERY&section=logs).
На странице можно выбрать интересующий тип логов