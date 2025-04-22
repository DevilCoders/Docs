# Routine operations automation

User story and high level design based on story for routine operations automation.

## User story

As cloud infra engineer I want:

* Automate routine operations.
* I want to approve operation, but other actions can be delegated to platform and users.

As user of multi-cloud infra platform I want:

* Request smth (cloud creation, environment bootstrap, etc) in easy way (I am ready to specify not many parameters, but
  not too much)
* Receive result of operation as soon as possible

## Let's look on some specific things

1. Operations can differ by "Execution result"

* Some operations may return "resource" as result of their execution

  Operation "Cloud creation" -> resource(Cloud)

* Other operations may return "state"

  Operation "Security audit" -> state([]Vulnerability)

2. Operations may be repeatable

   Operation "Security audit" should run periodically

3. Operations can be "Pipelined"

   "Cloud creation" operation consist of "Create cloud" and "Connect cloud to organization".
   And "Connect cloud to organization" should be executed after "Cloud creation"

4. Operations can be separated in actions

   "Bootstrap typical cloud" operation creates cloud, setup AD and SSO, setup base roles, etc. Operation "Create cloud"
   also contains cloud creation part


5. Operation with clouds may differ for different vendors

## High level design

Let's describe our platform in IaaS resources and PaaS resource.

### IaaS resource (Crossplane provider, ETC provider)

Low level resource which can rule all the fields.

* Knows how to connect to Cloud
* Knows how to perform CRUD actions
* Knows about resource lifecycle

### PaaS resource (crossplane Composition analog)

High level resource which compose IaaS resources in one simple.
You can not change all the fields.

* Compose multiple resources in one.
* Compose all clouds in one resource.
* Manage resource lifecycle during (creation/deletion/drift-reconciliation)

## Top level objects:

### CloudEnvironment

With this abstraction we're creating cloud with core environment.

Resources:

* YC: Cloud, admin-sa, VPC (IPv6), Subnet (IPv6), SecGroup
* Azure: Subscription, ResourceGroup, admin-sa, Network (IPv6), Subnet (IPv6), SecGroup, UserRoles on AD
* AWS: Account, admin-sa, VPC (IPv6), Subnet (IPv6), SecGroup, NAT, UserRoles on AD

### Kubernetes

With this abstraction we're creating kubernetes in existing core environment.

Resources:

* YC: Kubernetes, NodeGroup, kubernetes-sa, kms-key
* Azure: AKS, NodePool, ManagedIdentity
* AWS: EKS, NodePool, IAMRole, IAMPolicyAttachment

### ManagedDatabase

With this abstraction we're creating managed database in existing core environment.

Resources:

* YC: mdb PostgreSQL/MySQL/MongoDB
* Azure: PostgreSQL/MySQL/MongoDB
* AWS: rds PostgreSQL/MySQL/MongoDB

### Runtime

With this abstraction we're creating managed database in existing kubernetes cluster.

Resources:

* Common: Deployment, Service
* YC: ApplicationLoadBalancer?, DNS
* Azure: ApplicationLoadBalancer?, DNS
* AWS: ApplicationLoadBalancer?, DNS
* RTC: DeployStage, AWACS balancer, AWACS dns, many others

## Hard mode?

* Use easy mode in applicable cases. In other use hard mode.
* User can override easy mode templates?

## IaaS resources lifecycle

* Create

  PaaS resource trigger create in IaaS resource

* Update

  PaaS resource trigger update in IaaS resource

* Delete

  PaaS resource trigger delete in IaaS resource

* DriftDetection

  If IaaS resource requests drift reconciliation from PaaS resource.
  Just in case, during drift reconciliation PaaS resource can not trigger create or update.

## Resource dependencies

Describe dependencies graph in PaaS resource controller.

* Should we allow users to change behavior?
* How we'll describe graph?
    * [BehaviorTrees](https://www.researchgate.net/publication/309616544_How_Behavior_Trees_Modularize_Hybrid_Control_Systems_and_Generalize_Sequential_Behavior_Compositions_the_Subsumption_Architecture_and_Decision_Trees)
* How we'll visualize execution status? Draw execution graph and show running/failed/succeed/waiting nodes?

## Examples

```yaml
apiVersion: multi-cloud.yandex-team.ru/v1alpha1
kind: CloudEnvironment
metadata:
    name: infra-cloud
---
apiVersion: multi-cloud.yandex-team.ru/v1alpha1
kind: Kubernetes
metadata:
    name: kubernetes
spec:
    location: yc.ru-central-1
    envRef:
        name: infra-cloud
    version: "1.21"
    minCount: 1
    maxCount: 3
---
apiVersion: multi-cloud.yandex-team.ru/v1alpha1
kind: ManagedDatabase
metadata:
    name: postgresql
spec:
    location: yc.ru-central-1
    envRef:
        name: infra-cloud
    engine: postgresql
    version: "14"
---
apiVersion: runtime.yandex-team.ru/v1alpha1
kind: Runtime
metadata:
    name: application
spec:
    rtc-prod:
        cpu: 4c
        mem: 500mb
        image: cr.yandex/my-awsm-app:v1.4
        envRef:
            name: infra-rtc
        replicas: { sas: 3, vla: 3, man: 3 }
    yandex-cloud-prod:
        cpu: 4c
        mem: 500mb
        image: cr.yandex/my-awsm-app:v1.4
        envRef:
            name: infra-cloud
        replicas: { ru-central-1a: 3, ru-central-1b: 3, ru-central-1c: 3 }
    pre-stable:
        cpu: 1c
        mem: 100mb
        image: cr.yandex/my-awsm-app:v1.5
        envRef:
            name: infra-cloud
        replicas: { ru-central-1a: 1, ru-central-1b: 1, ru-central-1c: 1 }
```
