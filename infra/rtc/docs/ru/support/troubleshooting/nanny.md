# Системы управления сервисами (Nanny)
## Не создаётся таскгруппа {#tsckgrp-create-fail}
В случае, если модифицируются или создаются рецепты на выкладку и активацию снапшотов есть шанс увидеть на ошибку "Taskgroup creation failed: Failed to find recipe \<recipe name\>".
Тогда необходимо проверить наличе рецептов в панели Recipes, а так же, то, что указанные рецепты выставлены в Scheduling policy.

## У меня не выкладывается сервис {#deploy-fail}
Перед чтением ответа на этот вопрос нужно ознакомиться с [документацией по Nanny](https://wiki.yandex-team.ru/runtime-cloud/nanny/). И конкретно [HOWTO про управление сервисами](https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/).

Деплой сервиса может ломаться на разных стадиях. Чтобы понять, что именно сломалось, нужно открыть сервис и посмотреть в каком состоянии находится обрабатываемый снэпшот. Значения различных состояний **необходимо** прочитать в [документации](https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#service-state-management).

Варианты стадий, на которых может возникнуть проблема:

* [GENERATING](./nanny.md#generating-fail)
* [PREPARING](./nanny.md#preparing-fail)
* [ACTIVATING](./nanny.md#activating-fail)
![2017-10-2618-59-30.png](_assets/2017-10-2618-59-30.png)

В любом случае диагностику нужно начать с просмотра статуса задач в таскгруппе снэпшота (таскгруппу можно найти на скриншоте выше). Подробнее о таскгруппах можно почитать в [документации по рецептам](https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/alemate/yaml-recipes/). Таскгруппа представляет собой граф задач:

![2017-10-2619-17-22.png](_assets/2017-10-2619-17-22.png)

Чтобы понять, что именно происходит в таскгруппе нужно открыть соответствующий таск и посмотреть его состояние. Также будет полезно почитать лог таска:
![2017-10-2619-31-16.png](_assets/2017-10-2619-31-16.png)

Если проблема с одним из конкретных инстансов, информацию про него можно посмотреть в UI инстанса:
![2017-10-2619-42-26.png](_assets/2017-10-2619-42-26.png)
![2017-10-2619-45-33.png](_assets/2017-10-2619-45-33.png)

## Выкладка зависла на стадии GENERATING {#generating-fail}
Нужно открыть таск генерации конфигурации. Как это сделать, рассказано [выше](./nanny.md#deploy-fail). Нужно внимательно посмотреть на сообщение об ошибке в таске.
Популярные проблемы:

* Превышена квота под хранения вольюмов снапшота: `Result: FAIL: Cannot generate configuration mt_front-blue-unified--bluemarket-5587_d50e2737_sas-1568802163727: Cannot create configuration mt_front-blue-unified--bluemarket-5587_d50e2737_sas-1568802163727: Total rootfs + work_dir quota for all shapshots: 24576.0 MiB. RootFS + WorkDir volume quota in YP disk volume request: 18432.0 MiB. 24576.0 MiB > 18432.0 MiB.` Такая ситуация возникает, если неправильно настроена Cleanup Policy или последние несколько снапшотов зависли в статусе "Deactivate Pending" (снапшоты зависают в таком состоянии если было несколько неудачных выкладок подрят, которые не смогли по каким-то причинам перейти в статус ACTIVE). Генерация завершится успешно, если удалить ненужные снапшоты.
* У пользователя протух ресурс в sandbox: `Cannot generate configuration testing_tarantino_sas-1507794755365: Sandbox task 141043564 does not have a resource of type MARKET_TARANTINO_DATA`. Нужно собрать новый ресурс и прописать его в сервисе, желательно выставить у него TTL побольше, чем в прошлый раз, чтобы он не протухал.
* Медленно отвечает CMS. В логе таска будет множество запросов в CMS. В большинстве случаев сервисам не нужны заглушки в CMS, но есть исключения, поэтому мы не можем выключить их всем. При тормозах CMS нужно [выключить в сервисе создание заглушек в CMS](https://wiki.yandex-team.ru/runtime-cloud/nanny/howto-manage-service/#cms-stubs). Если сервис не может выключить заглушек в CMS, то мы ничем не можем помочь, сервис должен учиться жить без них.

## Выкладка зависла на стадии PREPARING {#preparing-fail}
Популярные проблемы:

* Инстанс в состоянии `TIME_LIMIT_VIOLATION`. Обычно это означает, что повис `prepare_script` в instancectl или instancectl его бесконечно рестартит и он не может успешно завершиться. Нужно посмотреть, какой именно скрипт падает в директории инстанса в `loop.log.full` и stderr этой секции в одном из `.err` файлов в директории инстанса.
* Инстанс очень долго в состоянии `ENTITY_RESOURCES_NOT_READY`. Варианты:
* На хосте перегружен диск. Отдиагностировать это можно с помощью `atop`:
`(bash)atop -dD -r /var/log/atop/atop.log # -b 18:20`.
* Недоступен ресурс в sandbox. Какой именно ресурс можно посмотреть в UI инстанса в поле `Last state` или в логе агента `/db/iss3/iss-agent.log` на хосте. Нужно попробовать скачать этот ресурс на другом хосте и на том же хосте руками, дальше или чинить проблему на данной машине, или искать ещё где-то. `sky get -wup rbtorrent:6ddafb5a0261c1f5b05660d09ce732600a22f5aa`
* На хосте поломан фастбон. Это гарантированно так, если не получается попинговать себя: `ping6 fb-sas1-1010.search.yandex.net`.
* На хосте кончилось место. Прямо сейчас у нас нет изоляции по диску, поэтому нужно искать того, кто загадил хост и сносить данные руками.
* ISS рапортует статус `ENTITY_RESOURCES_NOT_READY`, хотя ресурсы скачались, и долго выполняется выполняется `iss_hook_install` [https://st.yandex-team.ru/ISS-3801](https://st.yandex-team.ru/ISS-3801) См. выше про `TIME_LIMIT_VIOLATION`.
* Другие возможные причины: [https://wiki.yandex-team.ru/runtime-cloud/rtc-support/#cannot-download-resource](https://wiki.yandex-team.ru/runtime-cloud/rtc-support/#cannot-download-resource).

## Выкладка зависла на стадии ACTIVATING {#activating-fail}
Конкретную проблему нужно искать в логах инстанса в файлах `loop.log.full`, `anamnesis.log`, `*.err`, `*.out`.
В файле `loop.log.full` можно найти секцию, проверка статуса которой завершается неудачей, и после идти смотреть содержание `*.err` и `*.out` файлов этой секции.
Популярные проблемы:

* `HOOK_SEMI_FAILED`. Означает, что проверка статуса инстанса завершается неуспешно. Способ проверки статуса инстанса задаётся параметром `status_script` в instancectl.conf, или в Instance Spec в выпадающей панели "How to check container readiness"
Быстро посмотреть какая секция не проходит проверку статуса можно командой

```
# ./instancectl s
Name         Ready        Installed
-----------  -----------  -----------
start.sh     FAIL         FAIL
```
![instancespecrtcbutlerserviceshome](_assets/screenshot2019-09-25instancespecrtcbutlerserviceshome.png)

## Выкладка зависла из-за одной дохлой машинки {#single-bad-host}
В большинстве случаев проблема с выкладкой из-за недоступности одного сервера или нескольких инстансов говорит о неправильной настройке сервиса. Подробнее об этом см. [соответствующий пункт](https://wiki.yandex-team.ru/runtime-cloud/rtc-support/#host-is-unreachable).

При проблемах с малым числом инстансов может помочь увеличение окна деградации `operating_degrade_level/stop_degrade_level`. Подробно об этом нужно почитать в [документации](https://wiki.yandex-team.ru/jandekspoisk/sepe/nanny/alemate/yaml-recipes/#operating-degrade-level).

## Один или несколько инстансов висят в FAILED_TO_START_META_CONTAINER {#nodes-ips-changed}
**Данная инструкция справедлива только для сервисов с менеджером ресурсов Gencfg.**
Если такой статус появился в сервисе у инстанса, использующего YP.Lite - необходимо обратиться в rtcsupport.

**Пример инстанса:**
![testingmarketstaticpagessasserviceshome](_assets/screenshot2020-09-28testingmarketstaticpagessasserviceshome.png)

**Причина:**
Такой статус инстанса обычно проявляется, если у ноды сменился IP-адрес, а сервис выложен с использованием старого Gencfg-тега. В результате старый IP-адрес инстанса с новыми настройками сети ноды становится несовместим.

**Способ исправления:**
Чтобы привести сетевые настройки инстанса в соответствии с настройками ноды - нужно обновить Gencfg-тег в сервисе на последний актуальный. Сделать это можно в панели Instances сервиса с помощью кнопки редактирования группы
![instancestestingmarketstaticpagessasserviceshome1](_assets/screenshot2020-09-28instancestestingmarketstaticpagessasserviceshome1.png)
![instancestestingmarketstaticpagessasserviceshome](_assets/screenshot2020-09-28instancestestingmarketstaticpagessasserviceshome.png)

Сохраняем изменения в новый снапшот и активируем его.
Новые сетевые настроки инстанса применятся, когда у него будет target-state ACTIVE - !!**не PREPARED**!!.
Должно быть как на скриншоте:
![testingmarketstaticpagessasserviceshome1](_assets/screenshot2020-09-28testingmarketstaticpagessasserviceshome1.png)

Соответственно подготовка снапшота с последним Gencfg-тегом может зависнуть, если в рецепте присутствует промежуточная стадия подготовки снапшота(перевод в PREPARED-state).
Чтобы обойти это нужно модифицировать [degrade-level'ы](https://wiki.yandex-team.ru/runtime-cloud/nanny/alemate/yaml-recipes/#degradation-params) у таски на выкладку.
Инструкция по изменению параметров деградации у исполняющихся тасок: [https://wiki.yandex-team.ru/runtime-cloud/nanny/alemate/yaml-recipes/#how-to-update](https://wiki.yandex-team.ru/runtime-cloud/nanny/alemate/yaml-recipes/#how-to-update)
Перейти к таскгруппе, где будет список тасок Alemate, у которых можно будет изменить degrade-level'ы можно используя ссылку на неё напротив поля "Taskgroup". Пример такой ссылки есть на скриншоте:
![testingmarketstaticpagessasserviceshome2](_assets/screenshot2020-09-28testingmarketstaticpagessasserviceshome2.png)

## Инстанс перешел в состояние UNKNOWN {#instance_unknown_state}
В состояние UNKNOWN инстанс может попасть в следствие двух самых распостраненных проблем:

- Неисправна dom0 машина
- Неконсистентные настройки сети dom0 и сети контейнера(актуально для изолированных по сети контейнеров.
- Закончилось дисковое простратво в workdir контейнера из-за чего nanny не получает текущее состояние инстанса(проверить проблему можно командой `df -h ./` в shell контейнера)

**Неисправна dom0 машина**
В данном случае достаточно проверить состояние машины в интерфейсе оркестратора железом Wall-E.

- Перейти на страницу dom0-машины в Wall-E можно прямо из интерфейса Nanny, щёлкнув по ссылке "Wall-E url"
- Для поиска машины нужно ввести в поле FQDN имя машины
- Проверить наличие тикета в ITDC/RUNTIMECLOUD
- Проверить состояние здоровья машины
![mapsautoupdaterprestableserviceshome](_assets/screenshot2019-09-25mapsautoupdaterprestableserviceshome.png)
![hostmyt1-0562searchyandexnetinformation-wall-e](_assets/screenshot2019-09-25hostmyt1-0562searchyandexnetinformation-wall-e.png)

## Как посмотреть утилизацю ресурсов хоста инстансами сервиса {#porto_panel}
Для оценки утилизации ресурсов инстанса из UI Nanny доступна ссылка на porto панель golovan, найти её можно следующим образом:

1) Перейдите на страницу вашего сервиса в UI Nanny и нажмите кнопку Instances
![selection009.png](_assets/selection009.png)
1) В открывшемся списке инстансо выберите нужный инстанс, нажмите кнопку YASM и выберите "Porto container statistics"
![selection010.png](_assets/selection010.png)
1) Далее вы попадете на страницу YASM с porto панелью, документация по панели доступна [тут](https://wiki.yandex-team.ru/golovan/common-signals/#portoinst)
1) Так же есть возможность собирать и рисовать статистику отдельно по подконтейнерам сервиса. Для этого необходимо вручную добавить в настройках juggler'а инстанса параметр "subcontainer_name" с именем подконтейнера, который хочется мониторить. Подробности тут: [GOLOVAN-6224](https://st.yandex-team.ru/GOLOVAN-6224)

## Как запустить отдельный подконтейнер через Instance Spec {#instance_spec_sub_container}
Требуется запустить один или несколько исполняемых файлов в отдельном подконтейнере или с заданными лимитами(наследуются от слот-контейнера).
Для этого требуется выставить лимиты на секцию в Instance Spec
![selection014.png](_assets/selection014.png)

## Где посмотреть логи перехода сервиса между состояниями {#nanny_events_log}
Тут [https://wiki.yandex-team.ru/runtime-cloud/nanny/yt-logs/nanny-service-event-log/](https://wiki.yandex-team.ru/runtime-cloud/nanny/yt-logs/nanny-service-event-log/)

## Скопированный сервис не поднимается в статусе HOOK_FAILED {#nanny_copied_service_failing}
Если ваш сервис использует секреты, то необходимо проверить, есть ли доступ к ним у скопированного сервиса.
При этом если доступа нет в loop.log.full будет отображаться примерно следующая ошибка:

```
<pod_id> 2 2019-09-24 07:54:33,348 CRITICAL - main - cannot make init actions: Cannot prepare instance: Cannot get secret from Nanny Vault: Failed to fetch keychain "keychain" secret "secret" revision "<revision_id>": 400 Bad Request. Service is not allowed to read the keychain probably. Please add this service to the allowed services list on keychain "keychain" page.

InstanceCtlInitError: Cannot prepare instance: Cannot get secret from Nanny Vault: Failed to fetch keychain "keychain" secret "secret" revision "<revision_id>": 400 Bad Request. Service is not allowed to read the keychain probably. Please add this service to the allowed services list on keychain "keychain" page.
```

## В UI Nanny указана одна версия Instancectl, а в конфигурации снапшота другая {#nanny_instancectl_version}
Версия в UI обновляется при выпуске новой стабильной версии Instancectl, при этом, чтобы она уехала в конфигурацию снапшота необходимо вручную прожать кнопку "Save" напротив Runtime. В diff'e, показываемом при сохранении, отобразится изменение версии Instancectl.
![runtimeattributeshistorytest-serviceserviceshome](_assets/screenshot2019-09-24runtimeattributeshistorytest-serviceserviceshome.png)

**Релизы сделанные роботом (черед Ticket Integration или API) будут содержать неизменную версию InstanceCtl, если она не была изменена вручную в новой конфигурации. Изменения в UI на данные ревизии никак не повлияют.**
Чтобы включить автоматическое обновление Instancectl , необходимо настроить его в Ticket Integration.
![ticketsintegrationtest-serviceserviceshome](_assets/screenshot2019-09-24ticketsintegrationtest-serviceserviceshome.png)

Ветка Stable - редкие релизы, содержащие Must-have изменения. Содержит исправления для критичных ошибок.
Ветка Prestable - основные стабильные изменения Instancectl, содержащие менее необходимые правки, основная ветка обновлений Instancectl.

## Как зайти в PREPARED-ревизию {#ssh_to_prepeared}
Стандратное подключение к 22 порту инстанса происходит в ревизию с target-state ACTIVE. Но иногда необходимо подключиться к ревизиям в target-state PREPARED, для просмотра логов или диагноситки работы install-hook'а.
Сделать это можно с помощью `ssh` или `sky portoshell`. Для этого необходимо открыть список инстансов необходимой ревизии кнопкой `Instances`:
![Screenshot_2020-06-30%20rtcbutler%20Services%20Home.png](https://jing.yandex-team.ru/files/dimrul/Screenshot_2020-06-30%20rtcbutler%20Services%20Home.png)
И в строчке необходимого инстанса нажать на кнопку в столбике Access:
![Screenshot_2020-06-30%20rtcbutler%20Services%20Home%281%29.png](https://jing.yandex-team.ru/files/dimrul/Screenshot_2020-06-30%20rtcbutler%20Services%20Home%281%29.png)
Откроется окно с вариантами подключения:
![Screenshot_2020-06-30%20rtcbutler%20Services%20Home%282%29.png](https://jing.yandex-team.ru/files/dimrul/Screenshot_2020-06-30%20rtcbutler%20Services%20Home%282%29.png)
Для подключения к инстансу воспользуйтесь командой, предоставленной в этом окне. При нажатии на кнопку команда скопируется в буфер обмена ![copy](https://jing.yandex-team.ru/files/dimrul/Screenshot_2020-06-30%20rtcbutler%20Services%20Home%284%29.png).
В случае, если инстансов слишком много и затруднительно искать проблемный, можно выбрать команду от первого попавшегося, и заменить FQDN пода в команде на FQDN необходимого пода.

