# Provider jet YC

[Repo](http://github.com/yandex-cloud/provider-jet-yc)

## Operations

### Update terraform provider version

* Set new version

    * in [Makefile](https://github.com/yandex-cloud/provider-jet-yc/blob/main/Makefile#L9)
    * in [go.mod](https://github.com/yandex-cloud/provider-jet-yc/blob/main/go.mod#L12)

* Regenerate provider

    ```shell
    go mod vendor && make generate
    ```

### Build and push new images

* Update tag

    * in [package/crossplane.yaml](https://github.com/yandex-cloud/provider-jet-yc/blob/main/package/crossplane.yaml#L7)
    * in [README.md](https://github.com/yandex-cloud/provider-jet-yc/blob/main/README.md?plain=1#L40)

* Build images

   ```shell
   make
   ```

* In output find sha256 of new images. Then tag and push images in registry.

   ```shell
   CONTROLLER_HASH=''
   PROVIDER_HASH=''
   TAG_VERSION=v0.1.14
   docker image tag sha256:$PROVIDER_HASH cr.yandex/crp0kch415f0lke009ft/crossplane/provider-jet-yc:$TAG_VERSION
   docker image tag sha256:$CONTROLLER_HASH cr.yandex/crp0kch415f0lke009ft/crossplane/provider-jet-yc-controller:$TAG_VERSION

   docker image push cr.yandex/crp0kch415f0lke009ft/crossplane/provider-jet-yc-controller:$TAG_VERSION
   docker image push cr.yandex/crp0kch415f0lke009ft/crossplane/provider-jet-yc:$TAG_VERSION
   ```

### Deploy provider from private registry

**For now crossplane does not support installing providers from private registry.**

To deploy provider we need:

* Deploy provider controller

```shell
kubectl apply -f infra/kube/yc/internal/deployment
```

* Apply CRDs from provider-jet-yc repo

```shell
kubectl apply -f package/crds
```
