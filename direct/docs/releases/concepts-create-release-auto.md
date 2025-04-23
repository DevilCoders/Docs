# Сборка релизов по крону

Статус документа и самой сборки релизов по расписанию: в разработке.
Работает для релизов: dna и direct.

## Из чего состоит

Сверху вниз по порядку вызовов:

- crontab на одном из ppcdev (последний раз ppcdev7), искать так: `grep create-release-auto /etc/cron.d -r` — здесь расписание сборок
- скрипт `dt-autorelease-ctl` для управления настройками автосборки — самый главный для пользователей
- скрипт `dt-create-release-auto.py`
- скрипт `direct-release`

## dt-autorelease-ctl
Самый популярный сценарий — поменять QA-инженера. Это делается так (приложение в `-a` подставлять свое):
```sh
dt-autorelease-ctl -a java-logviewer schedule --qa 'staff:lena-san'
```

Проверить, подходит ли текущее время для сборки релиза:
```sh
dt-autorelease-ctl -a java-logviewer check
```

Форсировать запуск сборки (робот начнёт пробовать сразу же и будет продолжать пробовать 3 часа):
```sh
dt-autorelease-ctl -a java-logviewer force
```

Посмотреть расписание/текущие команды:
```sh
dt-autorelease-ctl -a java-logviewer show
```

Больше подробностей по `-h`
```sh
dt-autorelease-ctl -h
```

## Форсирование сборки
Если нужна повторная сборка во временное окно, уже настроенное в расписании, то достаточно воспользоваться командой
```sh
dt-autorelease-ctl -a <app> clear-last-try
```

Если же требуется сборка вне стандартного временного окна данного релиза, то ее можно форсировать через команду
```sh
dt-autorelease-ctl -a <app> force
```
При необходимости очистив поле `last-try` командой выше.

Если при попытке форсировать сборку `dt-autorelease-ctl` ругается на наличие значения в поле cmd, то его можно очистить командой
```sh
dt-autorelease-ctl -a <app> clear-cmd
```

Для сборки релизов dna и java-web может пригодиться параметр -i (insistence): при значении не меньше 2 игнорируется [наличие "парных" релизов](https://a.yandex-team.ru/arc/trunk/arcadia/direct/infra/direct-utils/direct-release-tools/bin/dt-create-release-auto.py?rev=r8329083#L134):
```sh
dt-autorelease-ctl -a <app> force -i 2
```

## dt-create-release-auto.py

dt-create-release-auto.py делает:

- выставляет переменные окружения, чтобы `direct-release` нашел роботные токены, не слал уведомления и т.п.
- перенаправляет вывод `direct-release` в файлы в `/var/log/yandex/autoreleases`

Должен научиться:

- отправлять события в juggler
- определять assignee из каких-нибудь дежурств
- отправлять ТГ-уведомления "релиз собрался"
- создавать события в Инфре "релиз собирается"
- и т.д.

С вопросами и предложениями приходите к lena-san@

