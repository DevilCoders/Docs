## Setup EKS cluster

### Initial setup
```
eksctl create cluster -f drive/services/drivematics-eks/(testing|production).yaml
```

### Install dashboard
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.1/aio/deploy/recommended.yaml
```
The most up-to-date information is available at https://github.com/kubernetes/dashboard

### Install crossplace
```
kubectl create namespace crossplane-system

helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update

helm install crossplane --namespace crossplane-system crossplane-stable/crossplane

curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh
# you may need to replace your kubectl after that

kubectl crossplane install configuration registry.upbound.io/xp/getting-started-with-aws:v1.7.0
```
The most up-to-date information is available at https://crossplane.io/docs/v1.7/getting-started/install-configure.html

### Install AWS Load Balancer controller
```
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.1/docs/install/iam_policy.json &&
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json

eksctl create iamserviceaccount \
--cluster=drivematics-(testing|production) \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--role-name "AmazonEKSLoadBalancerControllerRole" \
--attach-policy-arn=arn:aws:iam::<AWS_account_id>:policy/AWSLoadBalancerControllerIAMPolicy \
--approve

helm repo add eks https://aws.github.io/eks-charts
helm repo update
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=drivematics-(testing|production) --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller --set region=eu-central-1 --set vpcId=vpc-<Id>
```

### Add access to cluster
```
eksctl create iamidentitymapping     --cluster drivematics-(testing|production)     --region=eu-central-1     --arn arn:aws:iam::869374968268:user/<USERNAME>     --group system:masters
```

### Add cluster to your kubeconfig
```
aws eks update-kubeconfig --region eu-central-1 --name drivematics-(testing|production) --alias drivematics-(testing|production)
```
