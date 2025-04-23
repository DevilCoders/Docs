# parsing

## Описание

Сервис принимает информацию об объявлениях на сайтах конкурентов от внешних парсеров. Сохраняет и обновляет их в своей в базе, ведет учет изменений. Осуществляет дальнейшую обработку, дообогащение и фильтрацию. Отправляет в связанные системы для последующей аналитики, а также обзвона силами коллцентров для размещения у нас с согласия владельцев. Также ведет статистику размещений спарсенных объявлений в нашем сервисе и статистику дозагрузки фотографий владельцами. Отслеживает статус объявлений на сайтах конкурентов и помечает снятые с продажи.

## Документация

https://wiki.yandex-team.ru/vertis/comtransparsing/

## Проект в тимсити

https://t.vertis.yandex-team.ru/project.html?projectId=VerticalsBackend_Parsing

## Чаты

parsing deployment: https://t.me/joinchat/BKuv7xe40v2Xc_YvD4uzaA

parsing monitoring: https://t.me/joinchat/BKuv7xCIxBOth8pLXvylzA (сюда падают алерты из дашборда в графане parsing-alerts)

## Метрики

parsng-alerts: https://grafana.vertis.yandex-team.ru/d/AQzuhDVik/parsing-alerts?orgId=1&refresh=1m

Остальные метрики - выпадающим списком справа сверху.

## Сборка и тесты

    Локально: mvn clean install
    В тимсити: https://t.vertis.yandex-team.ru/buildConfiguration/VerticalsBackend_Parsing_ParsingCompileRunTestsArcadia?mode=builds

## Выкладка в дев

    ./deploy-api.sh
    ./deploy-scheduler.sh

## Релиз

В проекте тимсити есть сборки Release Api и Release Scheduler. Нажимаем Run нужной сборки, через некоторое время модуль выкатится в тестинг (если все ок), и об этом придет уведомление в чат https://t.me/joinchat/BKuv7xe40v2Xc_YvD4uzaA (parsing deployment). Для отправки в прод, можно нажать в чате на ссылку promote

## Дженкинс

https://j.vertis.yandex-team.ru/job/Deploys/job/Parsing

## Выкладка в тестинг без тимсити

Например, выкладка в тестинг из ветки (правда, тестинг всего один)

В проекте parsing:
./changes.sh parsing-api #либо parsing-scheduler

Обновляется файл parsing-api/CHANGELOG.md. Коммитим его:
git commit -am 'changes'

Вызываем скрипт dockerrelease.sh:
./dockerrelease.sh parsing-api

Скрипт соберет докер-образ, отправит его в регистри и дернет выкладку из него в тестинг в дженкинсе.

test

## git-hooks
To enable git hooks you need to cd to `<project directory>/scripts/hooks` and run
`chmod +x setup-git-hooks.sh && ./setup-git-hooks.sh`

If you need to update hooks, just run `./setup-git-hooks.sh` after pulling changes from github.
