# PostgreSQL application

In this guide we'll:

* Build docker image of application that works with PostgreSQL
* Push image in existing docker registry
* Add docker credentials to pull image from kubernetes
* Create kubernetes secret with credentials of existing postgresql
* Deploy application that works with existing postgresql

## Prerequisites

* Deployed docker registry. Explore examples:
    * [~~Azure~~](../../../azure/examples/registry)
    * [~~AWS~~](../../../aws/examples/registry)
    * [~~YC~~](../../../yc/examples/registry)

* Deployed PostgreSQL. Explore examples:
    * [Azure](../../../azure/examples/postgresql)
    * [AWS](../../../aws/examples/postgresql)
    * [YC](../../../yc/examples/postgresql)

## Step by step

1. Build image

Example image can be found in [infra/kube/examples/demo-images/http-pg-image](../../demo-images/http-pg-image). Go
there:

```shell
cd infra/kube/examples/demo-images/http-pg-image
```

Build image

```shell
docker build
```

2. Push image in registry

```shell
REGISTRY_URL="<set url of your registry here>"
docker image tag <sha256 hash from build command output> $REGISTRY_URL/demo/http-pg-image:v0.1
docker image push $REGISTRY_URL/demo/http-pg-image:v0.1
```

3. Modify docker credentials for kubernetes.

Your local credentials can be found with:

```shell
cat ~/.docker/config.json
```

Replace `.dockerconfigjson` field with your own docker config in [docker-creds.yaml](docker-creds.yaml)

4. Modify PostgreSQL credentials

Edit `host`, `user`, `password`, `database` fields in [postgresql-creds.yaml](postgresql-creds.yaml)

5. Modify deployment configuration

Set your own image url in `spec.template.spec.containers.image` in [deployment.yaml](deployment.yaml) file

6. Deploy everything

```shell
kubectl apply -f infra/kube/examples/deployments/
```
