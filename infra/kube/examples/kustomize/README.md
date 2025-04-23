# Kustomize example deployment staging

## Specs

Simulating staging with kustomize.

* Kustomizing nginx config in nginx-conf.yaml simulating version change
* Kustomizing nodes count in deployment.yaml simulating production resources
* Patching namespace nginx-prod/nginx-test in kustomization.yaml to separate resources

## Apply

```shell
#
# Execute from examples/kustomize dir
#

# for test configuration
kubectl apply -k overlays/test

# for prod configuration
kubectl apply -k overlays/prod
```

## Getting resources statuses

```
❯ kubectl get -k overlays/prod
NAME                        DATA   AGE
configmap/nginx-configmap   2      2m38s

NAME                    TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
service/nginx-service   LoadBalancer   10.2.142.31   84.201.129.68   80:31006/TCP   2m38s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-deployment   3/3     3            3           2m38s


❯ kubectl get -k overlays/test
NAME                        DATA   AGE
configmap/nginx-configmap   2      29m

NAME                    TYPE           CLUSTER-IP    EXTERNAL-IP       PORT(S)        AGE
service/nginx-service   LoadBalancer   10.2.239.72   178.154.205.166   80:32563/TCP   29m

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx-deployment   1/1     1            1           20m
```
