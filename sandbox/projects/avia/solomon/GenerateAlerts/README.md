## Генерация алертов в Solomon

### Сборка бинарной таски

1. Чекаутим код бинарных тасок: `./ya make --checkout -j0 sandbox/projects/avia/solomon/GenerateAlerts`
1. Переходим в папку с кодом таски: `cd sandbox/projects/avia/solomon/GenerateAlerts`
1. Собираем бинарник: `ya make -r --checkout --yt-store`
1. Загружаем бинарник в sandbox: `./GenerateAlerts run --create-only --type AVIA_SOLOMON_GENERATE_ALERTS --attr task_type=AVIA_SOLOMON_GENERATE_ALERTS`

