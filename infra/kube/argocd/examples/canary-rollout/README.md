# Argo Rollouts

Argo Rollouts is a Kubernetes controller and set of CRDs which provide advanced
deployment capabilities such as blue-green, canary, canary analysis,
experimentation, and progressive delivery features to Kubernetes.

## Canary deployment

Simply setup strategy for canary deployment

```yaml
strategy:
  canary:
    canaryService: canary-demo-preview
    steps:
    - setWeight: 20
    - pause: {}
    - setWeight: 40
    - pause: {duration: 10}
    - setWeight: 60
    - pause: {duration: 10}
    - setWeight: 80
    - pause: {duration: 10}
```

In this workflow described canary deployment with steps.

1. Trigger rollout start.

2. Firstly rollout updates 20% instances with new version.

3. After this canary deployment you need manually approve further rollout.

4. After approve rollout starts deploy all others instances with configurable waits.

## Further read

* [Other examples](https://github.com/argoproj/argo-rollouts/tree/master/examples)

