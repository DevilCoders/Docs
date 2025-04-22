# Релизный процесс

У проекта есть два продовых окружения: [production](https://deploy.yandex-team.ru/stages/travel-frontend-rasp-production) и [prestable](https://deploy.yandex-team.ru/stages/travel-frontend-rasp-prestable). В prestable идет 5% от всего продового трафика. То есть в prestable идет 5% трафика, а в production 95%. Данное деление трафика происходит на [Awacs-балансере](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-prod-rasp-balancer/show/).

Prestable играет роль последней проверки релиза на уже реальных пользователях. В случае, если релиз будет содержать какую-то ошибку, то от нее пострадают только 5% пользователей. Так же логика на балансере устроена так, что в случае возникновения 5xx ошибки при обработке GET-запроса, данный запрос будет передан в следующее окружение (production или prestable), что может снизить вероятность ошибки.

По-умолчанию при переходе на продакшен сервиса (https://rasp.yandex.ru) нельзя определить куда именно вы попали: на production или prestable. Более того, часть запросов (включая основной и ajax), могла быть обработана на production, а другая часть на prestable.

Но есть гарантированный способ попасть на production или prestable. Для этого нужно модифицировать заголовки запросов добавив заголовок `X-Force-To-Prestable: prestable` для того чтобы попасть на prestable или `X-Force-To-Prestable: stop`, чтобы попасть на production. Для этого можно скачать расширение для браузера, которое умеет патчить заголовки для всех запросов, включая ajax, например [modHeader](https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj) для Chrome.

## Выкатка релиза вручную

-   В окружении YDeploy (например [prestable](https://deploy.yandex-team.ru/stages/travel-frontend-rasp-prestable)) перейти на вкладку "Config"
-   нажать кнопку "edit" в правом верхнем углу
-   Выбрать box "server"
-   Выбрать вкладку "resources"
-   Отредактировать путь к docker-образу

Выглядит это примерно так: ![ydeployChangeDockerImage](/docs/images/ydeployChangeDockerImage.png)

## Откатить релиз на предыдущий

-   В окружении YDeploy (например [prestable](https://deploy.yandex-team.ru/stages/travel-frontend-rasp-prestable)) перейти на вкладку "History"
-   Выбрать нужный релиз в истории и нажать на кнопку "apply"
-   Выбрать "apply with changes"
-   Нажать на кнопку "Update" в правом верхнем углу
-   Тут может вылезти попап с предложением что-нибудь обновить, например апнуть версию podAgent. Лучше не соглашаться на эти изменения, потому что они могут вызвать ошибки совместимости, переаллокацию подов и прочее, а вы наверное не о хорошей жизни откатываетесь и не нужны вам эти лишние неприятности
-   Сравнить изменения и закоммитить их

## Шаги по выкатке релиза (это инструкция для разработчиков, для тестировщиков лежит [здесь](https://wiki.yandex-team.ru/travel/rasp/dev/qa/processnaja-dokumentacija/releaseprocess/))

-   После мерджа ПР в trunk, в CI автоматически запускается [релиз](https://a.yandex-team.ru/projects/portalvteam/ci/releases/timeline?dir=travel%2Ffrontend%2Frasp&id=release)
-   Если ПР еще в тестинге, все новые релизы вытесняют старые. Если на момент мержа, релизный тикет уже был создан, создается новый релиз (без перезаписывания старого)

Шаги:

1. тестировщик, собирает [релиз](https://a.yandex-team.ru/projects/portalvteam/ci/releases/timeline?dir=travel%2Ffrontend%2Frasp&id=release)
2. проверяет релиз в [тестинге]https://testing.morda-front.rasp.common.yandex.ru/ и [тач](https://t.testing.morda-front.rasp.common.yandex.ru/)
3. сообщает дежурному-фронтендеру, что нужно выкатить релиз в престейбл.
4. дежурный-фронтендер контроллирует поведение prestable через [дашборд с показателями сервера](https://datalens.yandex-team.ru/huurcsd89uwse-travel-frontend?tab=9l4&state=95bd2e72112) и через [дашборд с ошибками](https://error.yandex-team.ru/projects/travel/projectDashboard?filter=service%20%3D%3D%20rasp.frontend) (к сожалению на данный момент на нем нет возможность посмотреть ошибки только для prestable).
5. После того как убедимся что с релизом все хорошо. Катим релиз в production.
6. Смотрим на приборы в production
    - [Дашборд с показателями сервера](https://datalens.yandex-team.ru/huurcsd89uwse-travel-frontend?tab=9l4)
    - [Дашборд с ошибками](https://error.yandex-team.ru/projects/travel/projectDashboard?filter=service%20%3D%3D%20rasp.frontend)
7. Если с релизом все ок, тестировщик закрывает [релиз](https://a.yandex-team.ru/projects/portalvteam/ci/releases/timeline?dir=travel%2Ffrontend%2Frasp&id=release)
