# Managing cluster

## Creating cluster

First, create clusters. This process can take from 10 to 30 minutes.

```
eksctl create cluster -f aws-eks-cluster.yaml
eksctl create cluster -f aws-eks-cluster-testing.yaml
```

Then create namespaces if needed:
```
kubectl apply -f stable-namespace.yaml
```

## Update nodegroup
By design, nodegroups are immutable. This means that if you need to change something (other than scaling) like the AMI or the instance type of a nodegroup, you would need to create a new nodegroup with the desired changes, move the load and delete the old one. ([ref](https://eksctl.io/usage/managing-nodegroups/#nodegroup-immutability))

So, you update nodegroup configuration (`managedNodeGroups` section in ClusterConfig; you need to make a new name for updated nodegroup) and run the command below.

```
eksctl create nodegroup -f aws-eks-cluster-testing.yaml
```

Then run `eksctl delete nodegroup` with `--only-missing` flag to delete all node groups which are not presented in the config.
```
eksctl delete nodegroup -f aws-eks-cluster-testing.yaml --only-missing --approve
```

Note: nodegroup is not deleted right after the command completed. It needs about 5 minutes for nodegroup to be actually deleted (at least once I noticed this behavior).

## Switch cluster for kubectl

To switch kubectl config between stable and testing use:
- `aws eks update-kubeconfig --name default` - for stable
- `aws eks update-kubeconfig --name testing` - for testing

## Configuring policy for AWS Load Balancer Controller

Amazon's original user guide is here: https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html

TL;DR: Just run next commands replacing `cluster`, `name` and `role-name` values for aws-load-balancer-controller to work.

```bash
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.4.1/docs/install/iam_policy.json
aws iam create-policy --policy-name TestingAWSLoadBalancerControllerIAMPolicy --policy-document file://iam_policy.json
eksctl create iamserviceaccount \
  --cluster=testing \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name "TestingAmazonEKSLoadBalancerControllerRole" \
  --attach-policy-arn=arn:aws:iam::582601430203:policy/TestingAWSLoadBalancerControllerIAMPolicy \
  --approve
helm repo add eks https://aws.github.io/eks-charts
helm repo update
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=testing \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller
kubectl get deployment -n kube-system aws-load-balancer-controller
```

## Mapped docker images

Relative paths are saved in 582601430203.dkr.ecr.us-east-2.amazonaws.com

- quay.io/mongodb/mongodb-agent:11.12.0.7388-1
- quay.io/mongodb/mongodb-kubernetes-operator-version-upgrade-post-start-hook:1.0.4
- quay.io/mongodb/mongodb-kubernetes-readinessprobe:1.0.9
- quay.io/mongodb/mongodb-kubernetes-operator:0.7.4
- docker.io/mongo:4.2.20
- 602401143452.dkr.ecr.us-west-2.amazonaws.com/amazon/aws-load-balancer-controller:v2.4.2
- k8s.gcr.io/csi-secrets-store/driver:v1.2.2
- k8s.gcr.io/csi-secrets-store/driver-crds:v1.2.2
- k8s.gcr.io/sig-storage/csi-node-driver-registrar:v2.5.1
- k8s.gcr.io/sig-storage/livenessprobe:v2.7.0
- public.ecr.aws/aws-secrets-manager/secrets-store-csi-driver-provider-aws:1.0.r2-6-gee95299-2022.04.14.21.07
- quay.io/prometheus/alertmanager:v0.24.0
- quay.io/prometheus/blackbox-exporter:v0.20.0
- quay.io/brancz/kube-rbac-proxy:v0.12.0
- jimmidyson/configmap-reload:v0.5.0
- grafana/grafana:8.5.0
- k8s.gcr.io/kube-state-metrics/kube-state-metrics:v2.4.2
- quay.io/prometheus/node-exporter:v1.3.1
- quay.io/prometheus/prometheus:v2.35.0
- k8s.gcr.io/prometheus-adapter/prometheus-adapter:v0.9.1
- quay.io/prometheus-operator/prometheus-operator:v0.56.0
- quay.io/prometheus-operator/prometheus-config-reloader:v0.56.0

## Helms

Repositories:
- eks: https://aws.github.io/eks-charts
- mongodb: https://mongodb.github.io/helm-charts
- secrets-store-csi-driver: https://kubernetes-sigs.github.io/secrets-store-csi-driver/charts

Go to helm_values/testing or helm_values/stable directory, then:

- For helms installation:
```
helm install -f mongo.yaml community-operator mongodb/community-operator
helm install -f aws-load-balancer-controller.yaml aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system
helm install -f csi-secrets-store.yaml csi-secrets-store secrets-store-csi-driver/secrets-store-csi-driver -n kube-system
```

- For helms update:
```
helm upgrade -f mongo.yaml community-operator mongodb/community-operator
helm upgrade -f aws-load-balancer-controller.yaml aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system
helm upgrade -f csi-secrets-store.yaml csi-secrets-store secrets-store-csi-driver/secrets-store-csi-driver -n kube-system
```

## External manifests

Run ```kubectl apply -f <manifest.yaml>``` with manifests in external_manifests
