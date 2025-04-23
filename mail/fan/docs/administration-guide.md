# Администрирование

## Создание аккаунта

Команда для создания аккаунта в системе:

    delivery1p:~$ /usr/lib/yandex/fan/bin/manage.py create-account --id=yandex.mail --title="Яндекс.Почта" --users=kapp,aaz

создаёт аккаунт и добавляет роль "Пользователь" логинам, указанным в параметре users.

## Работа с отписками

Утилита, чтобы удалить отписку:

   $ /usr/lib/yandex/fan/bin/manage.py ununsubscribe --emails='a@b.c,d@e.f'
