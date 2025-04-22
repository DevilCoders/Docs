# @ps-int/datasync-client

## Как опубликовать новую версию?

```bash
npm run package X.Y.Z
```

Или, для публикации beta-версии:
```bash
npm run package-beta X.Y.Z-beta.N
```

## Разработка

1. В директории пакета делаем
```bash
npm i
npm link
```
2. В нужном нам "хостовом сервисе" делаем
```bash
npm link @ps-int/datasync-client
```
3. Запускаем сборку в watch-режиме (в screen/tmux/whatever)
```bash
# в директории пакета
npm start
```
