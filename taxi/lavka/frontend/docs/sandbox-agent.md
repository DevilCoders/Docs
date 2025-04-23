## Как зайти на агент
{% cut "Нажимаем на кнопку Suspend (пауза)" %}

![ci flow example](_images/sandbox-agent/suspend.png "ci flow example")

{% endcut %}

Ожидаем перехода в статус `Suspended` (через `Suspending`)

Появляется кнопка `Open shell`, она открывает новое браузерное окно:
{% cut "Скрин" %}

![open shell example](_images/sandbox-agent/open-shell.png "open shell example")

{% endcut %}

По-умолчанию окно может быть маленьким (зависит от браузера), нужно увеличить его размер:
{% cut "Скрин" %}

![open shell example](_images/sandbox-agent/open-shell-example.png "open shell example")

{% endcut %}

## Вернуть Аркадию
`Suspend` ставит процесс arc на паузу, поэтому его нужно возобновить - послать сигнал SIGCONT
```bash
kill -CONT $(pidof arc)
```

После этого можно зайти в директорию с Аркадией:
```bash
cd ./mounted_arcadia/taxi/lavka/frontend
```
