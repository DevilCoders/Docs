# Trendbox-tail

![version](https://badger.yandex-team.ru/npm/@yandex-int/trendbox-tail/version.svg)
[![oko](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/trendbox-tail)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/trendbox-tail)
![owner](https://badger.yandex-team.ru/npm/@yandex-int/trendbox-tail/owner.svg)

Пакет для вывода логов сборки в trendbox.

## Install

```bash
npm install @yandex-int/trendbox-tail -g
```

## Usage

Без параметров выводит список jobs:

```bash
trendbox-tail
```

С параметром выводит хвост сборки этой job с догрузкой по websocket.
В качестве параметра можно передать часть строки названия,
напр. для сборки `ci/trendbox [build]: Publish list of changed packages`
можно написать

```bash
trendbox-tail "Publish list"
```
