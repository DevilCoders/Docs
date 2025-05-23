# FAQ

В рамках данного раздела будет собираться информация по тому как пользоваться [Y.Deploy](https://yd.yandex-team.ru/).
На этой странице собраны самые частые вопросы.
За более подробной информацией обращайтесь к подстраницам раздела (справа)

## Как запустить свой первый сервис? {#quickstart}

Ознакомьтесь с разделами [Запуск сервиса](quick-start.md) и [Базовая настройка балансировки](launch/balancing.md).

## Квоты: Сколько можно жить во временной (tmp) квоте? Как заказать квоту? Как узнать, на что тратится квота / сколько ресурсов доступно? {#quota}

[Про временную tmp квоту.](https://wiki.yandex-team.ru/yp/tmp/)
[Как заказать квоту.](https://wiki.yandex-team.ru/yp/quotas/)
[Как перенести квоту при миграции из Qloud](how-to/migration/qloud/qloud.md)

Узнать на что тратится квота / сколько ресурсов доступно:

- [https://qyp.yandex-team.ru/profile](https://qyp.yandex-team.ru/profile)
- [https://wiki.yandex-team.ru/yp/yp-cli/#uznatnachtotratitsjakvota](https://wiki.yandex-team.ru/yp/yp-cli/#uznatnachtotratitsjakvota)

##  Что такое Multi Cluster Service и Per Cluster Service? Чем они отличаются? {#rs-vs-mcrs}

Вы можете запускать свои сервисы, используя примитивы деплоя Multi Cluster и Per Cluster. От выбранного примитива деплоя зависит то, сколько Pod может быть недоступно в локациях. Подробнее читайте в разделе [Примитивы деплоя](concepts/deploy-unit/deploy-primitives.md).

##  Как настроить выкладки, чтобы они работали при недоступном ДЦ? {#mcrs-unavailable-dc}

Если часть ДЦ, на которых развёрнут сервис, недоступна, можно делать выкладки в доступные ДЦ, если используется примитив деплоя **Multi Cluster Service**. Для этого достаточно указать disruption budget больше числа подов, заказанных в недоступном ДЦ. Тогда выкладка будет идти в доступные ДЦ с окном, равным `disruption_budget - <число подов заказанное в недоступном ДЦ>`.
Например, вы создали Multi Cluster Service в локациях SAS, MAN, VLA. В каждой из локаций вы создали по 10 Pod'ов (инстансов) и сказали, что disruption budget = 11. Это значит, что при выключении ДЦ MAN деплой сможет продолжаться в ДЦ SAS и VLA с окном 1.
После возврата недоступного ДЦ новая ревизия стейджа будет докачена в него автоматически.

## Как настроить affinity (сожительство) с инстансами другого сервиса? {#affinity}

*Напр. хочу, чтобы инстансы сервиса А и сервиса Б выполнялись на одной машинке?*
Если это независимые сервисы с разными релизными циклами, то этого сделать не получится.
При этом у вас есть возможность обеспечить колокацию за счет размещения сервисов в разных Box'ах одного Pod'а.

## Доступно ли API для управления деплоем подов как альтернатива dctl? {#api}

Наша консольная утилита dctl фактически является оберткой поверх [API YP](https://wiki.yandex-team.ru/yp/api/).
Доступ к API выдается [через форму](https://forms.yandex-team.ru/surveys/24997/).

**Обратите внимание**:
* создание объектов другого типа по умолчанию запрещено
* создание объектов Stage роботными пользователями также запрещено.

Про мотивацию - [https://clubs.at.yandex-team.ru/infra-cloud/601](https://clubs.at.yandex-team.ru/infra-cloud/601).

## Какие возможности для массового редактирования свойств подов/боксов/ворклодов существуют? {#templates}

На данный момент такой возможности нет, но у нас идеи как это имплементировать на базе "Шаблонов Stage'ей".

## Как читать графики на вкладке monitoring? {#monitoring}

Мы используем общую панель Porto-метрик.
Подробнее о метриках на этой панели можно [почитать тут](https://wiki.yandex-team.ru/golovan/common-signals).

## Как реализовать более хитрую схему деплоя инстансов сервиса, чем поочередное обновление инстансов? {#deploy_scenario}

Пока никак - поддерживается только [Rolling update](https://wiki.yandex-team.ru/ru/rsc-for-users/).

## Как автор сервиса узнает, что написанные им проверки не отрабатывают/таймаутятся? Есть ли какие-то стандартные средства диагностики (мониторинги) на поды/боксы? {#diagnostics}

Статусы всех объектов стейджа отображаются в UI. Если что-то пошло не так - страничка не будет "зеленой".
Результаты проб также отправляются в golovan [в виде сенсоров](reference/monitorings/user-sensors/user-sensors.md).

## Можно ли класть спеку stage.yaml, полученную через dctl, в VCS/Аркадию? {#store_stage.yaml}

Можно, если вы используете новую модель хранения секретов в спеке сервиса. Подробнее - в [документации](https://deploy.yandex-team.ru/docs/how-to/secrets)

## Что происходит с секретами, если Секретница недоступна/права на секрет поменялись/уволился владелец секрета? {#secret_issues}

* Секретница недоступна в момент обновления конфигурации stage (без изменения секретов):
Взаимодействие с API не пострадает, но накатка обновленной версии будет произведена только в тот момент, когда Секретница станет доступна.

* У секрета поменялись права доступа после выдачи delegation token/владелец delegation token уволился:
Делегирующий токен связан только с самим секретом и дает право прочитать секрет тому, кто этим токеном обладает. При получении токена можно привязать токен к tvm-приложению, тогда Секретница проверит и айди приложения из сервис-тикета. Еще один уровень проверки — подпись (пароль) для токена.
На возможность прочитать секрет по токену никак не повлияют смена прав доступа пользователей к секрету, увольнения и прочие действия в связках пользователь-секрет. Пока текущий владелец секрета не отзовет токен, по токену можно получить секрет. Поэтому на оба вопроса ответ простой — ничего не произойдет.

## Как изменить права доступа {#stage_access}

Права доступа определяются ролевой моделью, описанной [здесь](reference/access-management/rbac.md).
Работать с ролями можно напрямую через [IDM](https://idm.yandex-team.ru/system/deploy-prod/roles). Также новые роли можно запрашивать на главной странице проекта (Вы будете перенаправлены на предзаполненную форму в IDM). Все выданные роли видны на главной странице проекта.

##  Как фильтровать Поды в GUI {#filters}

На странице Status можно отображать не все Поды, а только те, которые удовлетворяют некоторым условиям. Есть пара преднастроенных фильтров (по ревизии и по статусу) и возможность задавать произвольный фильтр [с синтаксисом YP SelectObjects](https://wiki.yandex-team.ru/yp/api/). Фильтры оперируют путями в [схеме объекта Pod](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/autogen.proto?rev=6407541#L215). Основной интерес представляет поле `/status` типа [TPodStatus](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/data_model.proto?rev=6411293#L1285), описывающее текущее состояние.
Примеры:

* Поды, которые не могут подняться из-за какой-либо ошибки
`[/status/agent/execution_error] != null`
* Поды, которые не могут подняться из-за специфичной ошибки
`is_substr("Unknown virtual disk ref", string([/status/agent/execution_error/message]))`
* Поды, зашедуленные на конкретный хост
`[/status/scheduling/node_id] = "man2-9421.search.yandex.net"`

Можно также фильтровать по статусу составных частей Пода (box, workload, volume, resource), но это сложнее, т.к. в [статусе подового агента](https://a.yandex-team.ru/arc/trunk/arcadia/yp/client/api/proto/pod_agent.proto?rev=6434628#L66) соответствующие поля представлены списками и индексация происходит по порядковому номеру, а не по идентификатору. Порядок тот же, что и в GUI, начиная с 0.

* Поды, в которых 0-й workload не активировался:
`[/status/agent/pod_agent_payload/status/workloads/0/state] != "active"`

## Как обновить большие данные под сервисом (сотни гигабайт)? Как сделать это по кастомному алгоритму (схеме деплоя)? {#large_resources}

Мы разрабатываем resource cache, который в связке с рецептами позволит разделить фазы скачивания ресурса от фазы обновления (рестарта) сервиса

##  Как настроить балансировку из L3-балансера, развёрнутого в L3-manager, напрямую в поды, развёрнутые в Деплое? {#l3-balancer-into-pods}

[Документация](https://wiki.yandex-team.ru/pochta/sre/deploy/L3/) от наших пользователей.

##  Хочу настроить компонент X (rsyslogd/cron/etc), не собирая костыли. Можно ли найти/списать готовый пример у коллег? {#grep_all_stages}

Можно грепнуть все стейджи. Например:

```bash
yanddmi@yanddmi-dev[~/tmp]:ya tool yp select stage --address xdc --selector /meta/id --selector /spec/deploy_units --format json --no-tabular > stages.json 
yanddmi@yanddmi-dev[~/tmp]:cat stages.json | ya tool jq '.[]' -c | grep 'rsyslogd' | ya tool jq '.[0]'
"adfox-engine-testing-1"
"core-test-stage"
"madamada-partner-test-stage"
"partner-autotest-stage"
"partner-autotest-stage-2"
"partner-preprod-stage"
"partner-production-stage"
"partner-test-stage"
"zapravki-prestable"
"zapravki-production"
"zapravki-testing"
```
Далее можно посмотреть на конфигурацию этих стейджей в UI.

## Как долго применяются обновления в Stage?

Время обновления зависит от многих факторов. Для понимания, как происходит применение изменений, ознакомьтесь с со статьёй [Как обрабатывается спецификация Stage](reference/internals/stage-specification-processing.md).

## Могу ли я выполнить команду во всех подах своего deploy unit'a? {#sky}
В деплое поддержана возможность выполнения команды во всех подах деплой юнита в конкретном боксе.

Это делается при помощи команды [Skynet](https://doc.yandex-team.ru/Search/skynet-desc/) ``sky run`` ([документация](https://doc.yandex-team.ru/Search/skynet-api/sky/usage.html#run)) вида:

``sky run 'echo ${DEPLOY_BOX_ID} @ ${DEPLOY_POD_PERSISTENT_FQDN}' b@<project_id>.<stage_id>.<du_id>.<box_id>``

Больше информации о способах адресации инстансов - в [документации](https://doc.yandex-team.ru/Search/skynet-api/sky/blinovcalc.html).
