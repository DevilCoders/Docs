## Run and push docker image

```
docker build . -t registry.yandex.net/taxi/mobile-linux-buildagent/testing:0.0.1 .

docker push registry.yandex.net/taxi/mobile-linux-buildagent/testing:0.0.1
```

## Run docker image 

```
docker run -e QLOUD_MEMORY_LIMIT=8000000000 -e QLOUD_ENVIRONMENT=qloud.test.local -e QLOUD_INSTANCE=1 -it registry.yandex.net/taxi/mobile-linux-buildagent/testing::0.0.1
```

## Read about authorization in registry

https://wiki.yandex-team.ru/qloud/docker-registry/#authorization

## Read wiki mobile agents

https://wiki.yandex-team.ru/users/irbis/android/teamcity-agenty-v-qloud/# android-buildagent-qloud
