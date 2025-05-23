# AppHost и граф

Граф — это конфиг для AppHost или сценарий сборки ответа на некоторый запрос. Именно он отвечает за то, в какие бэкенды, когда и при каких условиях нужно сходить, чтобы сформировать ответ.

Увидеть текущий граф можно в [Horizon](https://horizon.z.yandex-team.ru/graphs/svg/JOBS/jobs/_/trunk).

### Чтобы что-то поменять в графе, нужно

- Сделать необходимые изменения в [тестовом графе](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/services/jobs/graphs/testing.json)
- При следующем запуске сервиса (`npm start`) граф будет выгружен в `Horizon` с именем вида `testing_<username>-jobs_test`, ссылка на выгруженный граф появится в консоли. После выгрузки графа убедитесь, что он валиден, а также, что он успел задеплоиться хотя бы на несколько машинок, в противном случае вы не сможете его использовать. Можно сразу вносить изменения в `Horizon` - главное, не забыть их корректно портировать.
  ![](https://jing.yandex-team.ru/files/koreil/2021-04-19T10:38:43Z.ca19a5d.png)
  ![](https://jing.yandex-team.ru/files/koreil/Снимок%20экрана%202021-04-19%20в%201.36.35%20PM.png)
- Если вам необходимо добавить новые бэкенды, добавлять их следует [в папочку в Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/backends/JOBS)
- Протестируйте свои изменения локально. Убедитесь, что приезжает нужная версия графа — для этого можно добавить параметры `dump=eventlog&eventlog_format=html`, под выдачей вы увидите логи и среди прочего - версию графа.
  ![](https://nda.ya.ru/t/lXnn1T_Q3t6phU)
- Закоммитьте изменения в тестовый граф
- Портируйте изменения [в Аркадию](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/verticals/JOBS/jobs.json Аркадию)
- Когда граф будет готов к выкатке в продакшн, воспользуйтесь Релизной машиной, чтобы его зарелизить (см. следующий раздел)

### Релизная машина

- [Релизная машина](https://rm.z.yandex-team.ru/)
- [Релизная машина, Jobs Graph](https://rm.z.yandex-team.ru/component/jobs_graphs/manage?detail=job_results&scopes=2&branch=2&tag=1)

Через релизную машину в прод релизятся [бэкенды](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/backends/JOBS) (за исключением бэкендов с `trunk_overwrite`, которые выезжают в прод СРАЗУ после влития в `trunk`, но это редкая и опасная опция), [routing_config](https://a.yandex-team.ru/arc/trunk/arcadia/web/app_host/conf/http_adapter/vertical/JOBS/routing_config.json), графы.

1. С помощью кнопки `Pre release` отводим стабильную релизную ветку. Это действие по факту запускает SB-задачи, в том числе типа `CREATE_BRANCH_OR_TAG` и `BUILD_HORIZON_AGENT_CONFIG` + должны пройти тесты, если они есть. Может понадобится авторизоваться в Sandbox API через OAuth ([получить](https://sandbox.yandex-team.ru/oauth)). После авторизации, если она была нужна, придется еще раз нажать `Pre release`
   До момента появления в интерфейсе новой ветки может пройти ~10 минут. Параллельно робот начнет слать на почту отчеты о запущенных Sandbox-задачах.
2. Когда задача отработает, нужно нажать на три точки слева вверху и выбрать новую ветку. Через ~15 минут станет активна кнопка `Release`. Благодаря этому создается сущность "релиз" — по факту релизятся SB-таски. Галочку `Use Robot` проставлять НЕ нужно.
   ![](https://jing.yandex-team.ru/files/koreil/Снимок%20экрана%202021-01-19%20в%201.34.40%20PM.png).

3. Релиз начинает прорастать в nanny (занимает около 5 минут). Это можно увидеть на `dashboard` вертикали, [пример](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/apphost_jobs/) для jobs. Появится так называемый "метарецепт" — плашка справа.
4. `Select -> Commit -> Apply`
   ![](https://jing.yandex-team.ru/files/koreil/Снимок%20экрана%202021-01-14%20в%203.55.36%20PM.png)
5. На плашке каждого сервиса появится новый хеш — между ними можно переключаться. Нам нужно нажать `Deploy` (сверху справа).
6. В выпадающем списке Recipe выбрать `auto`:
   ![](https://jing.yandex-team.ru/files/koreil/Снимок%20экрана%202021-03-25%20в%2011.12.23%20AM.png)

> ⚠️☠️ **Кнопку `Activate` нажимать НЕЛЬЗЯ!**
