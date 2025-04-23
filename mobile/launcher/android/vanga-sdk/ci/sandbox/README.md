##Сборка catboost

* config.yaml - конфиг для запуска сборки в sandbox
* build_catboost.sh - скрипт для сборки (выкачивает ресурсы из аркадии, собирает catboost и создаёт PR)

Сборка в тимсити: [Vanga:Build catboost](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=MobileNew_Monorepo_Launcher_Vanga_BuildCatboost&tab=buildTypeStatusDiv)

Созданный pull request можно найти тут - [monorepo](https://bb.yandex-team.ru/projects/MOBILE/repos/monorepo/pull-requests?state=OPEN&at=refs%2Fheads%2Flauncher%2Fandroid%2Fvanga-sdk%2Fnext-release)

Задача на разработку - [PHONE-6375](https://st.yandex-team.ru/PHONE-6375)

В конфиге мы указываем наш собственный контейнер lxc [1179213200](https://sandbox.yandex-team.ru/task/533775585/view), с поддержкой SVN.
Полное описание параметров для config.yaml находится в Wiki - [Generic Teamcity Runner](https://wiki.yandex-team.ru/mobvteam/sandbox-runner/)
