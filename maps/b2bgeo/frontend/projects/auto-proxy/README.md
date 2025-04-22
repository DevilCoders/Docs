# nginx auto proxy

## Как сбилдить

1.Залогиниться в registry.yandex.net

```
docker login -u <login> registry.yandex.net
```

Логин со стафа. В качестве пароля токен для приложения у которого есть доступ к docker registry.

2.Собрать docker image

```
docker build . --tag registry.yandex.net/b2bgeo/auto-proxy:1.0
```

3.Push to registry

```
docker push registry.yandex.net/b2bgeo/auto-proxy:1.0
```

## How run local

1.Собрать docker image

```
docker build . --tag registry.yandex.net/b2bgeo/auto-proxy:1.0
```

2.Run

```
docker run -p 80:80 registry.yandex.net/b2bgeo/auto-proxy:1.0
```
