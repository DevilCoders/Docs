# Выдача прав на пакеты ABC-группам

NPM подерживает выдачу прав на ABC-группы через `npm onwer`

## Формат овнеров

Можно дать права на пакет всему сервису, а можно только конкретной роли в рамках сервиса:

- `abc:{SERVICE}` для предоставления доступа всей группе, например `npm owner add abc:npm-repo @yandex-int/verdaccio-main`
- `abc:{SERVICE}:{ROLE}` для предоставления доступа роли в группе, например `npm owner add abc:npm-repo:administration @yandex-int/verdaccio-main`

## Откуда брать названия сервисов и ролей

Чтобы получить название сервиса(slug), нужно зайти на страницу сервиса в ABC из строки адреса взять последнюю часть:
`https://abc.yandex-team.ru/services/npm-repo/` -> `npm-repo`

Получение названия роли чуть сложнее. Для этого необходимо перейти на страницу сервиса,
нажать в списке ролей на нужную роль, после чего взять в качестве названия роли
значение параметра scope из query string:
`https://abc.yandex-team.ru/services/npm-repo/?scope=development` -> `development`

![Пример получения названий](https://jing.yandex-team.ru/files/frimuchkov/Untitled%20Diagram%284%29.png)
