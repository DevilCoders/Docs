Для обновления кода таски запусти команду

ya make -r --target-platform=linux && ya upload ./moneymap_monitorings -T SANDBOX_TASKS_BINARY --attr version=$(date +"%Y.%m.%d-%H.%M") --attr released=stable --attr task_type=MONEYMAP_MONITORINGS --ttl=inf

Если нет ssh ключа (через который происходит получение sandbox токена) нужно ещё его добавить:
SANDBOX_TOKEN=<токен>

ya make -r --target-platform=linux && ya upload ./moneymap_monitorings -T SANDBOX_TASKS_BINARY --attr version=$(date +"%Y.%m.%d-%H.%M") --attr released=stable --attr task_type=MONEYMAP_MONITORINGS --token $SANDBOX_TOKEN --ttl=inf
