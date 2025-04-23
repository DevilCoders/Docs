## ansible-playbook:

### Использование ansible-playbook:
Применить конфиг:
```ansible-playbook mail_mxback.yml -vvv```

Проверка конфига в dry_run:
```ansible-playbook mail_mxback.yml -vvv -check```

### Установка ansible-playbook:
https://wiki.yandex-team.ru/sm/juggler/ansible/#ansible2.x

Для работы необходим токен в переменной окружения: `JUGGLER_OAUTH_TOKEN`

Получить токен - https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0

### Использование установленнего ansible-playbook в Qloud:
Пололжить токен на рабочей машине, например в: `~/.config/juggler_token`

Подключиться:
```export JUGGLER_OAUTH_TOKEN=$(cat ~/.config/juggler_token); ssh -o SendEnv=JUGGLER_OAUTH_TOKEN ansible-juggler.mail.yandex.net```

Из Аркадии чекаутить так (нужно указать имя пользователя):
``` svn  co svn+ssh://<username>@arcadia.yandex.ru/arc/trunk/arcadia/mail/monitoring/delivery/ansible-juggler-configs```

На машине также утсановлен **jctl**
