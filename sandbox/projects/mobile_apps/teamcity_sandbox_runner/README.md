### Как выкатить новую версию TSR
TSR - это бинарная sdk2 задача, так как мы используем код из аркадии. По этому для выкатки новой версии, нужно выложить бинарь с правильными атрибутами. Это можно сделать следующей комбинацией команд.

    cd arcadia/sandbox/projects/mobile_apps/teamcity_sandbox_runner/bin
    ya make
    ./bin upload --attr target=teamcity_sandbox_runner/bin --attr version=<tsr-version> --attr release=stable --token <sb-token>
    
*sb-token можно получить [тут][1]

[1]: https://sandbox.yandex-team.ru/oauth/token "oauth-token"