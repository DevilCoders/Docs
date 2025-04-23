# Install provider on control-plane cluster

## Apply resources CRD

1. Go to repo `cd ~/go/github.com/vaspahomov/provider-jet-aws/`
2. Apply CRDs `kubectl apply -f package/crds`

## Add docker creds secret

1. Download puller creds for crossplane-registry from yav. And save sa-key in key.json

2. Add key for cr.yandex for SA

```shell
export DOCKER_CONFIG=~/.docker/sa-config.json
cat key.json | docker login \
--username json_key \
--password-stdin \
cr.yandex
```

3. Create k8s secret with docker-creds

```
kubectl -n crossplane-system create secret generic regcred \
--from-file=.dockerconfigjson=~/.docker/sa-config.json/config.json \
--type=kubernetes.io/dockerconfigjson
```

## Deploy provider

Provider example configurations can be found in [infra/kube/internal/providers](../../internal/providers).
Ask [vaspahomov@](http://staff.yandex-team.ru/vaspahomov) for more info.
