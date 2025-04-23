# Templar

**DEPRECATED: templar устарел, используйте [kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html).**

NodeJS-приложение для выполненния `priv`/`bemtree`-файлов

Назначение: локальная разработка и тестирование.

[F.A.Q.](https://wiki.yandex-team.ru/search-interfaces/infra/templar/faq/)

## Минимальные требования
* OS X 10.8.x - 10.11.x, Linux
* nodejs >= 4 (мы рекомендуем использовать [nvm](https://github.com/creationix/nvm))

## Быстрый старт (на примере web4)
```
cd ~/wc1/web4
npm install @yandex-int/templar --registry https://npm.yandex-team.ru
npx templar start -sd
```

Темплар автоматически сгенерирует сертификаты, добавит их в KeyChain и запустит локальный DNS.

Рабочая копия будет достуна по адресам:

* десктоп: https://local.yandex.ru:3443/search/?text=test
* тач: https://local.yandex.ru:3443/search/touch/?text=test
* пад: https://local.yandex.ru:3443/search/pad/?text=test

## Быстрый старт (на примере fiji)
```
cd ~/fiji
npm install @yandex-int/templar --registry https://npm.yandex-team.ru
npx templar start -sd
```
Рабочая копия будет доступна по адресам:

* https://local.yandex.ru:3443/images/search?text=bmw
* https://local.yandex.ru:3443/images/touch/search?text=bmw
* https://local.yandex.ru:3443/images/pad/search?text=bmw
* https://local.yandex.ru:3443/video/search?text=bmw
* https://local.yandex.ru:3443/video/touch/search?text=bmw
* https://local.yandex.ru:3443/video/pad/search?text=bmw
