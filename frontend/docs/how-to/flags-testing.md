# Тестирование под выборками

Для тестирования флагов используется Sandbox-таск `FRONTEND_MONOREPO_TESTS_RUNNER`.

## Ограничения и пререквизиты

Для того, чтобы можно было тестировать флаги:
* Необходимо подготовить гермиону в проекте по [доке](./hermione-exp-flags.md).
* Разбить npm-скрипт `ci:hermione` на два скрипта: `ci:hermione:build` и `ci:hermione:test`. Например для `ydo`:
  * ```
    {
      "ci:hermione": "YENV=testing HERMIONE_RUN=1 run-s build:with-storybook deploy:static 'hermione -- --play --retry 4'",
      "ci:e2e": "YENV=testing npm run e2e -- --retry 4"
    } 
    ```
  * ```
    {
      "ci:hermione": "run-s ci:hermione:build ci:hermione:test",
      "ci:hermione:build": "YENV=testing HERMIONE_RUN=1 run-s build:with-storybook deploy:static",
      "ci:hermione:test": "YENV=testing HERMIONE_RUN=1 npm run hermione -- --play --retry 4",
      "ci:e2e": "npm run ci:e2e:test",
      "ci:e2e:test": "YENV=testing npm run e2e -- --retry 4"
    } 
    ```

## Запуск

1. Открыть [Sandbox](https://sandbox.yandex-team.ru) и создать таску `FRONTEND_MONOREPO_TESTS_RUNNER`.

   ![Открыть окно создания таски](../images/flags-testing-1.png)
   ![Создать таску FRONTEND_MONOREPO_TESTS_RUNNER](../images/flags-testing-2.png)

2. Указать параметры:
   1. `Owner` – FRONTEND
   2. `Description` – понятное (в первую очередь вам самим) описание
   3. `Service` – тестируемый сервис
   4. `Release ticket key` – релизный тикет, куда будет отправляться информация о запущенных тасках
   5. `Checks` – выбрать какие инструменты запускать
   6. `JSON with flags` – если нужно явно указать какие-то флаги в JSON-формате
   7. `test-id` – id тестируемой выборки
   8. `Flags Handler` – handler, который указывался при создании флага
   9. `Paths to flags in the test_id context` – путь/пути к расположению флагов в выборке в формате `MAIN.REPORT.templates`
   10. `[Hermione e2e] base url` – умолчанию стоит https://hamster.yandex.ru - последний продакшен-релиз, но можно подставить адрес беты. Это используется только в e2e-тестах.

3. Запустить таску нажав на `Run`.

   ![Запустить таску](../images/flags-testing-3.png)

4. Дождаться результатов тестирования в указанный тикет. Также созданные таски можно будет найти по [фильтру](https://sandbox.yandex-team.ru/tasks?children=true&type=TRENDBOX_CI_JOB_BETA&desc_re=flags%2F.*), где вместо `.*` в `flags/.*` написать id таски `FRONTEND_MONOREPO_TESTS_RUNNER`.
