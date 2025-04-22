# promozavr
![npm stable version](https://badger.yandex-team.ru/npm/@ps-int/promozavr/version.svg)

Показывающий код для промок Яндекс 360

## Разработка

1. В директории пакета делаем
```bash
npm i
npm link
```
2. В нужном нам "хостовом сервисе" делаем
```bash
npm link @ps-int/promozavr
```
3. Запускаем сборку в watch-режиме (в screen/tmux/whatever)
```bash
# в директории пакета
npm start
```

### Сборка и публикация

```bash
# в директории пакета
# версия по semver
npm run package X.Y.Z
```
