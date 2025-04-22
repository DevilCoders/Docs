## Build and push

### Setup credentials
```
aws configure
aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 869374968268.dkr.ecr.eu-central-1.amazonaws.com
```
If you are on a Mac and want to automate login process on you Linux VM:
```
brew install findutils
aws ecr get-login-password --region eu-central-1 | gxargs -0 -I{} ssh MY_VM_HOST 'docker login --username AWS --password "{}" 869374968268.dkr.ecr.eu-central-1.amazonaws.com'
```
### Build
```
ya package drive/services/drivematics-telematics-server/package.json --docker --docker-network host --docker-registry 869374968268.dkr.ecr.eu-central-1.amazonaws.com --docker-push
```

## Minikube
- Install minikube
- Install conntrack: ```sudo apt-get install conntrack```
- Start minikube: ```minikube start --driver=none```
- Create a secret: ```kubectl create secret generic drivematics-awsecr-cred --from-file=.dockerconfigjson=/home/$USER/.docker/config.json --type=kubernetes.io/dockerconfigjson```
- Uncomment ```imagePullSecrets``` section in **deployment.yaml**

## Secrets
### ClickHouse
```
kubectl create secret generic drivematics-telematics-clickhouse-credentials --from-literal=password='MY_PASSWORD'
```

## Deploy
```
kubectl apply -f drive/services/drivematics-telematics-server/deployment.yaml
kubectl scale --replicas=<COUNT> deployment drivematics-telematics-server-deployment
```
