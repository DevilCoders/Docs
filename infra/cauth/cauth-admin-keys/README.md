# cauth-admin-keys

Обновление:
Редактируем список админов в файле `admins`. Если нужно удалить ключ существующего пользователя на машине, вносим его логин в `ADMINS_REMOVE_LIST` в `файле debian/postinst`.

Выполняем `mk_src.py`, коммитим результат в репозиторий.

Сборка:
`ya package --debian package.json`

Для сборки необходимы `devscripts`, `dpkg-dev`.
