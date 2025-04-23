This helm chart will create OIDC provider.

If you want to run AWS ALB in your cluster, you must install this chart.

Run this chart after `eks` chart, because you will need some values from the result of `eks` chart.

----

OpenID Connect provider URL will be available after EKS cluster is created.
For example, to get OIDC URL you can run
```
kubectl get clusters.eks -n <namespace> <clustername > \
  -o jsonpath="{.status.atProvider.identity[0].oidc[0].issuer}";echo
```

You can also find this URL in AWS Console, in cluster overview: 

It should look like this:

```
https://oidc.eks.eu-north-1.amazonaws.com/id/EXAMPLED539D4633E53DE1B71EXAMPLE
```

----

To get thumbprint of `oidc.eks.<your_eks_cluster_region>.amazonaws.com`,
you should run `./oidc_thumbprint.sh <your_eks_cluster_region>`

This script is based on scripts from this issue
https://github.com/terraform-providers/terraform-provider-aws/issues/10104

Example: 

```
$ ./oidc_thumbprint.sh eu-north-1
9e99a48a9960b14926bb7f3b02e22da2b0ab7280

```
