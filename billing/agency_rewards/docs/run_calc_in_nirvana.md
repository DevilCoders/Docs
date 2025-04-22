Запуск расчета в Nirvana
===============

Базовый граф и пример реакции:
https://nirvana.yandex-team.ru/browse?selected=9397720

Чтобы запустить расчет из бункера:

- Запросить роль "Пользователь роботов без доступа к паролю" в сервисе "Тестирование расчетов премий агентств":\
https://abc.yandex-team.ru/services/ybar-test/
- Выдать нужные права в YT роботу `robot-balance-ar-tst`: read на все таблицы, из которых нужно прочитать данные, write на таблицы, в которые нужно записать данные (например, таблица, указанная в  `result-path`)
- Запросить права writer на нужный узел в Нирване (написать кому-нибудь из участников [роли](https://nirvana.yandex-team.ru/roles/nirvana.operation.yb-ar)):
  - Прод: https://nirvana.yandex-team.ru/browse?selected=9397851
  - Тест: https://nirvana.yandex-team.ru/browse?selected=9397849


- Создать новую реакцию. В ней указать:
    - Trigger type: `Start when all input artifacts are updated`
    - Source Workflow ID: выбрать `Workflow` и указать ID графа Run calc query (`330e235c-43da-4c7b-9eaa-63bf140f94ed`)
    - Добавить все поля из `Inputs->Global parameters`, всем указать тип `Constant`
- Заполнить эти поля:
    - `Arcadia Revision`: оставлено для обратной совместимости с реакциями, указать любое число.
    - `bunker-path`: путь до расчета в Бункере относительно `agency-rewards/{env}/calc/`, т.е. если полный
      путь: `https://bunker.yandex-team.ru/agency-rewards/test/calc/market/monthly_market`,
      указываем `market/monthly_market`
    - `bunker-version:` версия расчета в Бункере (`stable`/`latest`/номер)
    - `cluster`: кластер на YT (`hahn`/`freud`/etc)
    - `env`: окружение, из которого будет взят расчет в Бункере (`prod`/`test`)
    - `platform-run-dt`: месяц, за который нужно запустить расчет, в формате `YYYY-MM` (июль 2018 = `2018-07`)
    - `result-path`: путь до таблицы на YT, куда нужно сложить результаты (например: `//tmp/mylogin/table`)
    - `env-config`: Патч env'а из расчета в таком же формате (т.е. список словарей, в каждом из которых два
      ключа: `name` и `value`), но с экранированием кавычек и в одну строку. Например, если нужно подать такой патч:

```json
[
    {
        "name": "acts",
        "value": "//home/balance/test/yb-ar/market/acts/202103"
    },
    {
        "name": "rewards",
        "value": "//home/balance/test/yb-ar/market/rewards/market/202103"
    }
]
```

Подаем:
```json
[{\"name\": \"acts\", \"value\": \"//home/balance/{env}/yb-ar/market/acts/{calc_dt}\"}, {\"name\": \"rewards\", \"value\": \"//home/balance/{env}/yb-ar/market/rewards/{calc_name}/{calc_dt}\"}]
```

 - Активируем и запускаем реакцию. Во вкладке Launches можно увидеть запуски, открыть граф и посмотреть результат запуска. Во вкладке `Logs` хранятся:
   - Ссылка на таблицу в YT с результатами
   - Shared url YQL-запроса

