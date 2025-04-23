This helm chart configures prerequisites for AWS ALB add-on.

If you want to install [AWS ALB add-on](https://github.com/aws/eks-charts/tree/master/stable/aws-load-balancer-controller) run this chart before.

----

OIDC ID will be available after EKS cluster is created, and it is a part of OIDC URL.

OIDC URL:
```
https://oidc.eks.eu-north-1.amazonaws.com/id/EXAMPLED539D4633E53DE1B71EXAMPLE
```

OIDC ID:
```
EXAMPLED539D4633E53DE1B71EXAMPLE
```

For example, to get OIDC ID you can run
```
kubectl get clusters.eks -n <namespace> <clustername > \
  -o jsonpath="{.status.atProvider.identity[0].oidc[0].issuer}"| awk -F'/' '{print $NF}';echo
```

----

**After you installed this chart, you must switch your kubernetes context to your new cluster, where ALB should be installed.**

Then you must create service account for ALB.

Save below manifest to `alb.serviceacc.yaml`, replacing `111122223333` with your account ID,
and `AmazonEKSLoadBalancerControllerRole` with `eks-alb-role-<projectName>-<projectSuffix>`.

`projectName` and `projectSuffix` you set in values.yaml


```
apiVersion: v1
kind: ServiceAccount
metadata:
  labels:
    app.kubernetes.io/component: controller
    app.kubernetes.io/name: aws-load-balancer-controller
  name: aws-load-balancer-controller
  namespace: kube-system
  annotations:
    eks.amazonaws.com/role-arn: arn:aws:iam::111122223333:role/AmazonEKSLoadBalancerControllerRole
```

Then run `kubectl apply -f alb.serviceacc.yaml`.

After this, you can install AWS ALB with:

```
helm repo add eks https://aws.github.io/eks-charts
helm install aws-load-balancer-controller eks/aws-load-balancer-controller --set clusterName=<your_cluster_name> -n kube-system --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller
```
