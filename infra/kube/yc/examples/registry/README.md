# Provision Registry

In this example we'll provision Container Registry

## Prerequisites

* Set up kubernetes environment with crossplane
* Reconciled core resources

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision Registry

1. Create registry

```shell
kubectl --context yc-crossplane apply -f infra/kube/yc/examples/registry/registry.yaml
```

2. Check resources statuses. Wait then both SYNCED and READY becomes True:

```shell
kubectl --context yc-crossplane get -f infra/kube/yc/examples/registry/registry.yaml
```

3. Create Repository

```shell
REGISTRY_ID=$(kubectl --context yc-crossplane get -f infra/kube/yc/examples/registry/registry.yaml -o json | jq -r '.metadata.annotations["crossplane.io/external-name"]')
envsubst < infra/kube/yc/examples/registry/repository.yaml | kubectl --context yc-crossplane apply -f -
```

4. Check registry status

```shell
kubectl --context yc-crossplane get -f infra/kube/yc/examples/registry/repository.yaml
```

## Upload image in registry

1. [Authenticate in docker cli.](https://cloud.yandex.com/docs/container-registry/operations/authentication)

2. Build some image with `docker build`

3. Tag image

```shell
docker image tag sha256:<image-hash> cr.yandex/$REGISTRY_ID/demo-repository:v0.1
```

4. Push image

```shell
docker image push cr.yandex/$REGISTRY_ID/demo-repository:v0.1
```

5. And now you can pull image with:

```shell
docker image pull cr.yandex/$REGISTRY_ID/demo-repository:v0.1
```

## Connect with Managed Kubernetes

[Step by step by Yandex Cloud](https://cloud.yandex.com/en-ru/docs/managed-kubernetes/solutions/container-registry)

## Connect with external Kubernetes with Docker creds

1. Create service Account

2. [Create update docker config](https://cloud.yandex.com/en-ru/docs/container-registry/operations/authentication#sa-json)

3. And now you can find creds in `~/.docker/config.json` under `cr.yandex` section

```shell
cat ~/.docker/config.json
```

## Create Lifecycle Policy

Not supported in provider-jet-yc for now. Can be added in the future.

[How to create lifecycle policy with yc cli.](https://cloud.yandex.com/en-ru/docs/cli/cli-ref/managed-services/container/repository/lifecycle-policy/create)
