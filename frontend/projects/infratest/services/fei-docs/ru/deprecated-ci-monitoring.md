# Мониторинг CI/CD в web4, fiji, frontend

Здесь собрана информация о приборах, по которым можно отслеживать скорость производва в этих репозиториях до момента миграции на общеаркадийную сборку и CI.

У нас есть преднастроенные графики, все они живут в [DataLens](https://datalens.yandex-team.ru/). Для удобства рекомендуем вам [собрать дашборд](https://datalens.yandex-team.ru/docs/concepts/dashboard) с наиболее интересными для вас графиками с выбранными параметрами. Например, если вы коммититесь на Cycle-Time на окне 28 дней для 80-го перцентиля по задачам, вероятно вам и графики скорости конвейера будут интересны именно на этом окне и этом перцентиле.

При необходимости, вы можете собрать свой график по нашим данным, или выполнять разовые аналитические запросы в наши таблицы.

## Графики

Наиболее полное представление о вашем CI поможет составить [универсальный дашборд CI/CD](https://datalens.yandex-team.ru/lw6x2o8isccge-dashboard).

Для работы с дашбордом вам надо понимать следующие термины:

- *задача* (ci task или ci job) — конкретная задача в Sandbox, обычно она красит какую-то проверку в пулреквесте. Например, запуск unit-тестов, или deploy беты.
- *билд* (ci build) — полный набор задач, запустившихся для какого-то события. Например, вы открыли пулреквест, и по этому событию запустились задачи бутстрапа, гермионы, палмсинка — все вместе они составляют билд.
- *фейл-рейт* (fail rate) — отношение количества упавших задач или билдов к общему количеству. Например, если из 10 билдов 2 упало — fail rate составляет 20%.
- *скользящее окно* (moving window) — выборка данных за определённый период. Когда мы говорим «сегодня fail rate билдов составляет 5% на скользящем окне 14 дней» это значит, что из всех билдов, запускавшихся в последние 14 дней упали 5%. Если такое значение за 20-е сентября, значит речь о билдах, запускавшихся с 7 по 20-е сентября включительно.Скользящее окно позволяет сгладить резкие скачки в величине и увидеть тренд. Чем меньше скользящее окно, тем резче колебания графика.
- *перцентиль* (percentile) — значение, которое заданная величина не превышает с фиксированной вероятностью. Когда мы говорим «задачи гермионы на 80-м перцентиле выполняются за 20 минут», это значит 80% задач гермионы выполняется за 20 минут и меньше. Анализ скорости выполнения задач на перцентилях позволяет оценить большинство задач, исключив из статистики редкие выборсы с аномально длинными задачами.

### Cycle-time в деталях

От начала работы над фичей до появления её в продакшене проходит несколько стадий. На каждой стадии важны разные автоматические и ручные процессы.

#### Разработка

Это время от того момента, как задачу взяли в работу, до открытия ревью-реквеста. Трекать этот период сейчас можно на [цикл-тайме](https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=2z) по статусам. Но здесь вмешивается человеческий фактор: не забыл ли исполнитель перевести задачу в корректный статус, когда взял её в работу.

#### Ревью

Считается от того момента, как ревью-реквест открыт, до того, как он встал в очередь на влитие. Это тоже можно отследить на [цикл-тайме](https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=2z) по статусам, при условии, что автоматика корректно переводит тикеты в статусы при открытии ревью-реквеста и при постановке в очередь. На время этого этапа влияет сразу несколько вещей:

1. **Время ожидания проверок в пулреквесте.** От пуша в арк до момента, когда в Аркануме прокрашиваются статусы. Увидеть это можно на графике [Pipeline Speed]. Строится по событиям из Arcanum.
1. **Стабильность проверок**: чем нестабильнее проверки, тем больше разработчику приходится тратить время на отладку и починку. Увидеть это можно на графике [Infra FR](https://datalens.yandex-team.ru/aclfv98lnuo25-infra-fr-dashboard?state=da88b9a9227) в контексте pull-request. Строится по событиям из Sandbox. Обогащается с помощью [zeroline]. Можно увидеть Fail Rate каждой проверки, а так же наиболее популярные ошибки в проверках.
1. **Время ревью и количество итераций**. Сейчас прибора про это нет, делайте заказы в Arcanum.

#### Влитие ревью-реквеста

От момента, когда написали `/merge`, до собственно влития. Это тоже можно отследить на [цикл-тайме](https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=2z) по статусам, при условии, что автоматика корректно переводит тикеты в статусы при постановке в очередь и при влитии.

1. **[Ready For Dev]** показывает время от первой постановки в очередь MQ до влития. Может включать время, потраченное на доработку ревью-реквеста после неудачной попытки влития (с конфликтами например). Строится по событиям от MQ.
  1. **[Queue Time]** показывает время, которое ревью-реквест провёл в очереди. То есть от `/merge` до фидбека: влития или сообщения об ошибке. В процессе mq-проверки могут запускаться несколько раз для разных кешей, если кеш зеленый, он будет влит, а если красный, размер кеша будет уменьшаться вплоть до 1 ревью-реквеста в этом кеше, и только после этого фейла мы дадим фидбек в репозиторий.
  1. **[Infra FR](https://datalens.yandex-team.ru/aclfv98lnuo25-infra-fr-dashboard?state=14d12c06226)** для проверок MQ показывает, какие проверки нестабильны в MQ-кешах.
  1. **[Infra FR](https://datalens.yandex-team.ru/aclfv98lnuo25-infra-fr-dashboard?state=b2a8c30e220)** для влития в MQ показывает, какая доля влитий (после успешного прохождения проверок) оказалась неуспешной и по каким причинам.

#### Ожидание релиза

От момента, когда ревью-реквест влился в транк, до отведения релиза. Это тоже можно отследить на [цикл-тайме](https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=2z) по статусам, при условии, что автоматика корректно переводит тикеты в статусы при влитии и отведении релиза.

#### Релиз

От отведения релиза до попадания на продакшен. Опять же, видно на [цикл-тайме](https://datalens.yandex-team.ru/k9cxivluw5xah-metrika-cikl-tayma-servisov-otdela-poiskovyh-interfeys?tab=2z) по статусам.

[Pipeline Speed]: https://datalens.yandex-team.ru/apyt19vo829m7-klyuchevye-metriki-infrastruktury-frontenda?tab=GE
[Ready For Dev]: https://datalens.yandex-team.ru/apyt19vo829m7-klyuchevye-metriki-infrastruktury-frontenda?tab=P6&state=68aeebca187
[Queue Time]: https://datalens.yandex-team.ru/apyt19vo829m7-klyuchevye-metriki-infrastruktury-frontenda?tab=DR4
[zeroline]: https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/services/zeroline/


## Таблицы

Вы можете выполнять запросы по нашим данным прямо в [YQL](https://yql.yandex-team.ru/docs/clickhouse).

Вот примеры запросов в наши таблицы:

- [stats.task_statuses](https://yql.yandex-team.ru/Operations/YG2b9wuEI1Sgw0BA0IXk-oIP2Gohb6FDj3iLMbeLn2g=)
  Связь task_id, build_id, build_context, repository, status. (для infra-fr) Содержит и время выполнения задачи в секундах — duration.
  Отправляется из sandbox_ci и trendbox_ci задач через zeroline.
- [stats.ci_builds](https://yql.yandex-team.ru/Operations/YVI4Bq5OD-peHBhrnp-V43PH7IsmrGmBeYtzcTrrk20=)
  Связь build_id, build_context, head_ref, head_commit_sha, author. Только для репозитория frontend.
- [stats.required_checks](https://yql.yandex-team.ru/Operations/YG2bw_MBw4KPI8kbLANxF9GfuL00OVDjXxdb82gPItM=)
  Список обязательных проверок на проекте. Заполняется вручную.
- [stats.merged_prs](https://yql.yandex-team.ru/Operations/YG2ZP9K3DKODcDVLn0cB9M1s11NB1fnPAQzcuWCjbqI=)
  Связь пулреквестов (в github) и тикетов в трекере.
  Хук в Github уходит в webhook-handler/stat-on-pr-merge, откуда пишется в эту табличку.
- [stats.pushed_commits](https://yql.yandex-team.ru/Operations/YG2aCQuEI1Sgwz8clq0TWMeBJlRy-uiKxdcD94NxxC4=)
  Связь пулреквестов, коммитов и пользователей.
  Хук в аркануме уходит в webhook-handler/push-to-status-finish-v2, откуда пишется в эту табличку
- [stats.reported_statuses](https://yql.yandex-team.ru/Operations/YG2bZL94hqYITQVZ8ksyIAuCAIuW8fe0rYaHPoy7Ans=)
  Статусы (gh|arc)-проверок по sha и время, когда эти проверки приняли такой статус.
  Хук в аркануме уходит в webhook-handler/push-to-status-finish-v2, откуда пишется в эту табличку
- [stats.release_steps](https://yql.yandex-team.ru/Operations/YG2bBr94hqYITQUYpVmF2oBrk3O2AjjKlDCNqbPnlv0=)
  Время выкладки релиза по шагам, но только для проектов на sandbox-ci.
  Сигнал отправляется из sandbox_ci задач через metrics-logger.
- [stats.trendbox_steps_profiler](https://yql.yandex-team.ru/Operations/YG2c5_MBw4KPI8n8KWYxaoN_dE9PMCtfrwAcMLe-_gE=)
  Время выполнения шагов в trendbox-задачах. Есть task_id, build_id, ref, commit_sha и местами project.
  Собирается шедулером с помощью anulus. Часть данных не доходит: FEI-21956

Данные смежных команд, которые могут вас заинтересовать:

- [Sandbox](https://docs.yandex-team.ru/sandbox/statistics)
- [Arcanum](https://yt.yandex-team.ru/hahn/navigation?path=//home/devtools-activity/sources/v1/pull_requests)
