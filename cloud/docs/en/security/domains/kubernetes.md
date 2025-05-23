# Kubernetes security

The section includes recommendations for {{ yandex-cloud }} users on security settings in [{{ managed-k8s-full-name }}](../../managed-kubernetes/index.yaml).

## Responsibility {#division-of-responsibility}

The user is responsible for all actions made inside the Kubernetes node. The user is responsible for the security of the nodes and their proper setup in accordance with {% if product == "yandex-cloud" %}PCI DSS requirements and other {% endif %}security standards.

{{ yandex-cloud }} is responsible for the the Kubernetes API security.

The user is responsible for correctly choosing security settings in {{ managed-k8s-short-name }}, including selecting the [channel](../../managed-kubernetes/concepts/release-channels-and-updates.md) and the update schedule.

## Sensitive data {#critical-data}

When using {{ managed-k8s-short-name }} to comply with {% if product == "yandex-cloud" %}PCI DSS or other {% endif %}security standards, it is forbidden to: 

* Use sensitive data in names and descriptions of clusters, node groups, namespaces, services, and pods.
* Use sensitive data in [Kubernetes node labels](../../managed-kubernetes/concepts/#node-labels) and [{{ yandex-cloud }} service resource labels](../../overview/concepts/services.md#labels).
* Use sensitive data in pod manifests.
* Use sensitive data in etcd in clear text.
* Write sensitive data to {{ managed-k8s-short-name }} logs.

## Resource model {#resource-model}

Wherever possible, ensure maximum isolation between resources:

* Use a separate organization for each "large-scale" project. 
* Use a separate cloud for each development team.
* Use a separate Kubernetes cluster located in a separate folder for each service.
* Use a separate namespace for each microservice.

Your clouds must have no shared resources. Cloud members must have access only to their clouds.

Less strong isolation models are also possible, for example:

* Projects are split between different clouds.
* Development teams are assigned independent folders.
* Services have separate Kubernetes clusters.
* Microservices have independent namespaces.

## Network security {{ managed-k8s-short-name }} {#network-security}

We don't recommend that you grant access to the Kubernetes API and node groups from non-trusted networks (for example, from the internet).
Use firewall protection when needed (for example, [security groups](../../vpc/concepts/security-groups.md)). In the section below, you can find links to instructions on how to set up firewall protection in security groups.

### Segmentation {#segmentation}

#### Cloud level {#cloud-level}

Restrict network access to the Kubernetes API (master) and node groups using [instructions for security groups](../../managed-kubernetes/operations/security-groups.md).

When using an ALB as an [Ingress Gateway](../../managed-kubernetes/tutorials/alb-ingress-controller.md), also complete the following steps:

1. Apply the security group to the ALB.
2. Additionally, apply the security group to the node group:

   * Source type: `<security group applied to the ALB>`.
   * Destination type: `node group`.
   * Port range: 30000-32767.

#### Kubernetes level {#kubernetes-level}

Restrict network access inside Kubernetes using the [Network Policy](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

You can use two network plugins in {{ yandex-cloud }}:

* [Calico](../../managed-kubernetes/concepts/network-policy.md#calico): A basic plugin.
* [Cilium CNI](../../managed-kubernetes/concepts/network-policy.md#cilium): An advanced plugin that uses advanced network policies applied at the [L7 layer (REST/HTTP, gRPC and Kafka)](https://docs.cilium.io/en/v1.10/gettingstarted/http/).

We recommend that you use the `default deny` rule for the default incoming and outgoing traffic, allowing only relevant traffic.

To generate policies, you can use the Cilium CNI built-in Hubble platform to analyze the traffic manually. Various solutions for automatic generation of network policies are also available on the market.

{% if product == "yandex-cloud" %}
![](../../_assets/overview/solution-library-icon.svg)[Kubernetes security solutions comparison matrix.](https://github.com/yandex-cloud/yc-solution-library-for-security/blob/master/kubernetes-security/choice_of_solutions/Сравнение_функций_k8s_security.pdf)

{% endif %}
For useful examples of network policies, see the [repo](https://github.com/ahmetb/kubernetes-network-policy-recipes). 

A helpful tool to create both basic and advanced network policies is available [here](https://editor.cilium.io/).

#### Setting up incoming network access {#ingress}

For online endpoints, we recommend that you allocate an independent Kubernetes cluster or independent node groups (using [Taints and Tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#:~:text=Node%20affinity%20is%20a%20property,onto%20nodes%20with%20matching%20taints) + [Node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) mechanisms). By doing this, you establish a DMZ so that if your nodes are compromised online, your attack surface is small.

To enable incoming network access to your workloads via HTTP/HTTPS, use the [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) resource.

There exist at least two variants of an Ingress controller that you can use in {{ yandex-cloud }}:
- [NGINX Ingress Controller](../../managed-kubernetes/tutorials/ingress-cert-manager.md).
- [{{ alb-name }} Ingress controller](../../managed-kubernetes/tutorials/alb-ingress-controller.md).

Benefits of {{ alb-name }} Ingress controller:
* Integration with the [{{ certificate-manager-full-name }}](../../certificate-manager/) cloud service.
* No need to install a controller to the cluster because everything is deployed on the [{{ alb-name }}](../../application-load-balancer/) side).

#### Restricting access to the metadata of VMs in the node group {#metadata-access-restriction}

For all pods, create a network policy to block network traffic to port 169.254.169.254 or use the default-deny policy from the [example](../../managed-kubernetes/operations/calico#enable-isolation). The policy must block workload node group metadata access because these node groups contain sensitive data, such as the token of the service account assigned to the node.

## Authentication and access control {{ managed-k8s-short-name }} {#authentication-and-access-control}

The access of {{ iam-short-name }} accounts to {{ managed-k8s-short-name }} resources is managed at the following levels:

* [{{ managed-k8s-short-name }} service roles](../../managed-kubernetes/security/#yc-api) (access to the {{ yandex-cloud }} API): They enable you to control clusters and node groups (for example, create a cluster, create/edit/delete a node group, and so on).
* Service roles to access the Kubernetes API: They let you control cluster resources via the Kubernetes API (for example, perform standard actions with Kubernetes: create, delete, view namespaces, work with pods, deployments, creating roles, and so on). Only the basic global roles at the cluster level are available: `k8s.cluster-api.cluster-admin`, `k8s.cluster-api.editor`, and `k8s.cluster-api.viewer`.
* Primitive roles: These are global primitive {{ iam-short-name }} roles that include service roles (for example, the primitive role admin includes both the service administration role and the administrative role to access the Kubernetes API).
* Standard Kubernetes roles: Inside the Kubernetes cluster, you can use Kubernetes tools to create both regular roles and cluster roles. This way, you can control {{ iam-short-name }} accounts access at the namespace level. To assign {{ iam-short-name }} roles at the namespace level, you can manually create RoleBinding objects in a relevant namespace, specifying the {{ iam-short-name }} ID of the cloud user in the "subjects name" field. Example:

   ```
   apiVersion: rbac.authorization.k8s.io/v1
   kind: RoleBinding
   metadata:
   name: iam-user-aje0jndkhkvu04ek #name of the RoleBinding object
   namespace: micro1-ns 
   roleRef:
   apiGroup: rbac.authorization.k8s.io
   kind: ClusterRole
   name: admin
   subjects:
   - kind: User
   name: aje0jndkq855llvu04ek #cloud user ID
   ```

For the {{ managed-k8s-short-name }} cluster to run, you need two service accounts: [the service account of the cluster and the service account of the node group](../../managed-kubernetes/security/index.md#sa-annotation).

{% if product == "yandex-cloud" %}
![](../../_assets/overview/solution-library-icon.svg)[Example of setting up role models and policies in {{ managed-k8s-short-name }}.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/kubernetes-security/auth_and_access/role-model-example)

{% endif %}
## Secure {{ managed-k8s-short-name }} configuration {#secure-config-1}

### Secure configuration {#secure-config-2}

In {{ managed-k8s-short-name }}, the user is fully in control of all node group settings, but only partially in control of the [master](../../managed-kubernetes/concepts/index.md#master) settings. These settings are part of the user's overall cluster security responsibility.

The [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes) standard is designed to build a secure Kubernetes configuration, including node configurations.

In {{ yandex-cloud }}, the Kubernetes node groups are deployed by default with the configuration that complies with the CIS Kubernetes Benchmark.

The [kube-bench](https://github.com/aquasecurity/kube-bench) tool enables you to check whether the node group configuration is compliant with CIS Kubernetes Benchmark. The tool officially supports the {{ yandex-cloud }} node groups.

[Here](https://github.com/aquasecurity/kube-bench/blob/main/docs/running.md) you can see the examples of launching kube-bench on the nodes.

In addition, kube-bench supports integration with [Starboard Operator](https://blog.aquasec.com/automate-kubernetes-compliance) — another product for kube-bench automatic launching.

Starboard Operator is a free tool that helps you automate scanning of images for vulnerabilities and checking that the configuration complies with CIS Kubernetes Benchmark.

{% if product == "yandex-cloud" %}
![](../../_assets/overview/solution-library-icon.svg) [Integration between Starboard and {{ container-registry-full-name }} to scan running images](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/kubernetes-security/starboard_and_yc-cr)

{% endif %}
### Integrity control (FIM — File integrity monitoring) {#fim}

You must control two levels of file integrity in node groups:

* OS files of the node - for example, configuration files. 
* Container files - for example, critical files that the user application writes to the [volume](../../managed-kubernetes/concepts/volume.md).

#### OS files of the node {#fim-OS-files}

You can use, for example, [Osquery](https://osquery.io/) as an agent installed on the nodes using [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) and uses specific node folders mounted as a volume into the DaemonSet container (redirected file system).

{% if product == "yandex-cloud" %}
![](../../_assets/overview/solution-library-icon.svg)A comprehensive solution in [Osquery and kubequery in K8s.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/kubernetes-security/osquery-kubequery)

{% endif %}
#### Container files {#fim-container-files}

One of the methods to solve this task:

1. Use [readOnlyRootFilesystem](https://www.thorsten-hans.com/read-only-filesystems-in-docker-and-kubernetes/) in pods.
2. Make sure to mount folders to write the data to as separate volumes: as emptydir or individual disks.

If you mount folders as emptydir, files are stored on the node in the folder `/var/lib/kubelet/pods/PODUID/volumes/kubernetes.ioempty-dir/VOLUMENAME`. To ensure data integrity, you can monitor this folder by Osquery as [OS node files](#fim-OS-files).

In the case of separate disks (not emptydir), you can mount volumes in read mode to the above-mentioned DaemonSet running Osquery.

To control file integrity on the Kubernetes nodes, you can also use the tools listed in [Integrity control](secure-config.md#integrity-control).

There exist dedicated free solutions for Kubernetes nodes from Google or Argus, including [file-integrity-operator](https://github.com/openshift/file-integrity-operator).

## Data encryption and {{ managed-k8s-short-name }} secret management {#encryption-and-secret-management}

At the Kubernetes etcd level, encrypt secrets using an in-built [mechanism from {{ yandex-cloud }}](../../managed-kubernetes/concepts/encryption.md).

We recommend that you use SecretManager solutions to work with Kubernetes secrets. [{{ lockbox-name }}](../../lockbox/index.yaml) is such a solution in {{ yandex-cloud }}.

{% if product == "yandex-cloud" %}
{{ lockbox-name }} was integrated with Kubernetes using the [External Secrets](https://external-secrets.io/latest/) open-source project. The solution is available in {{ marketplace-name }} for Kubernetes in the basic simplified scenario: [External Secrets Operator with Yandex Lockbox support](/marketplace/products/yc/external-secrets).

Useful instructions on working with External Secrets:

* [Instructions](https://external-secrets.io/latest/provider-yandex-lockbox/) to work with External Secrets and {{ lockbox-name }} from the project description.
* [Instructions](../../lockbox/tutorials/kubernetes-lockbox-secrets.md) to work with External Secrets and {{ lockbox-name }} from the {{ yandex-cloud }} documentation.

Many methods to differentiate access to secrets using this tool have been [described](https://external-secrets.io/latest/guides-multi-tenancy/#eso-as-a-service).

The most secure recommended option for encrypting secrets is ESO as a Service (External Secrets Operator as a service). In this case, the global administrator has access to the namespace where ESO is installed, and administrators of specific namespaces create their respective [`SecretStore`](https://external-secrets.io/latest/api-secretstore/) objects (where they specify {{ iam-short-name }} authorized access keys for their {{ lockbox-short-name }} secrets). If this `SecretStore` object is compromised, only the authorized key of one specific namespace is compromised (rather than all of them, as in the case of Shared ClusterSecretStore).

{% endif %}
### Encryption in transit {#encryption-in-transist}

For in-transit encryption, use TLS interaction between pods. If you can't use TLS interaction, use service mesh solutions:

* [Istio](https://istio.io/)
* [Linkerd](https://linkerd.io/)

### Encryption at rest {#encryption-at-rest}

If you need to encrypt your stored data, you can use:

* {{ kms-name }}, for encrypting data at the application level (including when you use persistent volumes).
* A custom method of data encryption. However, in this case, protection of the keys and of the key management procedure is the sole responsibility of the user.

## Protection against malicious code in {{ managed-k8s-short-name }} {#malware-protection}

{% if product == "yandex-cloud" %}

There are two levels where you can enable malicious code protection in Kubernetes:

* Container Registry level protection.
* OS-level protection of Kubernetes nodes.

Security scanner in [{{ container-registry-name }}](../../container-registry/concepts/vulnerability-scanner.md).

{% endif %}

To protect the containerization host levels, you can use a variety of paid and free solutions from the "Runtime security" and "Antivirus engine" classes. Examples of free solutions:

* [Kubernetes ClamAV](https://cloud.google.com/community/tutorials/gcp-cos-clamav)
* [Sysdig Falco](https://falco.org/) (it can also function as an Intrusion Detection System)

Be sure to also use the Kubernetes built-in support for [AppArmor](https://kubernetes.io/docs/tutorials/security/apparmor/) and [Seccomp](https://kubernetes.io/docs/tutorials/security/seccomp/).

{% if product == "yandex-cloud" %}
![](../../_assets/overview/solution-library-icon.svg)[Analyzing Kubernetes security logs in ELK: audit logs, policy engine, falco.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/auditlogs/export-auditlogs-to-ELK_k8s)

{% endif %}
## Vulnerability management {{ managed-k8s-short-name }} {#vulnerability-management}

{{ yandex-cloud }} within {{ managed-k8s-short-name }} is in charge of vulnerability management and security updates on the [master](../../managed-kubernetes/concepts/index.md#master). The user must independently control vulnerabilities on the Kubernetes worker nodes.

### Scanning for vulnerabilities {#vulnerability-scanning}

You can break vulnerability scanning into the following levels: 

* Image-level vulnerability scanning.
* Vulnerability scanning of the OS nodes in Kubernetes.

Vulnerability scanning at the image level is detailed in [Protection against malicious code in {{ managed-k8s-short-name }}](#malware-protection).

Examples of free universal solutions for vulnerability scanning of the OS nodes in Kubernetes are given in [Scanning for vulnerabilities](vulnerability-management.md#vulnerability-scanning).

There also exist both paid and free solutions for scanning Kubernetes hosts for vulnerabilities: for example, such free tools as kube-hunter and trivi (scan filesystem).

## Security updates {#security-updates}

{{ managed-k8s-short-name }} issues updates in a regular manner. To meet the Information Security standards:

* Select a relevant update channel and enable either automatic installation of updates, or manual installation immediately after publication in the selected channel.
* Double-check that the ad settings meet the Information Security standards.
* Use one of the three latest Kubernetes versions, because updates (including security updates) are only released for these versions.

## Backup and recovery {#backup-and-restore}

Set up backups in {{ managed-k8s-short-name }} by following the [guide](../../managed-kubernetes/tutorials/backup.md). When storing your backups in {{ objstorage-name }}, follow recommendations from the [Secure configuration for {{ objstorage-name }}](secure-config.md#object-storage).

## Security policies in Kubernetes {#kubernetes-security-policies}

Requirements listed in [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) from Kubernetes let you prevent threats related to Kubernetes objects.

To implement the requirements, you can either use the Kubernetes built-in [Pod Security Admission Controller](https://kubernetes.io/docs/setup/best-practices/enforcing-pod-security-standards/) tool or open-source software (for example, other Admission Controllers: OPA Gatekeeper, Kyverno).

Examples using Kyverno:

{% if product == "yandex-cloud" %}
* ![](../../_assets/overview/solution-library-icon.svg)[Analyzing Kubernetes security logs in ELK: audit logs, policy engine, falco.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/auditlogs/export-auditlogs-to-ELK_k8s)
* ![](../../_assets/overview/solution-library-icon.svg)[Example of setting up role models and policies in {{ managed-k8s-short-name }}.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/kubernetes-security/auth_and_access/role-model-example)

{% endif %}
To control compliance with Pod Security Standards, you can also use the following tools within CI/CD:

* [Kyverno CLI](https://kyverno.io/docs/kyverno-cli/)
* [The gator CLI](https://open-policy-agent.github.io/gatekeeper/website/docs/gator)

Or a separate [Kubesec](https://kubesec.io/) tool.

## Practices for securely creating and using Docker images {#best-practices-docker-image}

Use these check lists to meet requirements for secure creation of images:

* [Dockerfile best practices](https://sysdig.com/blog/dockerfile-best-practices/#2-2)
* [Kubernetes Security Checklist and Requirements](https://github.com/Vinum-Security/kubernetes-security-checklist/blob/main/README.md)

You can control Dockerfile in your CI/CD pipeline using the [Conftest](https://www.conftest.dev/) utility.

## Runtime protection {#runtime-protection}

When using minimal images or distroless images without a shell, use [ephemeral containers](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/).

{% if product == "yandex-cloud" %}
![](../../_assets/overview/solution-library-icon.svg)[Solution running Osquery.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/kubernetes-security/osquery-kubequery)

{% endif %}
## Load sharing between nodes {#load-sharing}

Data loads with different security contexts (i.e., different severities of data processed) must be processed on different Kubernetes nodes. To enable load sharing within a cluster, use different node groups with different settings for [`node labels`](https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/) and [`node taints`](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/). Be sure to combine both settings.

## Collecting, monitoring, and analyzing audit logs {{ managed-k8s-short-name }} {#collection-monitoring-analysis-audit-logs}

Events available to the user in the {{ managed-k8s-short-name }} service can be classified as levels:

{% if product == "yandex-cloud" %}
* Kubernetes API events (Kubernetes Audit logging).
   {% endif %}
* Kubernetes node events.
* Kubernetes pod events.
* Kubernetes metrics.
* Flow logs Kubernetes.

{% if product == "yandex-cloud" %}
### Kubernetes API level (Kubernetes Audit logging) {#kubernetes-api-level}

Audit events are collected from the Kubernetes API level by {{ cloud-logging-name }}.

![](../../_assets/overview/solution-library-icon.svg)[Analyzing Kubernetes security logs in ELK: audit logs, policy engine, falco.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/auditlogs/export-auditlogs-to-ELK_k8s)

{% endif %}
### Kubernetes nodes level {#kubernetes-nodes-level}

Kubernetes node level events are collected and exported similarly to [collecting OS audit logs](audit-logs#os-level).

### Kubernetes pods level {#kubernetes-pods-level}

Different options for collecting and exporting pod-level events in Kubernetes is described in the [Kubernetes official documentation](https://kubernetes.io/docs/concepts/cluster-administration/logging/).

{% if product == "yandex-cloud" %}
Examples of collecting and exporting pod logs:

* Exporting logs to {{ cloud-logging-name }} using Fluent Bit is described in the [{{ managed-k8s-short-name }}](../../managed-kubernetes/tutorials/fluent-bit-logging.md) documentation.
* Exporting pod logs into Elastic or Splunk is described in the [Yandex Cloud Security Solution Library](https://github.com/yandex-cloud/yc-solution-library-for-security/blob/master/kubernetes-security/osquery-kubequery/README_RU.md).

The [Filebeat](/marketplace/products/yc/filebeat) plugin for transferring logs to Elastic and [Fluent Bit with a {{ cloud-logging-name }} plugin](/marketplace/products/yc/fluent-bit) are available in {{ marketplace-name }}.

{% endif %}
### Kubernetes metrics {#kubernetes-metrics}

{{ monitoring-name }} includes a set of metrics to analyze availability of Kubernetes objects and their behavioral anomalies.

Instructions on how to export {{ monitoring-name }} metrics is given in the section [Exporting events to SIEM](audit-logs.md#metriki-yandex-monitoring).

{% if product == "yandex-cloud" %}
### Flow logs Kubernetes {#flow-logs-kubernetes}

![](../../_assets/overview/solution-library-icon.svg)[Exporting flow logs to {{ objstorage-full-name }}.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/auditlogs/cilium-s3)

{% endif %}
### {{ managed-k8s-short-name }} role model audit {#role-model-audit}

In the {{ managed-k8s-short-name }} console, you can audit the current role model used in the service. For this, go to the **Access management** tab in the service.

You can also use:
* [KubiScan](https://github.com/cyberark/KubiScan)
* [Krane](https://github.com/appvia/krane)

{% if product == "yandex-cloud" %}
## Kubernetes security solutions comparison {#security-solutions-comparison}

![](../../_assets/overview/solution-library-icon.svg)[Kubernetes security solutions comparison.](https://github.com/yandex-cloud/yc-solution-library-for-security/tree/master/kubernetes-security/choice_of_solutions)
{% endif %}