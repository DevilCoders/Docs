## Crossplane

Crossplane allows to manage clouds/subscriptions/AWS accounts and their resources with unified
approach:

1. select required resource template (yaml file) (VM, Postres, k8s, ObjectStorage and so on)
2. mmodify its content in correspondence with its necessary data (for example, required
   CPU and memory for VM)
3. start resource creation by command `kubectl apply` with specified resource file
   (kubectl is a standard utility for k8s cluster management)
4. check that resource was created successfully (command `kubectl get` or `kubectl describe`)

Crossplane can manage clouds of different vendors (Yandex.Cloud, AWS, Azure, GCP and so on),
create resources and get resource statuses. Resource template file are different for different
vendors but it's easy to get description of any attribute in resource yaml file
using `kubectl explain`. Moreover, resource files has documentation.

Crossplane can manage resources created externally, ie not using Crossplane.
For that purpose it is necessary to describe existing resources
using resource templates. After `kubectl apply` the resource becomes manageable by Crossplane.

In the future the majority of processes related to clouds (cloud creation, service account creation,
role management for users and service accounts and so on) will be executed by Crossplane.

Detailed information by [link](https://a.yandex-team.ru/arc/trunk/arcadia/infra/kube)
