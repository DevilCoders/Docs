## UpdateConversionLevelForMetrikaGoalsJob


### Продукт/подсистема

Ранжирование целей Метрики в Директе.


### Роль в работе продукта/подсистемы

Выгружает информацию о полезности целей ([оценку конверсионности](https://wiki.yandex-team.ru/goodmultigoal/)) в [ppcdict.metrika_goals](https://direct-dev.yandex-team.ru/db/ppcdict/tables/metrika_goals.html), колонка `conversion_level`, для саджеста топ5 и топ1 целей.


### Датафлоу

- Актуальный `conversion_level` берется из выгрузки ОКР:
[//home/bs/goodgoals/v3/GoalQuality](https://yt.yandex-team.ru/hahn/navigation?path=//home/bs/goodgoals/v3/GoalQuality)
для целей с отличающимися значениями в Директе (определяется с помощью снепшота
[//home/direct/mysql-sync/current/ppcdict/straight/metrika_goals](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/direct/mysql-sync/current/ppcdict/straight/metrika_goals))
и конвертируются следующм образом:
  - Если `IsPerfectGoal == 1`, тогда `conversion_level = 'perfect'`
  - Если `IsPerfectGoal == 0` и `IsGoodGoal == 1`, тогда `conversion_level = 'good'`
  - Если `IsPerfectGoal == 0`, `IsGoodGoal == 0` и `IsNotBadGoal == 1`, тогда `conversion_level = 'soso'`
  - Если `IsPerfectGoal == 0`, `IsGoodGoal == 0` и `IsNotBadGoal == 0`, тогда `conversion_level = 'bad'`
  - Иначе, если цель не найдена в yt таблице, то `conversion_level = 'unknown'`
- Сохраняем результаты в таблицу `ppcdict.metrika_goals`


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.UpdateConversionLevelForMetrikaGoalsJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'cpaautobudget.UpdateConversionLevelForMetrikaGoalsJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Перестанут обновляться данные о полезности целей.


### Как пользователи (или команда) заметят проблему и через какое время

Клиенты могут заметить неактуальную информацию о топ1 и топ5 целей Метрики, подставляемые в стратегию.

Команда может обнаружить отставание оценки конверсионности с помощью juggler-мониторинга.


### Контакты разработчиков и менеджеров

Разработчики: [Дмитрий Анощенков](https://staff.yandex-team.ru/dmitanosh)


### Желательное время исправления в случае поломки

Неделя, т.к. поломка джобы не создаст для пользователей непреодолимых проблем.


### Способы регулирования работы джобы

- ppc-property `conversion_level_update_limit` определяет максимальное количество записей для обновления за один запуск джобы.


### Известные причины поломок

- Не полное обновление оценок конверсионности подряд за несколько последовательных запусков.
Решается полным обновлением оценок конверсионности ваншотом `UpdateConversionLevelForAllMetrikaGoalsOneshot`.
Или, если проблема повторяется, увеличением лимита `conversion_level_update_limit`.


### Дополнительно: тонкости и подводные камни
