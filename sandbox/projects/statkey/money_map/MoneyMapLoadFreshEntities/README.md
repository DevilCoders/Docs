Для обновления кода таски запусти команду

ya make -r --target-platform=linux && ya upload ./MoneyMapLoadFreshEntities -T SANDBOX_TASKS_BINARY --attr version=$(date +"%Y.%m.%d-%H.%M") --attr release=stable --attr Name=MoneyMapLoadFreshEntities --ttl=inf
