# Network

In this example we'll provision core networks in AWS. Virtual network with private subnets for infra resources and
public subnets for external traffic. Setup other networking infra like SecurityGroups, InternetGateway, RouteTable.

## Networking schema

// TODO: visualisation of network

// TODO: where you need to place resources Kubernetes, RDS, VM, ALB, etc

## Prerequisites

* Set up kubernetes environment with crossplane

You have already done it if you have complete [getting-started.md](../../docs/getting-started.md)

## Provision

* Create VPC

kubectl --context crossplane apply -f infra/kube/aws/examples/net/vpc.yaml

* Change hardcoded IPv6 prefixes in [public-subnets.yaml](public-subnets.yaml)

  * Check VPC ipv6 range
    ```
    kubectl --context crossplane get -f infra/kube/aws/examples/net/vpc.yaml -o json | jq -r .spec.forProvider.ipv6CidrBlock
    2a05:d016:f1:2e00::/56
    ```
  * Set ipv6 for Subnets from VPC range

    In my case: subnet-a - `2a05:d016:f1:2e01::/64`, subnet-b - `2a05:d016:f1:2e02::/64`, subnet-c - `2a05:d016:f1:2e02::/64`

* Create resources

```shell
kubectl --context crossplane apply -f infra/kube/aws/examples/net
```

* Watch resources status

```shell
watch kubectl --context crossplane get -f infra/kube/aws/examples/net
```
