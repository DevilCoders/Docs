## Сборка и выкладка новой версии образа
### С помощью Sandbox
Версию образа именуем в формате `{NODE_VERSION}-{UBUNTU_VERSION}-{COMMIT_HASH}`, например `metrika/frontend/node:12.19.0-bionic-4f65ec1`

Клонировать [`задачу`](https://sandbox.yandex-team.ru/task/818492361/view) и подправить параметры:
- `Description` - исправить версию nodejs и хеш коммита
- `Commit` - хеш коммита
- `Tags to publish image with` - исправить версию nodejs и хеш коммита. можно целиком скопировать из `Description`
- `Docker --build-arg option` - исправить версию nodejs

### Сборка локально
```(bash)
$ docker build --network=host --build-arg NODE_VERSION=12.19.0 -t node_test -f nodejs.dockerfile .
```
