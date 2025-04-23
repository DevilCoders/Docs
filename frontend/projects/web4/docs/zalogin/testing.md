# Тестирование залогина

## hermione-auth-commands
[Пост в этушке](https://clubs.at.yandex-team.ru/search-interfaces/4157)

## TUS
[Страница на вики](https://wiki.yandex-team.ru/tus/)

[tus-cli](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/tus-cli) - для добавления аккаунтов в TUS.

tl;dr плагин для гермионы, который позволяет использовать реальные паспортные аккаунты при тестировании.
В обычных тестах данные о залогине записываются в дамп при его сохранении, в интеграционных происходит настоящая авторизация.

## Hermione
Если в вашем тесте необходима лишь залогиненность и у вас нет ajax запросов, то достаточно использовать параметр `yandex_login`.

Если необходим аккаунт с определенным состоянием, воспользуйтесь форевердатой из списка ниже.

Если в тесте присутствует ajax запросы, в которых проверяется залогиненность, воспользуйтесь командой `authOnRecord(login)` из TUS.
[Пример](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/features/touch-phone/burger-menu/burger-menu.hermione.js?#L228)

`login` - произвольное имя аккаунта. Лучше использовать логин, который уже есть в тестах, например `plain-user`.

Если в тесте необходим конкретный аккаунт или конкретное состояние аккуанта, добавьте его в TUS через `tus-cli`, а после
используйте в тесте `yaAuthOnRecord(login, { prefix: '' })`.

Пример добавления аккаунта: `tus-cli --consumer=web4 --env=prod save -l <login> <password>`

## Hermione e2e
Для интеграционных тестов на залогин используйте команду `auth(login, { prefix: '' })`. [Пример](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/web4/features/deskpad/authorization/authorization.hermione.e2e.js)

## Как проверить валидность ссылки на паспорт
Воспользуйтесь хелпером `yaCheckPassportLink()`, он умеет проверять корректность ссылки на паспорт, параметры и счетчики.

## Полезности
- [Список форевердат с различными аккаунтами на wiki](https://wiki.yandex-team.ru/zalogin/z-team/tipy-akkauntov-pasporta/)
