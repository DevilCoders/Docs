# How to use

Workspace dir `solomon/j/solomon-alert`

##### Login into docker registry.yandex.net
For push and pull images from registry required sing up.

Get oAuth token [here](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
```bash
docker login -u ${USER} -p ${OAUTH_TOKEN} registry.yandex.net
```

##### Build image
Build source code into image with tag `registry.yandex.net/${USER}/solomon-alert:latest`
```bash
make build
```

##### Publish into registy
```bash
make push
```
