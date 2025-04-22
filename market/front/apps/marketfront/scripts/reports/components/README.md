# Подсчет сущностей в проектных и платформенных папках

Скрипт для подсчета сущностей (резолверы/ресурсы/сущности/виджеты),
которые находятся в платформенных и проектных папках маркета.

Умеет собирать и находить diff между локальной версией и продовой.
Актуальное состояние хранится на [gh-pages](https://github.yandex-team.ru/market/marketfront/blob/gh-pages/reports/components_usage_report.csv)
Пушится после каждого релиза [пайплайном](https://tsum.yandex-team.ru/pipe/projects/front-market-unified/pipelines/master-per-commit/editor/20) обновления мастера


## Запуск

`npm run report:codehealth` - запишет csv файл `components_usage_report.csv`
в папку `/reports` со всеми компонентами, которые удалось достать.

`npm run report:validate` - сравнит компоненты локального репозитория с продовыми
и напишет дифф. Выдаст ошибку, если локально сущностей стало больше.

`npm run report:codehealth:stat` - соберет и отправит компоненты в виде, который
обрабатывает yandex.stat

`npm run report:codehealth:publish` - парсит и публикует на gh-pages сущности в виде csv
используется после мержа в мастер

