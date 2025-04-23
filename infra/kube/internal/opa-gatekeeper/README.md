# OPA Gatekeeper
Тут храним информацию о инсталляции [OPA Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/) в crossplane кластере.

What we have:
  * `gatekeeper.yaml` - fat YAML со всеми ресурсами (взят с официального сайта)
  * `examples/` - каталог примеров использования политик
  * `policies/` - используемые политики (рассчитываем, что можно сделать `kubectl apply -f .`)

# Emergency
In case of fire disable gatekeeper:
```
kubectl delete validatingwebhookconfigurations.admissionregistration.k8s.io gatekeeper-validating-webhook-configuration
```