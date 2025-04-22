branch-tools
============

## Утилиты для работы с ветками

https://wiki.yandex-team.ru/balance/frontend/projects/balance/dev/sborka-stendov

### `branch-bash`

  Запускает bash внутри ветки с правильной геометрией терминала

### `branch-binary-restart`

  Перезапускает ветку

### `branch-binary-upload`

  Загружает бинарь на 2h

### `branch-clean`

  Удаляет branches-testing/$branch и /var/log/branches-testing/$branch

### `branch-front`
  Вызывается например как `branch-front BALANCE-12345 admin-user-static`
  Доступные опции `no/admin/user/static/admin-user/admin-user-static`

## Сборка

  Сборка в TeamCity: https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Billing_Orchestra_YbBranchTools

## Установка

Автовыкладка не настроена, нужно обновить пакеты вручную:
```(sh)
greed-dev2h.paysys ~ $ sudo apt-get update && sudo apt-get install yb-branch-tools
```

## Разработка

  Изменения можно оформлять пулл реквестами или сразу пушить в master
