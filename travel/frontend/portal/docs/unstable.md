# Unstable

Это окружение используется для тестирования фич, которые нельзя полноценно протестировать на ферме, например, изменения конфига nginx, можно тестировать тут.

## Сборка и выкатка

Перед сборкой убедитесь, что никто больше не использует unstable в данный момент (можно просто спросить во фронтовом чатике).

Для того чтобы выкатить изменения, надо запустить [сборку в CI](https://a.yandex-team.ru/projects/portalvteam/ci/actions/launches?dir=travel%2Ffrontend%2Fportal&id=deploy-unstable) кнопкой "Run Action", указав нужную ветку.
После чего собирается образ и выкатывается на https://deploy.yandex-team.ru/stages/travel-frontend-portal-unstable.
