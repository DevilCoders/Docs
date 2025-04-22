# API Секретницы

* [Список сигналов для Голована](metrics.md)
* [Заметки для разработчиков Секретницы](devdocs.md)

## Гранты

Подвязываем заявки на гранты к тикету [VAULT-636](https://st.yandex-team.ru/VAULT-636).

### Команды для админов

Выдать приложению грант. В комментарии указываем номер тикета с запросом на гратны:
```
sudo -u www-data /usr/lib/yandex/passport-vault/vault_api grants grant 200001 "VAULT-636"
```

Отозвать грант:
```
sudo -u www-data /usr/lib/yandex/passport-vault/vault_api grants revoke 200001
```

Спсиок грантов:
```
sudo -u www-data /usr/lib/yandex/passport-vault/vault_api grants list
```

## Что делать, если надо сменить владельца секрету

Если владелец секрета уволился, но не перевесил секрет на коллег приходится перевешивать секрет. Порядок действий в этом случае следующий:

* Смотрим через ручку API https://vault-api.passport.yandex.net/1/secrets/sec-12345/owners или команду ```vault_api roles info sec-12345``` на сервере список владельцев секрета. Если есть «живые» владельцы, от правляем вопрощающего к ним.
* Если владельцев не осталось, то просим завести тикет в очередь VAULT с Трекере
* Крайне желаетльно перевешивать не на другого человека или группу в Сатфе, а на роль или скоуп в ABC
* После подтверждения от менеджера Секретницы и руководителя уволившегося сорудника, добавляем владельца в секерет командой ```vault_api roles add sec-12345 owner:...```

### Команды для админов

Посмотреть роли для секрета:
```
sudo -u www-data /usr/lib/yandex/passport-vault/vault_api roles info sec-12345
```

Добавить роль для секрета (описание роли как в yav):
```
sudo -u www-data /usr/lib/yandex/passport-vault/vault_api roles add sec-12345 owner:abc:passp:scope:development
```

Найти все роли и скоупы в сервисе (из списка можно сразу скопировать строку с описаним роли для команды roles add):
```
sudo -u www-data /usr/lib/yandex/passport-vault/vault_api find abc (abc_id|abc_slug)
```
