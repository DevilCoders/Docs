## create-dobby

Создание `INFRATEST_DOBBY_INTEGRAL` (`DRAFT`) после обновления версий.
[Фильтр с Sandbox-задачами](https://sandbox.yandex-team.ru/tasks?children=false&hidden=false&type=INFRATEST_DOBBY_INTEGRAL).

**NB: Не забудьте в созданной sandbox-задаче указать тикет.**

### Обновление только что опубликованных пакетов на новые версии
```
npx lerna version
...
npx lerna publish from-package
...

npx @yandex-int/create-dobby
...
Creating task
Task created: https://sandbox.yandex-team.ru/task/397656864/view
```

### Обновление пакетов на версии из конкретного коммита (не HEAD)
```
npx @yandex-int/create-dobby --commit 620a344a0ce9b8b0378ca36bdf322fc3e5a5cdeb
...
Creating task
Task created: https://sandbox.yandex-team.ru/task/397656864/view
```

### Обновление всех пакетов на последние актуальные версии 
```
npx @yandex-int/create-dobby --all
...
Creating task
Task created: https://sandbox.yandex-team.ru/task/397656864/view
```
