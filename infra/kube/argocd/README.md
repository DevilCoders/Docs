# [Argo](https://argoproj.github.io)

Get More Done with Kubernetes!

* [Argo CD](https://argoproj.github.io/cd/) - Declarative continuous delivery with a fully-loaded UI.
* [Argo Rollouts](https://argoproj.github.io/rollouts/) - Advanced Kubernetes deployment strategies such as Canary and
  Blue-Green made easy.
* [Argo Workflows](https://argoproj.github.io/workflows/) - Kubernetes-native workflow engine supporting DAG and
  step-based workflows.
* [Argo Events](https://argoproj.github.io/events/) - Event based dependency management for Kubernetes.

## Pros:

* Describe all infra (any cloud resources, deployments, ci workflows) in same way. And use common tooling to rule them
  all!
* Use kubernetes everywhere. (Deploy scalable application in k8s, create CI workers in k8s, use k8s resource model to
  describe cloud resources)
* You can use argo stack with any git vendor (gitlab, github, bitbucket)
* Easy to integrate all part of your infrastructure.
* UI for all parts of infrastructure.

## Known issues

* Authentication and authorization. You can log in argo only as admin.

# Problems and solving

1. Common tolling for infrastructure and deployments.

Since we're using crossplane to control cloud resources we can use common rich kubernetes tooling (kubectl, helm,
kustomize, k8s rbac, dashboards, validation hooks and many others) to manage cloud resources as well as vanila
kubernetes resources such as Deployment.

2. Hard to learn kubernetes and cloud infra.

With Crossplane and ArgoCD you can set up templates for deployments and infrastructure resources such as Managed
Kubrenetes, PostgreSQL and have same UI for both.

* Templating

Since crossplane use kubernetes CRD to describe infrastructure resources we can use helm or kustomize to template both
crossplane resources and deployments. In multi-cloud infra team we have some example templates:
for [ManagedKubernetes in AWS](../aws/helm/kubernetes), for [Canary deployments](../examples/helm/canary) and others.

With helm developer defines only valuable subset of parameters in `values.yaml`. Other parameters defined by more
experienced

Example for deployment:

```yaml
projectName: "infra"
projectSuffix: "dev" # prod/prestable/testing/dev
resources:
    requests:
        memory: 32Mi
        cpu: 5m
replicas: 5
image:
    repo: argoproj/rollouts-demo
    version: green
```

* UI

If it's still hard, you'll have web UI dashboard where all resources will be shown with their status.

![argo-cd-infra](assets/argo-cd-infra.png)

3. Advanced deployments (canary / green blue).

There are no easy way to set up canary deployment vai vanilla kubernetes `Deployment` resource. But with Argo Rollouts
addon you'll have opportunity to easily set up canary or green/blue deployment strategy.

Example canary strategy deployment specification:

```yaml
strategy:
    canary:
        steps:
            -   setWeight: 20
            -   pause: { }
            -   setWeight: 40
            -   pause: { duration: 60 }
            -   setWeight: 60
            -   pause: { duration: 60 }
            -   setWeight: 80
            -   pause: { duration: 60 }
```

Also, with Argo Rollouts you can set up progressive deployments. And trigger events based on metrics in prometeus or
with any custom hooks which describe application state during deployment.

4. Multi-staging. Isolated testing and production.

To isolate multiple stages we'll use different AWS account / Azure subscription for different stages. In this paradigm
we'll easily separate all cloud resources in multiple stages. But we'll still be able to control all from one source of
truth (git repo) if we'll live in GitOps paradigm. Also, if we'll have different accounts for different stages we'll
easily assign different roles for different stages.

5. CI/CD workflows and releases automation.

Lets describe common release cycle:

* Write code
* Review code
* Run unit tests
* Build image
* Deploy on testing
* Run integration test and test something manually
* Deploy canary on some share of production
* Deploy everywhere

In GitOps paradigm as developer you can and need to manage system ony from git. You need to describe desired state of
your production using code and configs. After them automated workflows do others for you (build application image, run
tests, deploy testing, deploy production).

For CD part of system (provisioning infrastructure, testing and production deployment) we advise using ArgoCD. As user
you describe production with kubernetes yamls in git repo in declarative way and commit changes. On commit ArgoCD
applies configs in Kubernetes cluster and controllers starts to semi-magically bring real environment to target state.

Also, we have CI part of release on which we need to run some automated tests and build application artifacts. To
implement this steeps we'll use Argo Workflows. With them, you can describe any action in any environments. All
workflows run in kubernetes cluster in isolated docker containers.

Example lets describe image build in Argo Workflow:

```yaml
-   name: image
    inputs:
        parameters:
            -   name: path
            -   name: image
    # Mount the configuration so we can push the image.
    # This should create the /.docker/config.json file.
    volumes:
        -   name: docker-config
            secret:
                secretName: docker-config
    container:
        image: moby/buildkit:v0.9.3-rootless
        volumeMounts:
            # Mount code which we clone from git on previouse steps
            -   name: work
                mountPath: /work
            -   name: docker-config
                mountPath: /.docker
        workingDir: /work/repo/{{inputs.parameters.path}}
        env:
            -   name: DOCKER_CONFIG
                value: /.docker
        command:
            - docker
        args:
            - build
            - .
```

6. Security.

In GitOps paradigm you can totally prohibit developers manual access to production. Because you can do everything using
git! And use familiar to everyone best practices such as code review in case infrastructure provisioning. ArgoCD,
ArgoRollouts, Crossplane and other kubernetes controllers we'll perform real actions to reach target state using service
accounts credentials.

## Demo installation

![demo](assets/demo-installation.png)

* Use git as source of truth

    1. Store code.
    2. Develop, review code.
    3. Describe cloud resources.
    4. Describe testing environment.
    5. Describe prod environment.
    6. Describe CI workflows (images builds, tests).

* Deploy all infra components in control-plane Kubernetes

    1. ArgoCD - to sync resource specifications from git to multiple Kuberneteses
    2. Crossplane - to describe and manage cloud resources such as Kubernetes, PostgreSQL, S3 in k8s CRD model.
    3. Argo Workflow - to run CI workflows and use Kubernetes pods as CI workers.

* Use different AWS accounts for testing and prod environments
* In each account create managed Kubernetes (EKS in AWS) for runtime.
* In each runtime kubernetes (testing and prod) use same Argo Rollouts controllers. To use advanced deploy features.

## Store all specs in git repo

![git](assets/git.png)

## Sync resources in Kubernetes with ArgoCD

![argo-cd](assets/argo-cd.png)

## Deploy application with Argo Rollouts

![argo-rollouts](assets/argo-rollouts.png)

## Describe any workflows with Argo Workflows

![argo-workflows](assets/argo-workflows.png)
