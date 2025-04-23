## Build

```
ya package drive/services/drivematics-proxy/package.json --docker --docker-network host --docker-registry 869374968268.dkr.ecr.eu-central-1.amazonaws.com --docker-push
```

## Debug

```
kubectl exec -it -n drivematics-proxy drivematics-proxy-deployment-56874f8744-rfpj4 -- /bin/bash
kubectl --context drivematics-production -n drivematics-proxy logs deployment/drivematics-proxy-deployment
```
