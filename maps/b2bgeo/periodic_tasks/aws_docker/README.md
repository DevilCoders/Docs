# B2bGeo Periodic Tasks @ AWS

Service to perform periodic tasks by cron, deployed in AWS with Kubernetes.

## Infrastructure

Service deployment:
```sh
$ kubectl get deployments/periodic -n stable -o json
```
Service pods:
```sh
$ kubectl get pods -n stable -l app.kubernetes.io/name=periodic
```
Connect to pod and inspect logs:
```sh
$ kubectl exec -it <pod> -n stable -- /bin/bash
$ tail -100 /var/log/yandex/maps/b2bgeo/monitoring_aws.log
$ tail -100 /var/log/yandex/maps/b2bgeo/uptime_aws.log
```

## Deploy

How to build and update new image (tag is taken from the current Arc revision):
```sh
AWS_PREFIX=582601430203.dkr.ecr.us-east-2.amazonaws.com
REVISION=`arc describe --svnrevision | grep "Last Changed Rev:" | awk -v FS=': ' '{print $2}'`

aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin ${AWS_PREFIX}

ya package --custom-version=${REVISION} pkg.json

IMAGE=${AWS_PREFIX}/periodic:${REVISION}
docker build --network host -t ${AWS_PREFIX}/periodic:$REVISION - < b2bgeo-periodic-tasks.${REVISION}.tar.gz
docker push ${IMAGE}

kubectl set image -n stable deployments/periodic periodic=${IMAGE}
```
