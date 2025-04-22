# Policies
В работе администраторов часто нужны различные гибкие политики использования сервиса. Посмотрим на примеры:
>Я, как раз ответственный за namespace, хочу ограничить изменения объектов с label'ов `tier=production` в выходные.

>Я, как разработчик контроллера Service'а, хочу ограничить использование функции cpu set только для объектов в namespace'е _saas_.

>Я, как ответственный за namespace, хочу, чтобы объекты обязательно имели label'ы `tier=[production,prestable,testing]`. Таким образом я смогу фильтровать объекты и настраивать мониторинг, форсируя единый стиль.


# Решение: open policy agent gatekeeper
В экосистеме kubernetes есть готовый механизм:
  * [admission hook'и](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#admission-webhooks)
  * реализация политик в виде [open policy agent gatekeeper](https://github.com/open-policy-agent/gatekeeper)

Логика работы:
  * gatekeeper запускается в виде сервиса внутри кластера
  * подключается к api-server'у, подписавшись на изменения объектов политик
  * настраивает себя в качестве admission hook'а, "одобряя" изменения объектов

Все настройки выполняются через объекты KRM и kubectl. Пример:
  * Запускаем и создаём CRD
```
❯ kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/release-3.5/deploy/gatekeeper.yaml

namespace/gatekeeper-system configured
resourcequota/gatekeeper-critical-pods configured
customresourcedefinition.apiextensions.k8s.io/configs.config.gatekeeper.sh configured
customresourcedefinition.apiextensions.k8s.io/constraintpodstatuses.status.gatekeeper.sh configured
customresourcedefinition.apiextensions.k8s.io/constrainttemplatepodstatuses.status.gatekeeper.sh configured
customresourcedefinition.apiextensions.k8s.io/constrainttemplates.templates.gatekeeper.sh configured
serviceaccount/gatekeeper-admin configured
podsecuritypolicy.policy/gatekeeper-admin configured
role.rbac.authorization.k8s.io/gatekeeper-manager-role configured
clusterrole.rbac.authorization.k8s.io/gatekeeper-manager-role configured
rolebinding.rbac.authorization.k8s.io/gatekeeper-manager-rolebinding configured
clusterrolebinding.rbac.authorization.k8s.io/gatekeeper-manager-rolebinding configured
secret/gatekeeper-webhook-server-cert configured
service/gatekeeper-webhook-service configured
deployment.apps/gatekeeper-audit configured
deployment.apps/gatekeeper-controller-manager configured
poddisruptionbudget.policy/gatekeeper-controller-manager configured
validatingwebhookconfiguration.admissionregistration.k8s.io/gatekeeper-validating-webhook-configuration configured
```
  * Создаём шаблон ограничений
```
❯ cat k8srequiredlabels_template.yaml 
apiVersion: templates.gatekeeper.sh/v1beta1
kind: ConstraintTemplate
metadata:
  name: k8srequiredlabels
spec:
  crd:
    spec:
      names:
        kind: K8sRequiredLabels
      validation:
        # Schema for the `parameters` field
        openAPIV3Schema:
          properties:
            labels:
              type: array
              items: string
  targets:
    - target: admission.k8s.gatekeeper.sh
      rego: |
        package k8srequiredlabels

        violation[{"msg": msg, "details": {"missing_labels": missing}}] {
          provided := {label | input.review.object.metadata.labels[label]}
          required := {label | label := input.parameters.labels[_]}
          missing := required - provided
          count(missing) > 0
          msg := sprintf("you must provide labels: %v", [missing])
        }

❯ kubectl apply -f k8srequiredlabels_template.yaml 
constrainttemplate.templates.gatekeeper.sh/k8srequiredlabels created
```
  * Создаём политику ограничений на базе шаблона (требуем label):
```
❯ cat labels.yaml 
apiVersion: constraints.gatekeeper.sh/v1beta1
kind: K8sRequiredLabels
metadata:
  name: pod-must-have-tier
spec:
  match:
    kinds:
      - apiGroups: [""]
        kinds: ["Pod"]
  parameters:
    labels: ["tier"]

❯ kubectl apply -f /tmp/labels.yaml 
k8srequiredlabels.constraints.gatekeeper.sh/pod-must-have-tier created
```
  * Проверяем, что теперь мы не можем создать pod без обязательного label'а
```
❯ kubectl run ephemeral-demo --image=busybox:latest --restart=Never 
Error from server ([pod-must-have-tier] you must provide labels: {"tier"}): admission webhook "validation.gatekeeper.sh" denied the request: [pod-must-have-tier] you must provide labels: {"tier"}
```
