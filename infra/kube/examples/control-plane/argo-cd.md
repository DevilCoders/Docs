# ArgoCD installation

## Provision ArgoCD on existing control-plane k8s

1. Switch kubectl context on control-plane cluster

2. Deploy ArgoCD following [instructions](https://argo-cd.readthedocs.io/en/stable/getting_started/)

## Integrate with git

Follow [instructions](https://argo-cd.readthedocs.io/en/release-1.8/user-guide/private-repositories/).

## Create infra projects

```shell
k create namespace prod-infra
k create namespace pre-infra

argocd app create prod-infra --repo http://13.49.246.236/vaspahomov/examples.git --path prod-infra --dest-server https://kubernetes.default.svc --dest-namespace prod-infra
argocd app create pre-infra --repo http://13.49.246.236/vaspahomov/examples.git --path pre-infra --dest-server https://kubernetes.default.svc --dest-namespace pre-infra
```
