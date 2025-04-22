## Описание
Содержит ряд утилит, написанных на Python, для выполнения служебных операций - сжатия таблиц, управления бэкапами, подготовкой данных для аналитиков и т.д.

Все задачи могут быть запущено локально (правда ряд из них в read-only режиме) из [main.py](bin/main.py).

Задача сделаны так, чтобы они могли запускаться в Sanbdox.

## Задачи в Sandbox

Список всех задач: [https://sandbox.yandex-team.ru/schedulers?author=robot-pricelabs](https://sandbox.yandex-team.ru/schedulers?author=robot-pricelabs)

Все они настроены для запуска из-под пользователя **robot-pricelabs**

Исходники всех задач можно найти в [/sandbox/projects/market/pricelabs](../../../../sandbox/projects/market/pricelabs)


### Как задеплоить новую версию таски
Мы используем бинарные таски Sandbox-а, которые должны быть загружены перед использованием:
1) [https://clubs.at.yandex-team.ru/arcadia/16437](https://clubs.at.yandex-team.ru/arcadia/16437)
2) [https://wiki.yandex-team.ru/sandbox/tasks/build](https://wiki.yandex-team.ru/sandbox/tasks/build)

Т.е. изменение исходников в trunk не приводит к обновлению задачи, ее нужно именно загрузить в Sandbox.

Если потребуется обновить таску, то делаем следующее: 
1) Находим Linux машину (например, виртуалку QYP)
2) Компилируем таску: `ya make sandbox/projects/market/pricelabs`
3) Деплоим скомплированную таску в Sandbox: `sandbox/projects/market/pricelabs/bin/market-pricelabs upload --attr target=market/pricelabs/task --attr release=stable`
Она будет автоматически подтянута при следующем запуске задачи такого типа (ручной или через scheduler).

**Note:** новая версия автоматически применится и к задачам в тестовом окружении, и в продуктовом.

### Детали Sandbox таски
Для управления секретами токен делегирован: [https://wiki.yandex-team.ru/sandbox/yav/#permissions](https://wiki.yandex-team.ru/sandbox/yav/#permissions)
