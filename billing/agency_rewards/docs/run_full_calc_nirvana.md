Запуск полного расчета премий в тесте
===============

Граф в Нирване запускает полный расчет премий и кэшбэка. Данные берутся из тестовой среды: узел `test` в [Бункере](https://bunker.yandex-team.ru/agency-rewards/test), тестовая БД, тестовые пути в YT, запускается от имени -balance-ar-tst.

Чтобы запустить расчет, нужно создать реакцию на [базовый граф](https://nirvana.yandex-team.ru/flow/5c4d6cfd-7bd9-4f81-b0c9-646f54532583/6a7ebe2d-62e1-4c9b-a94f-492aff6cf5a2/graph). Для этого в Нирване создать реакцию в [billing/yb-ar/test](https://nirvana.yandex-team.ru/browse?selected=9397849), заполнив параметры реакции:
 - `Reaction name`
 - `Project` = `billing/yb-ar/test/Project`
 - `Trigget type` = `Start when all input artifacts are updated`
 - `Source Workflow ID`: выбрать `workflow`, значение -- ID базового графа `5c4d6cfd-7bd9-4f81-b0c9-646f54532583`
 - `Owner of workflow` = `robot-balance-ar-tst`
 - Справа появится выпадающий список Inputs, прожать `Inputs`->`Blocks Parameters`->`Run Full Calc in Agency Rewards`->`command line params`. Это аргументы командной строки, которые принимает бинарник, описаны [здесь](https://a.yandex-team.ru/arc_vcs/billing/agency_rewards/agency_rewards/utils/argument_parsers.py?#L150). Для заполнения выбрать тип `constant`.
   - чтобы указать месяц, за который нужно запустить расчеты, добавить аргумент `--platform-run-dt` в формате `YYYY.MM.DD HH24:MI:SS`. Месяц указывать **следующий** за тем, который нужен. Т.е. если нужно посчитать премии за декабрь 2021, указываем `--platform-run-dt=2022.01.01 10:00:00`
