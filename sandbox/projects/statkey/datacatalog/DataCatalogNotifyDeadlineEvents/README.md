Для обновления кода таски запусти команду:

`ya make -r --target-platform=linux &&
ya upload ./DataCatalogNotifyDeadlineEvents -T SANDBOX_TASKS_BINARY --attr version=$(date +"%Y.%m.%d-%H.%M") --attr release=stable --attr name=DataCatalogNotifyDeadlineEvents --ttl=inf`
