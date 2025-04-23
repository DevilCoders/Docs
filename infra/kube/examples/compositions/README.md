# Install crossplane configurations in yandex cloud k8s

## Write Compositions

Tree of dir with composition definitions files

```
~ tree
├── README.md
├── configuration
│   ├── aks
│   │   ├── composition.yaml
│   │   ├── crossplane.yaml
│   │   └── definition.yaml
│   ├── app
│   │   ├── composition.yaml
│   │   ├── crossplane.yaml
│   │   └── definition.yaml
│   ├── aso
│   │   ├── cert-manager
│   │   │   ├── composition.yaml
│   │   │   └── definition.yaml
│   │   ├── crossplane.yaml
│   │   └── release
│   │       ├── composition.yaml
│   │       └── definition.yaml
│   ├── crossplane
│   │   ├── crossplane
│   │   │   ├── composition.yaml
│   │   │   └── definition.yaml
│   │   ├── crossplane.yaml
│   │   └── provider-azure
│   │       ├── composition.yaml
│   │       └── definition.yaml
│   ├── crossplane-cluster
│   │   ├── composition.yaml
│   │   ├── crossplane.yaml
│   │   └── definition.yaml
│   ├── crossplane.yaml
│   ├── pg
│   │   ├── composition.yaml
│   │   ├── crossplane.yaml
│   │   └── definition.yaml
│   └── providers.yaml
└── example
    ├── aks.yaml
    ├── app.yaml
    ├── aso.yaml
    ├── crossplane-cluster.yaml
    ├── crossplane.yaml
    └── pg.yaml
```
For each crossplane Configuration you should create dir with crossplane.yaml and compositions dirs:

For Composition resource you should create nested dir with:

* composition.yaml

```
apiversion:apiextensions.crossplane.io/v1
kind:Composition
```

* definition.yaml

```
apiversion:apiextensions.crossplane.io/v1
kind:CompositeResourceDefinition
```

## Build/Push compositions in configuration

Execute following commands in `./configuration/<package-name>` dir:

```
kubectl crossplane build configuration --name yandex.infra
```

This command creates .xpkg file with configuration.

Now push configuration in your registry:

```
kubectl crossplane push configuration cr.yandex/crpq165pjbjiprv8pfri/crossplane/configuration/<package-name>:v0.1
```

## Apply configuration in cluster

Configurations definitions stored in configuration/ dir

**!! When writing new configuration!!**

* Do not forget set following lines in spec section.

  ```yaml
  packagePullSecrets:
    - name: docker-creds
  ```
* Create docker secret in k8s cluster

  For yandex cloud: use external-registry-puller service account.
    * Create iam key. Or get existing from
      yav [secret](https://yav.yandex-team.ru/secret/sec-01f9gr5p5ngkhn3xcqtfjezx56/explore/versions) yc-docker-puller
      ```
      yc iam key create --service-account-name external-registry-puller -o key.json
      ```
    * Configure docker for this sa
      ```
      cat key.json | docker login --username json_key --password-stdin cr.yandex
      ```
    * Create k8s secret from ~/.docker/config.json in namespace crossplane-system with name docker-creds
      ```
      kubectl create secret generic docker-creds -n crossplane-system  \
        --from-file=.dockerconfigjson=~/.docker/config.json \
        --type=kubernetes.io/dockerconfigjson
      ```

Apply all configurations:

```
kubectl apply -f configuration
```

## Now you can test examples

Examples compositions stored in example
