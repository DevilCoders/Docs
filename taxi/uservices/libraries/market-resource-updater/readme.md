# Market Resource Updater
Либа для общения с Access Agent'ом и обновлением ресурсов

###  Подключить и настроить потребления ресурса
[Иллюстрационный сервис](https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-uaccess/)
1. Подключить в сервисе библиотеку `yandex-taxi-library-market-resource-updater`. Компонент апдейтера зарегистриуется автоматически.
2. Подготовить модель данных (указать навзание ресурса, реализовать в конструкторе загрузку данных из файлов). Типа [такого](https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-uaccess/src/custom/dependencies.hpp?rev=r9628725#L10)
3. Позвать `AddDataResource` для всех ресурсов и затем `WaitAll`. [Пример](https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-uaccess/src/custom/dependencies.cpp?rev=r9628725#L18)
4. `AddDataResource` Вернет Reader у которого можно [получать](https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-uaccess/src/custom/dependencies.cpp?rev=r9628725#L27) текущую версию ресурса
5. Настроить апдейтер в [конфиге](https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-uaccess/configs/config.user.yaml?rev=r9628725#L20). 


### Локальная разработка
Поднять access-agent: https://a.yandex-team.ru/arcadia/taxi/uservices/services/market-uaccess/dev/start_agent.sh

