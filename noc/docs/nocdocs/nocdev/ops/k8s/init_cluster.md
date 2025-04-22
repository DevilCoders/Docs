# Процесс наливки нового клустера k8s в NOCDEV.

## Базовая наливка.
- создаем в дц три lxc контейнера на разных машинах под мастера
есть несколько условий для выбора гипервизоров:
гипервизоры должны быть с ядром выше 5.3(можно обновить, не стоит брать из группы %nocdev-dom0-lxd-kernel)
берем гипервизоры где уже есть контейнеры для которых есть acl на свитчах(эти гипервизоры сложно переналить, пусть так и будет, например grad,nocauth,netmap и т.д.)
пример:
```
[Serial] root> describe %nocdev-k8s-sas 
  Group: nocdev-k8s-sas
  Project: noc
  Description: 
@sas-1-2-1
sas-k8s2.net.yandex.net
@sas-11
sas-k8s0.net.yandex.net
@sas-2-4-1
sas-k8s1.net.yandex.net
Total: 3
```
- тюним профиль добавляя специальный:
```
lxc profile add container-name--net k8s
```
требуется это для возможности создания подконтейнеров и другой всякой штуки для кубера([статейка](https://www.adaltas.com/en/2020/02/04/install-debug-lxd-k8s/)).
- для worker nodes наливаем железные тачки в walle проекте [Nocdev k8s nodes](https://wall-e.yandex-team.ru/projects/hosts?project=nocdev-k8s-nodes), после чего добавляем его в нужную группу в кондукторе(например %nocdev-nodes-sas).
- создаеть L3 balancer для control plane, пример: [балансер](https://l3.tt.yandex-team.ru/service/16220), добавить до него дырки, пример: [puncher](https://st.yandex-team.ru/DOSTUPREQ-298306)
- не забыть в контейнерах перегенерить сеть для появления vip адресов(не забываем ipvs_tun тег в кондукторе на группу).
- добавляем группы в салт, используем юниты по аналогии с существующей схемой.
- солим и дергаем pkgver на мастерах до успешного завершения.

## Инициализация клустера.
- на любом из мастеров выполняем(не забываем указать нужный балансер):
```
cd /root/init; kubeadm init --pod-network-cidr=2001:db8:42:0::/56 --service-cidr=2001:db8:42:1::/112 --control-plane-endpoint "$api-l3-hostname:6443" --upload-certs --token-ttl 0 2>&1 | tee init.txt
```
Сети везде используем фиксированные, они нужны для внутренних нужд. Собственно взяты они из доки, какие использовать принципиальной разницы нет.
результатом должно быть появление токена для join`a других нод, так же нас интересует discovery-token-ca-cert-hash(так же в выводе будет много интересной инфы, например как перевыпустить токен).
при проблемах можно использовать ```kubeadm reset -f``` и ретраить, но все должно быть хорошо.
- добавляем токен и хэш в [yav](https://yav.yandex-team.ru/secret/sec-01g4hekqrevfgzsv17825jg98d) , нужно это для того чтобы воркер ноды подключались к control plane самостоятельно.
- сразу правим coredns, из-за локального unbound мы получаем [loop](https://coredns.io/plugins/loop/):
меняем '/etc/resolv.conf' на '2a02:6b8:0:3400::5005'
```
kubectl patch -n kube-system configmap/coredns --type merge --patch-file coredns.yaml
```
- меняем mode в конфиге kube-proxy на ipvs и masqueradeAll на true:
```
kubectl patch -n kube-system configmap/kube-proxy --type merge --patch-file kube-proxy.yaml
```
рестартим поды:
```
kubectl get po -n kube-system | grep kube-proxy | awk '{print $1}' | while read name; do kubectl delete po -n kube-system $name; done
```
- включаем cni(оригинальный yaml и патченный лежат в /root/init/calico для удобство просмотра diff) и применяем политики разрешающие трафик:
```
kubectl kustomize . | kubectl apply -f -
calicoctl apply --allow-version-mismatch -f calico-policy.yaml 
```
- join`им остальные два мастера используя команду из результата инициализации первого мастера. При проблемах ```kubeadm reset cleanup-node```.
Есть прикол: если vip адреса вы подняли, то для join их надо удалить, ведь иначе join попытается идти локально а не на балансер:(
- после всего этого доналиваем и солим воркер ноды, они подключаться сами:
```
modprobe br_netfilter
modprobe overlay
apt-get update
apt-get install repo-noc-stable repo-noc-bionic yandex-salt-components -y
apt-get update
apt-get install config-noc-common config-monitoring-pkgver config-noc-salt-minion -y
salt-call state.highstate
pkgver.pl -i -y
```
Сами то сами, но надо поправить calico ippool конфиги, после joinа новой ноды запускаем на любом мастере:
```
calico-manager | calicoctl apply --allow-version-mismatch -f -
```
посмотреть пулы:
```
calicoctl get ippool
```
или:
```
kubectl get ippool
```
деплой argocd, token для git pull берем из 'arc token show':
```
cd /root; git clone https://git@git.arc-vcs.yandex-team.ru/argocd
cd argocd/apps/argocd; kubectl create namespace argocd; kubectl kustomize . | kubectl apply -n argocd -f -
```
ждем когда все запускается, потом добавляем репы и приложения:
```
argocd login --insecure --grpc-web [$(kubectl get service/argocd-server -n argocd | grep -o "2001[^\ ]*")]:443 --username admin --password $(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
argocd repo add https://git@git.arc-vcs.yandex-team.ru/argocd --insecure-skip-server-verification --username git --password $(arc token show)
argocd app create argocd --dest-namespace argocd --repo https://git@git.arc-vcs.yandex-team.ru/argocd --path apps/argocd --dest-server https://kubernetes.default.svc
argocd app sync argocd --async --force
argocd app create ingress-nginx --dest-namespace ingress-nginx --repo https://git@git.arc-vcs.yandex-team.ru/argocd --path apps/ingress-nginx --dest-server https://kubernetes.default.svc
argocd app sync ingress-nginx --async --force
cd /root/argocd/apps/argocd-ingress; helm install argocd-ingress . -f values-test.yaml
```
после этого уже заработает морда argocd и там будут базовые приложухи
## Интересная инфа.
- кубер сам выпускает ca и сертификаты, посмотреть можно так: ```kubeadm certs check-expiration```
- сертификаты обновляются сами при апгрейде кубер пакетов [дока](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-certs/#automatic-certificate-renewal)
- мы решили использовать стандартный механизм работы с сертификатами для упрощения.
- основные серты действуют 10 лет, остальные 1 год, можно дернуть обновление руками, инфа есть в той же доке, примерно так ```kubeadm certs renew all```, после этого требуется рестарт нод.
- можно дрейнить ноды для рестарта, дока по апгрейду [дока](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

## TODO
- придумать как более красиво править или заливать сразу верные конфигмапы coredns и kube proxy.
- убрать cmd.run в салте.
- в calico-manager заюзать calico api либу(https://st.yandex-team.ru/NOCDEV-7543) и запускать это автоматически, лучше всего сделать из этого контроллер.
