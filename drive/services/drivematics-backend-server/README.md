## Build and push
```
ya package drive/services/drivematics-backend-server/package.json --docker --docker-network host --docker-registry 869374968268.dkr.ecr.eu-central-1.amazonaws.com --docker-push
```

## Miniube
### AWS PostgreSQL secret
- Create secret
```
kubectl create secret generic drivematics-db-credentials --from-literal=endpoints='drivematics-testing-db.cpwqkdhipnyo.eu-central-1.rds.amazonaws.com' --from-literal=dbname=drivematics_testing_db --from-literal=username=carsharing --from-literal=password='PASSWORD'
```

### AWS PostgreSQL access
- Apply docker network settings from ```https://docs.yandex-team.ru/qyp/faq```
- Edit CoreDNS config ```kubectl -n kube-system edit configmap coredns```
- Add section ```amazonaws.com:53```:
```
...
data:
  Corefile: |
    .:53 {
        ...
        forward . /etc/resolv.conf {
           max_concurrent 1000
        }
        ...
    }
    amazonaws.com:53 {
        errors
        cache 30
        forward . 2a02:6b8:0:3400::5005
        reload
    }
...
```

### AWS access
- Create secret
```
kubectl create secret generic drivematics-aws-credentials --from-literal=key_id=VALUE --from-literal=secret_key=VALUE
```
