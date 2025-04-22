[![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Ir_MboRobotUiDeploy/statusIcon)](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Ir_ModelsClusterizerDeploy)

Выкладка всех пакетов кластеризатора необходимо производить через релизный пайплайн:
https://tsum.yandex-team.ru/pipe/projects/ir/release/new/models-clusterizer

Выбираем нужные компоненты - диспетчер, воркер - которые нужно выложить, указываем фикс-версию из стартрека.

Фикс версию необходимо завести в стартреке:
https://st.yandex-team.ru/MARKETIR/versions
В формате: {год}.{месяц}.{порядковый номер релиза в этом месяце}
После этого привязать тикеты, которые нужно будет выложить к версии в стартреке.
На каждый тикет должен быть заведен пул реквест, который будет добавлен в релиз.

В данном репозитории содержатся три модуля.

### market-models-clusterizer-worker
Создаёт кластера из пачек товарных предложений.

### market-models-clusterizer-dispatcher
Раздаёт задания нескольким worker-ам и использует результаты их работы.

### market-models-clusterizer-common
Общий модуль между `market-models-clusterizer-worker` и `market-models-clusterizer-dispatcher`.
Не публикуется. Все от него должны зависеть по исходникам.
