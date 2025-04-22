> :warning: **Project Stub устарел**

> Рекомендуется вместо него использовать  
**[стаб для новых проектов в монорепе](https://a.yandex-team.ru/arc_vcs/frontend/services/stub).**

[![](https://drone.yandex-team.ru/api/badges/toolbox/project-stub/status.svg)](https://drone.yandex-team.ru/toolbox/project-stub)
![](https://badger.yandex-team.ru/npm/@yandex-int/generator-project-stub/version.svg)
![](https://badger.yandex-team.ru/npm/@yandex-int/generator-project-stub/owner.svg)
[![oko generator-project-stub](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/generator-project-stub)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/generator-project-stub)


## Документация

* [Как развернуть проект на основе Project Stub](https://wiki.yandex-team.ru/toolbox/project-stub/how-to-start/)

## Разработка

```sh
npm link

# Запускаем сборку генератора
npm run watch

# Для того чтобы протестировать генератор вызываем
yo @yandex-int/project-stub
```

## Публикация

Переключаемся на _master_ и подтягиваем свежие изменения.

Далее выполняем команду:
```sh
npm run release <version> <npm-tag>
```

Например:

```sh
# Выпускаем релизы
npm run release patch latest
npm run release minor latest
npm run release major latest
npm run release 7.0.0 latest

# Выпускаем пререлизы
npm run release prepatch next
npm run release preminor next
npm run release prepatch next
```
