argoCD git repo
login:
```
argocd login --insecure --grpc-web [$(kubectl get service/argocd-server -n argocd | grep -o "2001[^\ ]*")]:443 --username admin --password $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
```
add repos:
```
argocd repo add https://git@git.arc-vcs.yandex-team.ru/argocd --insecure-skip-server-verification --username git --password $(arc token show)
```
deploy app:
```
argocd app create argocd --repo https://git@git.arc-vcs.yandex-team.ru/argocd --path apps/argocd/ --dest-server https://kubernetes.default.svc --dest-namespace argocd
argocd app create dashboard --repo https://git@git.arc-vcs.yandex-team.ru/argocd --path apps/dashboard --dest-server https://kubernetes.default.svc
```
sync app:
```
argocd app sync ingress-nginx --async --force
```
deploy helm chart:
```
argocd repo add https://helm.influxdata.com/ --type helm --name influxdata
argocd app create telegraf-operator --repo https://helm.influxdata.com --helm-chart telegraf-operator --dest-namespace default --revision 1.3.8 --dest-server https://kubernetes.default.svc
```
