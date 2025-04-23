# CoverLayer
![npm stable version](https://badger.yandex-team.ru/npm/@ps-int/cover-layer/version.svg)

Компонент для отображения больших фоновых картинок и видео.

Инкапсулирует лучшие подходы по отображению разных форматов.

Постулирует набор файлов необходимых к передаче в разработку.

Подробное описание будет позже.

## Разработка

### В Storybook

```bash
npm ci
npm run storybook
```

### В сервисе

1. В директории пакета делаем
```bash
npm i
npm link
```
2. В нужном нам "хостовом сервисе" делаем
```bash
npm link @ps-int/cover-layer
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
