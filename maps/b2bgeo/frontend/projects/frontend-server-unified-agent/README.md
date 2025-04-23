# frontend-server unified-agent

## How to build & push docker image

1.Login in registry.yandex.net

```
docker login -u <staff_login> registry.yandex.net
```

Create OAuth token: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4b14841a33cc458cabc48dca14fa8f2a

2.Build docker image

```
docker build -t registry.yandex.net/b2bgeo/frontend-server-unified-agent:0.2 .
```

3.Push to registry

```
docker push registry.yandex.net/b2bgeo/frontend-server-unified-agent:0.2
```

## How run local

1.Login in registry.yandex.net

```
docker login -u <staff_login> registry.yandex.net
```

Create OAuth token: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4b14841a33cc458cabc48dca14fa8f2a

2.Build docker image

```
docker build -t registry.yandex.net/b2bgeo/frontend-server-unified-agent:0.2 .
```

3.Run

```
docker run -p 80:80 registry.yandex.net/b2bgeo/frontend-server-unified-agent:0.2
```
