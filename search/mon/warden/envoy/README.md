## Envoy proxy

> NOTE: provided configuration is nothing but "make it work" compilation of what was found in different guides
and issue discussions. Needs to be seriously reconsidered

### Setup

Brief howto for docker on QYP: https://wiki.yandex-team.ru/users/vmazaev/docker-v-qyp/

Envoy via docker: https://www.envoyproxy.io/docs/envoy/latest/start/install#install-envoy-using-docker

### Run
r
> NOTE: docker will fail to mount file from ARC, so copy it somewhere else, e.g. home dir

> NOTE: `$PORT` (8080) is the port to which UI proxies backend requests

```
CFG="${ARCADIA_ROOT}/search/mon/warden/envoy/envoy.yaml"
cp $CFG ~/
PORT=8080
docker run --rm -it \
      -v ~/envoy.yaml:/envoy.yaml \
      -p $PORT:$PORT \
      --name envoy \
      envoyproxy/envoy-dev \
          -c envoy.yaml
```
