# Nested crossplane

Examples of resources creation in nested crossplane cluster

On this step we already have provisioned Crossplane Cluster:

* K8S cluster in cloud e.g. Azure AKS
* Crossplane helm release installed on cluster
* Azure service operator helm release installed on cluster

Now we need:

* Configure crossplane providers if needed.
* Apply needed crossplane configurations with compositions.
* Then you can create resources.
