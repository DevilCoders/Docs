# ghost

### Описание
Сервис, снабжающий данными отчеты Почты на Statface.

[Вебфейс](https://stat.yandex-team.ru/Mail/CapacityPlanning/Mail) отчетов Почты.\
[Дашборд](https://stat.yandex-team.ru/Dashboard/MailDashboard?tab=100ct), построенный над этими отчетами.

### Разработка
Основной [референс](https://wiki.yandex-team.ru/statbox/Statface/externalreports/) по работе со Statface.\
Sandbox [job](https://sandbox.yandex-team.ru/scheduler/17906/view)-а, в рамках которой запускается сервис.\
[Креды](https://sandbox.yandex-team.ru/admin/vault?owner=robot-capacity-plan&limit=20), которые использует Sandbox-задача.\
[Они же](https://yav.yandex-team.ru/secret/sec-01dpp7e0zbb6kedej5nsnwmwrz/explore/versions), доступные для просмотра.

#### Workflow

Будучи запущенным, сервис
1. получает (синхронно) различные метрики Почты из внутренних сервисов Яндекса (Golovan, QLOUD, Solomon).\
Каждая из метрик представлена соответствующим классом, реализующим интерфейс `IResourceCalculator`.

2. загружает (синхронно) полученные данные на Statface посредством его публичного API.

#### Запустить руками
В коде список опций и семантику можно увидеть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/mail/ghost/bin/utils.py?rev=5881036#L36)

Примеры:
```
$ ya make
$ ./bin/ghost -l # посмотреть все имеющиеся калькуляторы
$ export TOKEN=... # добавить в env токены из секрета
$ ./bin/ghost -r mail.ghost.calculators.so.so_cpu.SOCpuCalculator # запустить нужный калькулятор; без опции -r запустятся все; с опцией -dr результаты залогируются в консоль, но не будут отправлены в отчет
$ ./bin/ghost -r mail.ghost.calculators.so.so_cpu.SOCpuCalculator -i 4 2 # собрать статистику в интервале [today - begin; today - end); например, если сегодня 04.12.2020, то будет собрана статистика за 30.11 и 01.12
```

#### Y.Deploy

https://yd.yandex-team.ru/stages/mail_ghost

#### TODO

Планы по развитию компонента мы строим [здесь](https://st.yandex-team.ru/MAILDLV-3691).
