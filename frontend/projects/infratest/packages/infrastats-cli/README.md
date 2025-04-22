# infrastats-cli

CLI утилита для построения отчета со статистикой по плавающим тестам, возникающим в ходе прогона [hermione](https://github.com/gemini-testing/hermione/) и [gemini](https://github.com/gemini-testing/gemini/) тестов.

Статистика собирается по `json-reporter` отчетам, скаченным из `sandbox`. Данные отчеты генерируются с помощью плагина [json-reporter](https://github.com/gemini-testing/json-reporter), который подключается к инструментам hermione и gemini.

Отчет строится с помощью инструмента [schetovod](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/schetovod) и сохраняется в текущую рабочую директорию в папку `infrastats-report`.

## Примеры использования

Построить отчет по hermione тестам в проекте web4 из 10 последних ресурсов за последние 10 минут:
```bash
node ./bin/infrastats-cli build-report --resource-type SANDBOX_CI_ARTIFACT --resource-limit 10 --resource-attr tool=hermione --resource-attr type=json-reporter --resource-attr project=web4 --resource-created-from 10m
```

Построить отчет по hermione тестам в проекте web4 из всех найденных смердженных ресурсов в dev за текущие сутки:
```bash
node ./bin/infrastats-cli build-report --resource-type SANDBOX_CI_ARTIFACT --resource-limit 100 --resource-attr tool=hermione --resource-attr type=json-reporter --resource-attr project=web4 --resource-attr released=stable --get-all-resources
```

Построить отчет по hermione тестам в проекте ydo из ветки master за последнюю неделю:
```bash
node ./bin/infrastats-cli build-report --resource-type SANDBOX_CI_ARTIFACT --resource-limit 100 --resource-attr tool=hermione --resource-attr type=json-reporter --resource-attr project=ydo --resource-attr branch=master --resource-created-from 1w --get-all-resources
```

## Запуск с дебагом

```bash
DEBUG=infrastats-cli:*,schetovod:* node ./bin/infrastats-cli build-report ...
```

## Если отваливаются запросы к API Sandbox

В случае если запросы к API Sandbox отваливаются и ничего не скачивается, то можно попробовать подкрутить таймауты и ретраи с помощью следующих переменных окружения:
* `SB_API_DOWNLOAD_TIMEOUT` - таймаут на скачивание ресурса (по умолчанию 60000 мс)
* `SB_API_RETRIES` - количество ретраев (по умолчанию 7)
* `SB_API_RETRIES_FACTOR` - экспоненциальный коэффициент отката (по умолчанию 2)
* `SB_API_MIN_RETRIES_TIMEOUT` - количество мс до начала первого ретрая (по умолчанию 500 мс)
* `SB_API_MAX_RETRIES_TIMEOUT` - максимальное количество мс между двумя ретраями (по умолчанию 2000 мс)
