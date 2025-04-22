<i>If you see any unactual information here, please fix it by yourself or with help of your chief/mentor.</i>

### Документация
https://wiki.yandex-team.ru/taxi-tech/taxi-scripts/

### Основная информация

В зависимости от того, куда деплоится сервис, папка со скриптами вашего сервиса должна называться по-разному (Системное решение будет реализовано в https://st.yandex-team.ru/TAXIPLATFORM-1716, голосуйте)

#### Сервис на железе 
Папка именуется как ваша кондукторная группа в стейбле 

К примеру, есть папка taxi_supply_diagnostics, в которой лежат некоторые скрипты. Они будут выполняться только на машинках сервиса taxi_supply_diagnostics

#### Сервис в облаке

Папка именуется как имя сервиса в nanny.yandex-team.ru, без постфикса окружения

Пример для https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_metadata-storage_testing/
Папка называется taxi_metadata-storage. Они будут выполняться только на контейнерах сервиса taxi_metadata-storage

В облаках есть важная особенность: в связи c ограничиями процесса выкатки сервисов, окружения для престейбла и стейбла - разные. Если скрипт нужно выполнить на престейбле - папка должна именоваться с постфиксом _pre

https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_metadata-storage_pre_stable/ – taxi_metadata-storage_pre
https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_metadata-storage_stable/ – taxi_metadata-storage

Для улучшения этой ситуации голосовать за тикет: https://st.yandex-team.ru/TAXIPLATFORM-1717
