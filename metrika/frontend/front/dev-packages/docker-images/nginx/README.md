## Сборка и выкладка новой версии образа
### С помощью Sandbox
Версию образа именуем в формате `{NGINX_VERSION}-{UBUNTU_VERSION}-{COMMIT_HASH}`, например `metrika/frontend/nginx:1.17.5-bionic-fd33054`

Клонировать [`задачу`](https://sandbox.yandex-team.ru/task/818493937/view) и подправить параметры:
- `Description` - исправить версию nginx и хеш коммита
- `Commit` - хеш коммита
- `Tags to publish image with` - поменять версию nginx и хеш коммита. можно целиком скопировать из `Description`
- `Docker --build-arg option` - поменять версию nginx

### Сборка локально
```(bash)
$ docker build --network=host --build-arg NGINX_VERSION=1.17.5 -t nginx_test -f nginx.dockerfile .
```
