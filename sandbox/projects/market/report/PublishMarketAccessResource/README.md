Для обновления кода таски запусти команду

ya make -r --target-platform=linux && ya upload ./PublishMarketAccessResource -T SANDBOX_TASKS_BINARY --attr release=stable --attr ttl=inf --attr Name=PublishMarketAccessResource --attr version=$(date +"%Y.%m.%d-%H.%M")
