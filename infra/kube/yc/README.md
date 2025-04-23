# Yandex.Cloud

**Status**: work in progress.

This part about managing cloud resources via Crossplane. With crossplane you can manage cloud resources and deploy
applications with single CLI tool - kubectl.

**For now, we can work with:**

* VPC Network
* VPC Subnet
* Kubernetes Cluster
* Kubernetes NodeGroup
* VirtualMachine
* MDB PostgreSQL
* MDB Redis
* MDB MongoDB
* ObjectStorage Bucket
* ObjectStorage Object
* ContainerRegistry
* DNS
* ServiceAccount
* ServiceAccount roles
* KMS
* Folder

**You:** requests cloud creation.
**We:** creating cloud and provide access to our crossplane cluster connected with your cloud.

Request cloud with crossplane environment via [form](https://st.yandex-team.ru/createTicket?queue=KUBERTC&_form=82765)

## Further read

* [Getting started guide](docs/getting-started.md)
* [Example guides how to provision common resources.](examples)
