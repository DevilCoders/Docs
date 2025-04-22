## Set up federation YC profiles.
Follow [yc setup manual](https://wiki.yandex-team.ru/cloud/support/tools/#yandex.cloudcliyc) to install `yc` and create two essential profiles named `prod-fed-user` and `preprod-fed-user`:
```shell
$ yc config profile list
preprod-fed-user
prod-fed-user ACTIVE
```


## Set up Wall-e service account YC profiles.
Use [../tools/yc-profile-creator](../tools/yc-profile-creator) script to create two service account's profiles named `prod-yc.wall-e.main-sa` and `preprod-yc.wall-e.main-sa`:
```shell
$ ../tools/yc-profile-creator/create-walle-main-sa-yc-profile -s prod
...
$ ../tools/yc-profile-creator/create-walle-main-sa-yc-profile -s preprod
...
$ ../tools/yc-profile-creator/create-walle-main-sa-yc-profile -s testing
...
$ yc config profile list
preprod-fed-user
preprod-yc.wall-e.main-sa
preprod-yc.wall-e.main-sa-testing ACTIVE
prod-fed-user
prod-yc.wall-e.main-sa
```


## Set up kubectl.
1. Make a backup of current kunectl configuration:
    ```shell
    $ mv ~/.kube/ ~/.kube_bak_$(date +%s)/
    ```
2. Create kubectl contexts:
    ```shell
    # Prod.
    yc config profile activate prod-yc.wall-e.main-sa
    yc managed-kubernetes cluster get-credentials --id catsrpd756apschlkafe --internal
    kubectl config rename-context yc-walle-mk8s-cluster walle-prod
    kubectl config set-context walle-prod --namespace=default
    kubectl config unset clusters.yc-managed-k8s-catsrpd756apschlkafe.certificate-authority-data
    kubectl config set clusters.yc-managed-k8s-catsrpd756apschlkafe.server https://walle-mk8s-cluster-kube-socat.wall-e.cloud.yandex.net
    kubectl config set clusters.yc-managed-k8s-catsrpd756apschlkafe.insecure-skip-tls-verify true

    # Preprod.
    yc config profile activate preprod-yc.wall-e.main-sa
    yc managed-kubernetes cluster get-credentials --id c490rrkpj0bbr1kmjg0s --internal
    kubectl config rename-context yc-walle-mk8s-preprod-testing-cluster walle-preprod
    kubectl config set-context walle-preprod --namespace=preprod
    kubectl config unset clusters.yc-managed-k8s-c490rrkpj0bbr1kmjg0s.certificate-authority-data
    kubectl config set clusters.yc-managed-k8s-c490rrkpj0bbr1kmjg0s.server https://walle-mk8s-cluster-kube-socat.wall-e.cloud-preprod.yandex.net
    kubectl config set clusters.yc-managed-k8s-c490rrkpj0bbr1kmjg0s.insecure-skip-tls-verify true

    # Testing.
    yc config profile activate preprod-yc.wall-e.main-sa-testing
    yc managed-kubernetes cluster get-credentials --id c49pnb4h4on3n1076le2 --internal
    kubectl config rename-context yc-walle-mk8s-testing-cluster walle-testing
    kubectl config set-context walle-testing --namespace=testing
    kubectl config unset clusters.yc-managed-k8s-c49pnb4h4on3n1076le2.certificate-authority-data
    kubectl config set clusters.yc-managed-k8s-c49pnb4h4on3n1076le2.server https://walle-mk8s-cluster-kube-socat.wall-e-testing.cloud-preprod.yandex.net
    kubectl config set clusters.yc-managed-k8s-c49pnb4h4on3n1076le2.insecure-skip-tls-verify true
    ```


4. These commands will result in three kubectl contexts:
    ```
    $ kubectl config get-contexts
    CURRENT   NAME            CLUSTER                               AUTHINFO                              NAMESPACE
              walle-preprod   yc-managed-k8s-c490rrkpj0bbr1kmjg0s   yc-managed-k8s-c490rrkpj0bbr1kmjg0s   preprod
              walle-prod      yc-managed-k8s-catsrpd756apschlkafe   yc-managed-k8s-catsrpd756apschlkafe   default
    *         walle-testing   yc-managed-k8s-c49pnb4h4on3n1076le2   yc-managed-k8s-c49pnb4h4on3n1076le2   testing
    ```


## `build-and-upload-walle-docker-images` script
Script automates building Wall-e Docker images and uploading them to stage's container registry.
Usage:
```shell
$ build-and-upload-walle-docker-images \
  -s [prod | preprod | testing] \
  -i [walled-python | walled-go | walle-shell | webapp] \
  -t some-docker-image-tag
```

NB: Building `webapp` requires access to `cr.yandex/cloud-ui/node-nginx` repository.


## Deploy to production.
1. Build and upload Docker image to registry, using either [Assembly Workshop](https://teamcity.aw.cloud.yandex.net/project/Walle) ([manual](https://wiki.yandex-team.ru/users/squirrel/notes/migration-to-yc/walle-cloud-infra/#assembly-workshop-builds-run)), or [build-and-upload-walle-docker-images](./build-and-upload-walle-docker-images) script with `-s prod` flag.
2. Edit `images` section in [overlays/yc-prod/kustomization.yaml](./overlays/yc-prod/kustomization.yaml): set desired image's `newTag` value to your Docker image's tag.
3. Run `kubectl config use-context walle-prod && kubectl apply -k overlays/yc-prod/` to apply changes.
4. Debug changes applied with
   ```shell
   kubectl get deployments
   kubectl describe deployment DEPLOYMENT

   kubectl get pods
   kubectl get pods -o jsonpath="{.items[*].spec.containers[*].image}" |tr -s '[[:space:]]' '\n' |sort |uniq -c
   kubectl logs POD_ID
   kubectl exec --stdin --tty POD_ID -- /bin/bash
   ```
5. Commit changes to Arcadia.


## Debug kustomize
See generated specs:
```
kubectl kustomize overlays/prod
```

Apply specific kustomized specs:
```
mkdir outputdir
kubectl kustomize overlays/prod -o outputdir
kubectl apply -f outputdir/<xxxx>.yaml
```
