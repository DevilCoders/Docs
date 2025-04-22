Нагрузочное тестирование апи Погоды
Две задачи:
- генерация патронов
- запуск самой стрельбы. Не может запуститься, если не сняты веса бэкендов в Сасово

как запускать локально:
`ya make -r && ./WeatherLoad run --type WEATHER_LOAD`
`ya make -r && ./WeatherLoad run --type WEATHER_LOAD_AMMO_GENERATOR`
Такой ya make запустит 2 сэндбокс таски: MDS_UPLOAD на загрузку бинаря из локального кода + указанную задачу.
Код, по которому запускается задача, указывается в tasks_resource или подставляется руками в UI.

графики трафика https://yasm.yandex-team.ru/chart/signals=balancer_report-report-service_total-outgoing_*xx_summ;hosts=ASEARCH;itype=balancer;ctype=prod;prj=ah.weather-load.yandex.net/?by=hosts
сбилдить ресурс https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=DEPLOY_BINARY_TASK&author=ftlka&limit=20

патроны за дождливый день в Москве
https://sandbox.yandex-team.ru/task/1050622151/view
https://sandbox.yandex-team.ru/task/1050621732/view
