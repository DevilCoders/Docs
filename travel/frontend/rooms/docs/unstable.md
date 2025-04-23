# Unstable

Это окружение используется для тестирования фич, которые нельзя полноценно протестировать на ферме, например, изменения конфига nginx, можно тестировать тут.

## Сборка и выкатка

Для того чтобы выкатить изменения, надо запустить [сборку в Teamcity](https://teamcity.yandex-team.ru/buildConfiguration/DataUI_YaTravel_YaTravelFrontend_BuildFromBranch?branch=__myBranchesProvider-myBranches__&buildTypeTab=overview&mode=builds) с выбранной веткой.

После сборки таска, можно выкатывать готовый образ на unstable.

Необхожимо убедится, что никто больше не использует unstable в данный момент.
