# Монорепозиторий Market CMS

[![oko](https://badger.yandex-team.ru/oko/repo/market-java/embedded-cms-annex/health.svg)](https://oko.yandex-team.ru/repo/market-java/embedded-cms-annex)

# Публикация пакетов

Перед публикацией необходимо залогиниться под роботом `robot-mbo-front`:

```bash
npm login --registry=https://npm.yandex-team.ru
```

Проверить что все в порядке:

```bash
npm whoami --registry=https://npm.yandex-team.ru
```

Должен быть выведен логин пользователя:

```bash
robot-mbo-front
```

Переходим на master ветку и получаем последние изменения:

```bash
git checkout master
git pull origin master
```

Желательно выполнить чистую установку:

```bash
node_modules/.bin/lerna clean -y
rm -rf node_modules
npm ci
```

И пытаемся опубликовать пакеты:

```bash
node_modules/.bin/lerna publish -y --graph-type=all --registry=https://npm.yandex-team.ru
```

Если все прошло успешно, то `lerna` должна была запушить изменения в master ветку и опубликовать пакеты в npm.

Если же возникли ошибки и `lerna` успела запушить изменения, но не опубликовала пакеты в npm, то для публикации нужно использовать следующую команду:

```bash
node_modules/.bin/lerna publish from-package -y --graph-type=all --registry=https://npm.yandex-team.ru
```
