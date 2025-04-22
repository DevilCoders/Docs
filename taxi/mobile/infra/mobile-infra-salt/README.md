Mobile Linux Salt Server
===========

## Setup before run: **(in progress...)**
- [get docker registry token](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=12225edea41e4add87aaa4c4896431f1)
- authorize in docker registry
```
$ docker login -u $(whoami) registry.yandex.net
Password: <OAuth token body>

Login Succeeded
```

## Build docker image
```
docker build . -t registry.yandex.net/taxi/mobile-infra-salt:${VERSION}

```


## Environment variables

Env variables are used to set config on startup, you can set the following envs

 - `SALT_USE`  - master/minion, defaults to master
 - `SALT_NAME` - minion name, defaults to to master
 - `SALT_GRAINS` - set minion grains as json, defaults to none
 - `LOG_LEVEL` - log level, defaults to info
 - `OPTIONS`   - other options passed into salt process, defaults to none

## Volumes

Following paths can be mounted from the container. `/srv/root` is needed to run your local states.

 - `/etc/salt` - Master/Minion config
 - `/var/cache/salt` - job data cache
 - `/var/logs/salt` - logs
 - `/srv/root` - states, pillar reactors

### Clean all docker stuff 
```
docker stop $(docker ps -a | grep salt-docker | awk '{print $1}') && 
docker rm $(docker ps -a | grep salt-docker | awk '{print $1}') && 
docker rmi $(docker images | grep salt-docker | awk '{print $3}') 
```
