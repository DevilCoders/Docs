# Schetovod

Инструмент для сбора и аггрегации данных из файлов `faildump.json` и `json-report.json`.

Данные файлы создаются и сохраняются в ресурсах, которые генерируются при выполнении задач:

* [SANDBOX_CI_WEB4_GEMINI](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_WEB4_GEMINI)
* [SANDBOX_CI_WEB4_HERMIONE](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_WEB4_HERMIONE)
* [SANDBOX_CI_GRANNY_GEMINI](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_GRANNY_GEMINI)
* [SANDBOX_CI_GRANNY_HERMIONE](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_GRANNY_HERMIONE)
* [SANDBOX_CI_FIJI_GEMINI](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_FIJI_GEMINI)
* [SANDBOX_CI_FIJI_HERMIONE](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_FIJI_HERMIONE)
* [SANDBOX_CI_NERPA_GEMINI](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_NERPA_GEMINI)
* [SANDBOX_CI_NERPA_HERMIONE](https://sandbox.yandex-team.ru/tasks?type=SANDBOX_CI_NERPA_HERMIONE)

Результатом работы плагина является удобный для просмотра html отчет,
в котором можно получить следующую информацию:

* тесты, которые падали с ошибками (число и процентное соотношение к общему количеству падений);
* данные о типах ошибок для каждого теста (число и процентное соотношение к общему количеству падений);
* браузеры, в которых происходили те или иные ошибки для каждого теста;
* типы ошибок, которые возникали для всех тестов;
* имена тестов, в которых происходили ошибки тех или иных видов.

## Установка

```bash
$ npm install @yandex-int/schetovod --registry=http://npm.yandex-team.ru
```

## Использование

```bash
Usage: schetovod [options]

  Options:

    -h, --help         output usage information
    -V, --version      output the version number
    -r, --root <path>  Root folder with dump files
```

Опция `-r` обозначает путь к корневой директории, в которой лежат дампы.

Предполагается, что файловая структура дампов имеет вид:

```
root
    <resource_id1>
        json-reporter.json
    <resource_id2>
        faildump.json
```

## Разработка

Запуск проверки синтаксиса кода с помощью `eslint`:
```bash
npm run lint
```

Очистка сгенерированых файлов (`report/bundle.js` и `report/result.json`):
```bash
npm run clean
```

Автомагически получить данные для тестирования:
```bash
./tools/get-test-report-data.js
./bin/schetovod -r test-data
```

Проверить работу в браузере:
```bash
cd report && python -m SimpleHTTPServer
open http://localhost:8000/index.html
```
