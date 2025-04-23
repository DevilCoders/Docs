# Автозаскипы

## Введение

Когда какие-либо тесты начинают слишком часто мьютиться, появляется риск, что функциональность, которую они покрывают, окажется сломанной и никто этого не заметит. Чтобы избежать этого, система автозаскипов каждый день собирает статистику по замьюту тестов, то есть смотрит как часто тот или иной тест мьютился в прогонах.

Если тест мьютился чаще, чем в 50% сборок (гермиона-задач), система автозаскипов автоматически скипает этот тест через Тесткоп. При этом заводится тикет заскипа, с указанием имени теста, браузера, инструмента *(hermione / hermione-e2e),* *mute rate* и перечнем сборок, в которых этот тест мьютился.

  *Примечание: 50% – это коэффициент замьюта (mute rate) по умолчанию; при желании, вы можете [изменить][how-to-setup-autoskips] эту величину, задав её в настройках проекта в конфиге Тесткопа.*

  ![скриншот: тикет автозаскипа](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.auto-skips.autoskip-ticket.png)

**Внимание:** за день для конкретного проекта система может создать **не больше 5 тикетов заскипа** – это ограничение было [введено](https://github.yandex-team.ru/search-interfaces/schedulers/blob/master/infra/testcop/skip-muted-tests/constants.js#L27) сознательно, чтобы система не могла заскипать слишком большое количество тестов во время каких-либо инфраструктурных сбоев.

## Как настроить систему автозаскипов?

Про общую настройку читайте в параграфе [Чтобы активировать механизм автозаскипов][how-to-setup-autoskips] раздела [Как подключить проект к Тесткопу?](https://doc.yandex-team.ru/si-infra/tests-stability/testcop/testcop-how-to-add-project.html)

## Как узнать какие тесты были автоматически заскипаны?

### Способ 1

- откройте в Стартреке вашу очередь;
- сделайте поиск по ключевым словам `Починить и расскипать автозаскипанный тест`.

### Способ 2

- откройте страницу [шедулера][autoskip-scheduler] в Sandbox'е;
- нажмите на **SCHEDULED RUNS**:

  ![скриншот: шедулер механизма автозаскипов](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.auto-skips.scheduler-autoskip.png)

- допустим, вы хотите посмотреть какие тикеты были созданы в последнем запуске – нажмите на ссылку последней задачи:

  ![скриншот: все запуски шедулера автозаскипов](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.auto-skips.scheduler-autoskip-runs.png)

- на странице открывшейся sandbox-задачи нажмите на ссылку **job_logs**:

  ![скриншот: конкретный запуск шедулера автозаскипов](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.auto-skips.scheduler-autoskip-run.png)

- появится список лог-файлов, откройте **step__script.log**:

  ![скриншот: все логи запуска шедулера автозаскипов](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.auto-skips.scheduler-autoskip-logs.png)

- в лог-файле *step__script.log* вы увидите в каких проектах какие тесты были заскипаны, и какие тикеты были созданы:

  ![скриншот: лог запуска шедулера автозаскипов](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.auto-skips.scheduler-autoskip-log.png)

- откроем, для примера, найденную в логах ссылку на тикет с автозаскипом:

  ![скриншот: тикет автозаскипа](https://jing.yandex-team.ru/files/robot-testcop/testcop.doc.user.auto-skips.scheduler-autoskip-created-ticket.png)

[autoskip-scheduler]: https://sandbox.yandex-team.ru/scheduler/43695/view
[how-to-setup-autoskips]: https://doc.yandex-team.ru/si-infra/tests-stability/testcop/testcop-how-to-add-project.html#chtoby-aktivirovat-mekhanizm-avtozaskipov
