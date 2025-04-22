blocks
======

## Переводы

Переводами рулить с помощью [tanker-kit](https://github.yandex-team.ru/lego/tanker-kit/). Не забвайте пушить переводы.

## Версионирование

Версию поднимаем, находясь в свежем бранче master. Поднять версию:

```
bower version [<newversion> | major | minor | patch]
```

Где `<newversion>` — валидная строка [semver](http://semver.org/lang/ru/). Например, `v0.3.6`.

Эта команда поменяет версию в `bower.json`, закоммитит это и создаст гит-тег с номером версии. Запушить коммит и тег:

```
git push && git push --tags
```

Не забудьте [добавить описание](https://github.yandex-team.ru/wmfront-common/blocks/releases) вашему релизу. Посмотреть, какие коммиты добавились с прошлого релиза:

```
git log --pretty=oneline tag1..tag2
```

Где `tag1` и `tag2` — теги, между которыми надо посмтреть коммиты. Например, `v0.3.5..v0.3.6`.
