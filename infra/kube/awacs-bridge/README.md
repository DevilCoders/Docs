## awacs bridge
Сервис синхронизирует endpoint'ы `NodePort` сервисов из kubernetes в YP.SD. Для этого ему нужны:
  * kubeconfig:
    * токен сервисного аккаунта (с правами на чтение всех нод и нужных endpoint'ов)
    * CA, которым подписан сертификат api-server'а
    * адрес api-server'а
  * `YP_TOKEN` - для доступа в YP
## Traffic flow: kube side
Принцип работы - использование существующей сетевой связности между подами в RTC (балансер) и нодами kubernetes'а. Отсюда требования к кластеру:
  * ноды кластера должны быть в ipv6 сети Яндекса и иметь сетевой макрос
  * должен быть открыт FW от макроса, в котором запущен балансер awacs до нод kubernetes'а  
  Это может быть один макрос, тогда доступ отдельно обеспечивать не нужно.

Для того, чтобы трафик, приходящий в ноды, попадал в поды - нужно настроить сервис с типом `NodePort`:
```
kind: Service
metadata:
    name: awacs-lb
spec:
  externalTrafficPolicy: Local # отправлять трафик только на поды локальной ноды
  ipFamilies:  # нужно указать IPv6 как минимум
  - IPv4
  - IPv6
  ipFamilyPolicy: RequireDualStack  # обязательно настроить v6
  ports:  # выбрать порт
  - nodePort: 32000  # этот порт используется в правиле для тестов в _CLOUD_YANDEX_CLIENTS_CROSSPLANE_NETS_
    port: 80
    protocol: TCP
    targetPort: 80
  selector:  
    app: nginx
  type: NodePort  # обязательно выставлять как порт ноды
```

## cервисный аккаунт
Для того, чтобы bridge мог подключиться к апи серверу, ему нужно аутентифицироваться. Для корректно создать и настроить сервисный аккаунт.
```
kubectl apply -f - <<EOF
apiVersion: v1
kind: ServiceAccount
metadata:
  name: awacs-bridge
EOF

TOKENNAME=$(kubectl get sa awacs-bridge -o jsonpath='{.secrets[0].name}')
TOKEN=$(kubectl get secrets $TOKENNAME -o jsonpath='{.data.token}' | base64 --decode)
CA=$(kubectl get secret $TOKENNAME -o "jsonpath={.data['ca\.crt']}")
```
Для локального запуска настроить `kubeconfig` можно так:
```
export KUBECONFIG=/tmp/kube
kubectl config set clusters.default.server https://178.154.240.5
kubectl config set clusters.default.certificate-authority-data $CA
kubectl config set users.awacs-bridge.token $TOKEN
kubectl config set contexts.default.user awacs-bridge
kubectl config set contexts.default.cluster default
kubectl config use-context default
```
Далее нужно разрешить аккаунту читать node'ы и endpoint'ы:
```
kubectl apply -f - <<EOF
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: awacs-bridge
rules:
- apiGroups: [""]
  resources: ["services", "nodes", "endpoints"]
  verbs: ["get", "watch", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: allow-awacs-bridge
subjects:
- kind: User
  name: system:serviceaccount:default:awacs-bridge
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: awacs-bridge
  apiGroup: rbac.authorization.k8s.io
EOF
```

## User story
  * Настраиваем роли для контроллера.
  * Получаем `YP_TOKEN`, например, для роботного аккаунта на стаффе.
  * Запускаем контроллер в своём кластере используя:
    * `command: ['/awacs-bridge', '-name', '<name>']` - выбираем уникальное имя для своего контроллера, например, `taxi-prod`.
    * `serviceAccount: awacs-bridge` - тот, что создали выше
  * Создаём сервис с `spec.type: NodePort`. Этого достаточно - контроллер начнёт экспортировать endpoint'ы этого сервиса (в ДЦ SAS), используя 
    * `service.spec.ports[0].nodePort` в качестве порта
    * IPv6 адрес ноды, на котором запущен под в качестве адреса endpoint'а
  Название endpointset'а будет сформировано как: `{service.Name}.{service.Namespace}.{controller.Name}`, например `nginx-deployment.default.taxi-prod`.
  * Указываем в AWACS в качестве бекенда YP.SD, выбирая кластер и имя endpoinset'а.

## Tips&tricks
Проверить endpoint'ы:
```
ya tool yp select --address sas endpoint --filter='[/meta/endpoint_set_id]="nginx-deployment.default.nekto0n"' --selector /meta/id --selector /spec/ip6_address --selector /spec/port
```


## Known issues/TODO:
  * Удаление/изменение endpoint'ов - реализовано только добавление и удаление целиком всего endpoinset'а.