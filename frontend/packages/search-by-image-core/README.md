# search-by-image-core

Библиотека основных утилит поиска по изображению (Сибирь).

Переиспользуется в проектах:
1. [fiji](../../projects/fiji)
2. [web4](../../projects/web4)
3) Умная камера
4) Промо товарной вертикали на морде

## Проверка в связке с основным проектом

### Быстро (локально)

Для быстрой проверки работы изменений этого пакета в связке с основным проектом можно воспользоваться командой [npm-link](https://medium.com/dailyjs/how-to-use-npm-link-7375b6219557):
```
~/arc/arcadia/frontend/projects/fiji › npm link ../../packages/search-by-image-core/
```

Эта команда создаст в node_modules симлинку на данный пакет и его актуальную версию можно будет импортировать, как обычно.

Если потребуется внести изменения в пакет, то чтобы они подтянулись в основной проект, нужно:
1. Пересобрать пакет: `~/arc/arcadia/frontend/packages/search-by-image-core › npm run prepare`
2. Перезапустить котика в основном проекте

После завершения отладки пакета нужно его отлинковать:
```
~/arc/arcadia/frontend/packages/search-by-image-core › npm uninstall
```

### Дольше (локально и на бете)

Отправить команду [`/canary`](https://wiki.yandex-team.ru/lego/autoreleases/).
