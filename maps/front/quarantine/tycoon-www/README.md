# Фронтенд проекта [Tycoon](https://wiki.yandex-team.ru/tycoon/)

[![oko health](https://badger.yandex-team.ru/oko/repo/mining/tycoon-www/health.svg)](https://oko.yandex-team.ru/repo/mining/tycoon-www)

* [Разработка](./docs/DEVELOP.md)
* [Беты/Стенды](./docs/BETA.md)
* [Y.Deploy](./docs/DEPLOY.md)
* [Релиз](./docs/RELEASE.md)
* [Дежурство](./docs/DUTY.md)
* [Инфраструктура](./docs/INFRASTRUCTURE.md)
* [API](./docs/API.md)
* [Docker](./docs/DOCKER.md)
* [Тесты](./docs/TESTS.md)
* [Workflow](./docs/WORKFLOW.md)
* [TVM](./docs/TVM.md)
* [Верстка писем](./docs/EMAILS.md)
* [Рецепты решения проблем](./docs/TROUBLESHOOTING.md)

## Ссылки
* [Яндекс Метрика](https://metrika.yandex.ru/dashboard?group=day&period=month&id=39321485)
* [Ошибки фронта (error-booster)](https://error.yandex-team.ru/projects/sprav/projectDashboard)
* [Ошибки nodejs (Y.Deploy logs)](https://deploy.yandex-team.ru/stages/tycoon-www-production/logs)
* [Скорость фронта](https://rum.yandex-team.ru/projects/sprav/projectDashboard)
* [Алерты Фронт](https://yasm.yandex-team.ru/alert/tycoon-front-errors)
* [Алерты 5xx ошибок](https://yasm.yandex-team.ru/alert/tycoon-server-errors)
* [Алерты 4xx ошибок](https://yasm.yandex-team.ru/alert/tycoon-server-4xx-errors)
* [Алерты балансера tycoon-www-production.sprav.yandex.ru](https://yasm.yandex-team.ru/template/alert/maps-front-tycoon-slb-alerts/)
* [Дашборд ITS для балансера tycoon-www-production.sprav.yandex.ru](https://nanny.yandex-team.ru/ui/#/l7heavy/tycoon-www-production.sprav.yandex.ru)
* [Графики потребления ресурсов инстансами](https://yasm.yandex-team.ru/template/panel/New-Porto-Container/deploy_unit=frontend;geo=man%7Cvla%7Csas;itype=deploy;stage=tycoon-www-production/)
* [График запросов в балансер tycoon-www-production.sprav.yandex.ru](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=tycoon-www-production.sprav.yandex.ru;itype=balancer;ctype=prod;locations=man,sas,vla;prj=tycoon-www-production.sprav.yandex.ru;signal=service_total;)
* [График запросов в балансер knoss_fast](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=knoss_fast;itype=balancer;ctype=prod;locations=man,sas,vla;prj=l7-balancer-knoss-fast;signal=sprav;)
* [Дашборд с графиками сервиса](https://yasm.yandex-team.ru/template/panel/maps-front-tycoon)

## Как заводить эксперименты в ab.yandex-team.ru
После того как в коде реализована функциональность под флагом, надо создать эксперимент в специальной админке - ab.yandex-team.ru. Флоу по созданию\ведению эксперимента [читаем тут](https://wiki.yandex-team.ru/users/vlandreev/jekspy/)

## Поддержка браузеров
* [Метрика](https://metrika.yandex.ru/stat/browsers?period=month&id=39321485&stateHash=5d5e8ee23746fd6d6561048d) (нужен доступ)
* [Процент поддержки браузеров](https://wiki.yandex-team.ru/search-interfaces/SupportedBrowsers/?from=%252Fusers%252Fedragun%252FSupportedBrowsers%252F)

## Использование моков данных
Для использования режима моков необходимо указать переменную окружения `USE_STUB` и присвоить ей значение `1` при запуске сервера:
`USE_STUB=1 npm start`

## Просмотр актуальности зависимостей
https://oko.yandex-team.ru/repo/mining/tycoon-www
Периодически нужно проверять зависимости на уязвимости - https://wiki.yandex-team.ru/product-security/yadi/

Выгрузка переводов в корне проекта: `npm run tanker`.
Переводы коммитятся отдельным коммитом - "Обновление переводов".

## Жучок
https://forms.yandex-team.ru/ext/admin/10019455/settings

## Организация в Testpalm
https://testpalm.yandex-team.ru/organizations/tycoon-www

## Флоу
1. Перед началом работы над задачей переводим тикет в статус «В работу».
2. Если задачу требуется показать менеджеру, то можно создать ПР с префиксом к описанию вида "WIP! TYCOON-123: Новая иконка" (WIP - Work In Progress), автоматически соберется бета, в описании ПР появится ссылка на бету, которую можно отдать для просмотра.
3. Если решение задачи очевидное и вмешательства менеджера не требуется, то разработчик создает pull request, и, после всех проверок, оставляет комментарий `/start` для запуска процесса ревью. Связанный тикет автоматически переводится роботом в статус «На ревью».
4. После ревью в комментариях пуллреквеста пишем `/merge` и ветка вольется в master. После влития ПР, примерно через 40 минут, код появляется в общей бете мастера https://master.beta.sprav.yandex.ru/sprav/.
5. После влития ПР тикет автоматически роботом переводится в статус "Merged to Dev".

## Логи и отладка инстансов
Зайти по ssh в контейнер и заглянуть в `cat /var/log/nginx/*`, в `cat /var/log/nginx/access-tskv.log` лежат обращения с заголовками.
