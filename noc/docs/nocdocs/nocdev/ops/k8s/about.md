# Мотивация

Во избежание кольцевых зависимостей критичной инфраструктуры NOCDEV от внутренних облаков нам приходится иметь свое железо.
Исторически машины наливались руками и использовались как bare metal решения.
С недавнего времени мы постарались большей частью перейти на [lxd контейнеры](https://wiki.yandex-team.ru/noc/nocdev/ops/newlxdcontainer/).
Lxd является хорошим проверенным решением, однако слабо автоматизировано, концепция не подразумевает катку через images, переезд контейнеров
тоже не подразумевается, быстрое масштабирование затруднено.
Все выше перечисленные нюансы затрудняют унификацию с инфраструктурой живущей в облаках, а так же использование общекомпанейских инструментов(ci/cd etc.).
Так же lxd слабо подходит под тестинги и стейджинги, тем более для автоматического разворачивания окружений.
Было принято решение сделать свое облако на bare metal.
Kubernetes стал в последние годы стандартом дефакто в области облачной инфраструктуры, поэтому был выбран именно он.
Так же уже есть успешный опыт внедрения в компании, больше мотивации у смежный команд [wiki](https://wiki.yandex-team.ru/cloud/devel/selfhost/obsuzhdenija/container-based-cloud-2021/).

## Что получилось сделать

- PoC клустер состоит из шести старых железных серверов в Сасово: 3 мастер ноды под L3 балансером + 3 воркер ноды.
- Железо:
  - setup профиль с большим разделом под /var.
  - наливка через два проекта в walle(преднастройка, генерация hostname, dns записи).
  - L3 балансер над мастер нодами для доступа к kubernetes api.
  - ipv6 only.
- k8s решения:
  - containerd + crictl для контейнеризации.
  - HA cluster with kubeadm [дока](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/).
  - ipv6 only network in for pod network cidr and for service network cidr.
  - ipvs mode in kube proxy.
  - calico cni with calico_backend: "none"(disable dynamic routing), ipv6 only mode.
  - в calico сетки для podов per worker node(прибитые по сути к TOR).
  - yandex docker registry with auth.
  - L3 yandex balancer + nginx ingress

## Как получилось то что получилось, возникшие проблемы

- calico cni был выбран как самый распространенный.
- ipv6 only сервера дают сделать четверку для подов только в случае оверлейной сети, но k8s cni такого не умеют(по крайней мере не удалось найти).
- для ipv6 only calico и многие другие не умеет оверлей, IPIP и vxLAN можно использовать только для v4.
- оверлей не смогли, но использовать серую сетку для podов не получилось тоже, анонсы берда долетают до соседних машин только в L2 сегменте(внутри одной стойки).
- остается попытаться выдавать подам адреса из нашей же TOR сети. Calico такое умеет, так и сделали.
- iptables mode в kube proxy для ipv6 only и NodePort(проброс порта контейнера на внешний порт ноды) не работает из-за баги(два раза делается listen на порт),
 багу зачинили но новой версии кубера еще нет.
- поэтому используем ipvs, ну и в целом ipvs выглядит удобнее и производительнее.
- Сервисный cidr остается серой сеткой, так как мы не можем выделить нормальную сеть(общую для всех машин),
 но это не создает проблем ибо ipvs сервис собирается на каждой машине(будет показано далее на практике).
- coredns конфиг приходится патчить из-за нашего локального unbound, в ином случае coredns подсасывает ::1 и начинает ходить сам в себя.

## Примерный план наливки клустера

- наливаем сами железки.
- тюним sysctl:
```
cat <<EOF | tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF
modprobe overlay
modprobe br_netfilter
cat <<EOF | tee /etc/sysctl.d/99-k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
net.ipv6.conf.default.forwarding    = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF
sysctl --system
```
- containerd:
```
apt-get install containerd -y
mkdir /etc/containerd
containerd config default > /etc/containerd/config.toml
systemctl restart containerd
```
- kubelet, kubeadm, kubectl на все сервера:
```
apt-get update; apt-get install -y apt-transport-https ca-certificates curl
curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
apt-get update; apt-get install -y kubelet kubeadm kubectl
apt-mark hold kubelet kubeadm kubectl
```
не переживаем насчет репы для xenial, другой и правда нет, официальная дока предлагает использовать эту для любых убунт.
- crictl config:
```
echo <<EOF | tee /etc/crictl.yaml
runtime-endpoint: unix:///var/run/containerd/containerd.sock
image-endpoint: unix:///var/run/containerd/containerd.sock
timeout: 10
debug: false
EOF
```
- on master nodes(так же можно найти доку по генерации автдобавления для kubectl):
```
export KUBECONFIG=/etc/kubernetes/admin.conf
echo "export KUBECONFIG=/etc/kubernetes/admin.conf" >> .bashrc
```
- calicoctl:
```
curl -o calicoctl -O -L   "https://github.com/projectcalico/calicoctl/releases/download/v3.19.1/calicoctl-linux-amd64"
chmod +x calicoctl
```
- сделали L3 балансер над мастер нодами порт 6443 и запустили.
- начинаем инициализацию клустера по [доке](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/):
  - запускаем на первой тачке и сохраняем вывод, при этом в control-plane-endpoint указывается ранее созданный балансер:
  ```
  kubeadm init --pod-network-cidr=2001:db8:42:0::/56 --service-cidr=2001:db8:42:1::/112 --control-plane-endpoint "sas-test-k8s0lb.net.yandex.net:6443" --upload-certs
  ...........
  [addons] Applied essential addon: CoreDNS
  [addons] Applied essential addon: kube-proxy
  Your Kubernetes control-plane has initialized successfully!

  To start using your cluster, you need to run the following as a regular user:
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config

  Alternatively, if you are the root user, you can run:
    export KUBECONFIG=/etc/kubernetes/admin.conf

  You should now deploy a pod network to the cluster.
  Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
    https://kubernetes.io/docs/concepts/cluster-administration/addons/

  You can now join any number of the control-plane node running the following command on each as root:

    kubeadm join sas-test-k8s0lb.net.yandex.net:6443 --token 2ra8ri.glkoeme2n8gtioxf \
	  --discovery-token-ca-cert-hash sha256:c4b1ae1923883299b3e7cba68d91f98ac6fd6c8e4a2001dce952ae2e1d00fc81 \
	  --control-plane --certificate-key 51f277abb3218bcbc12939eee5a708981b7b03fd0c96ca8bcf21e83004fc3a89

  Please note that the certificate-key gives access to cluster sensitive data, keep it secret!
  As a safeguard, uploaded-certs will be deleted in two hours; If necessary, you can use
  "kubeadm init phase upload-certs --upload-certs" to reload certs afterward.

  Then you can join any number of worker nodes by running the following on each as root:

  kubeadm join sas-test-k8s0lb.net.yandex.net:6443 --token 2ra8ri.glkoeme2n8gtioxf \
    --discovery-token-ca-cert-hash sha256:c4b1ae1923883299b3e7cba68d91f98ac6fd6c8e4a2001dce952ae2e1d00fc81
  ```
  токены временные и давно инвалидировались, можно не переживать.
  - запускаем `join` из результатов предыдущей команды на остальных нодах, на мастерах для мастера, на воркер нодах для воркер нод.
  - cluster готов, смотрим что говорит нам:
  ```
  sas-test-k8s0.net:~# kubectl get nodes -o wide
  NAME                           STATUS   ROLES                  AGE   VERSION   INTERNAL-IP                        EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION   CONTAINER-RUNTIME
  sas-test-k8s0.net.yandex.net   Ready    control-plane,master   11d   v1.23.3   2a02:6b8:c02:5cc:0:675:9092:86e8   <none>        Ubuntu 18.04.5 LTS   5.4.161-26.1     containerd://1.5.5
  sas-test-k8s1.net.yandex.net   Ready    control-plane,master   11d   v1.23.3   2a02:6b8:c02:5cc:0:675:9092:874e   <none>        Ubuntu 18.04.5 LTS   5.4.161-26.1     containerd://1.5.5
  sas-test-k8s2.net.yandex.net   Ready    control-plane,master   11d   v1.23.3   2a02:6b8:c02:76c:0:675:9094:29ba   <none>        Ubuntu 18.04.5 LTS   5.4.161-26.1     containerd://1.5.5
  sas-test-n0.net.yandex.net     Ready    <none>                 11d   v1.23.3   2a02:6b8:c02:563:0:675:9091:660    <none>        Ubuntu 18.04.5 LTS   5.4.161-26.1     containerd://1.5.5
  sas-test-n1.net.yandex.net     Ready    <none>                 11d   v1.23.3   2a02:6b8:c02:563:0:675:9092:8bf0   <none>        Ubuntu 18.04.5 LTS   5.4.161-26.1     containerd://1.5.5
  sas-test-n2.net.yandex.net     Ready    <none>                 11d   v1.23.3   2a02:6b8:c02:5cc:0:675:9092:8c62   <none>        Ubuntu 18.04.5 LTS   5.4.161-26.1     containerd://1.5.5
  ```
  - можно так же посмотреть `kubectl get all -A`.
- cluster готов, но самое время поменять конфиг kube proxy:
```
kubectl edit -n kube-system configmap/kube-proxy
```
меняем mode на ipvs.
по традиции надо порестартить kube proxy поды:
```
kubectl get po -n kube-system | grep kube-proxy | awk '{print $1}' | while read name; do kubectl delete po -n kube-system $name; done
```
- cluster готов, но он не будет работать без cni:
  - включаем dns64 в локальном unbound на всех тачках, иначе calico не осилит выкачать контейнеры.
  - качаем calico.yaml:
  ```
  curl https://projectcalico.docs.tigera.io/manifests/calico.yaml -o calico.yaml
  ```
  - идем делать там "none" мод и ipv6 only, делаем по [доке](https://projectcalico.docs.tigera.io/networking/ipv6#enable-ipv6-only), у меня получился такой diff:
    - calico_backend: "none"
    - меняем ipam на:
    ```
    "ipam": {
        "type": "calico-ipam",
        "assign_ipv4": "false",
        "assign_ipv6": "true"
    },
    ```
    - `CALICO_ROUTER_ID` закоментить
    - IP -> "none"
    - IP6 -> "autodetect"
    - CALICO_IPV4POOL_IPIP -> "NEVER"
    - CALICO_IPV6POOL_CIDR -> "2001:db8:42:0::/56"
    - FELIX_IPV6SUPPORT -> true
  - деплой calico:
  ```
  kubectl apply -f calico.yaml
  ```
  - смотрим в `kubectl get all -A`, убеждаемся что все запустилось.
  - И даже сейчас поды не заработают, нужно прибить к нодам сеточки, делается это примерно так:
  ```
  sas-test-k8s0.net:~# cat calico-n0.yaml 
  apiVersion: projectcalico.org/v3
  kind: IPPool
  metadata:
    name: ipv6-pool-n01
  spec:
    cidr: 2a02:6b8:c02:563:0:675::/96
    natOutgoing: false
    nodeSelector: kubernetes.io/hostname == "sas-test-n0.net.yandex.net" || kubernetes.io/hostname == "sas-test-n1.net.yandex.net"
  sas-test-k8s0.net:~# ./calicoctl apply -f calico-n0.yaml 
  ```
  результатом должно стать подобное:
  ```
  sas-test-k8s0.net:~# ./calicoctl get ippool
  NAME                  CIDR                          SELECTOR                                                                                                           
  default-ipv4-ippool   192.168.0.0/16                all()                                                                                                              
  ipv6-pool-n01         2a02:6b8:c02:563:0:675::/96   kubernetes.io/hostname == "sas-test-n0.net.yandex.net" || kubernetes.io/hostname == "sas-test-n1.net.yandex.net"   
  ipv6-pool-n2          2a02:6b8:c02:5cc:0:675::/96   kubernetes.io/hostname == "sas-test-n2.net.yandex.net"                               
  ```
- coredns в нашем случае не запускается из-за [лупа](https://coredns.io/plugins/loop/), идем в конфигмапу coredns и припиливаем любой нормальный днс сервер:
```
kubectl edit -n kube-system configmap/coredns
```
- еще нюанс, tor не знает что на нашем сервере есть еще ipшнеги из /96 сетки кроме нашего, поэтому ему нужно сообщить об этом, дабы пакеты снаружи роутились в наш сервер тором. Ставим ndppd на каждую воркер ноду и подсовываем подобный конфиг:
```
proxy eth0 {
    rule 2a02:6b8:c02:563:0:675::/96 {
        static
    }
}
```
в дальнешйем можно будет заюзать специальный влан, в котором анонсится вся подсетка.
- ура, все готово, я бы ребутнул для порядка!

## yandex docker registry

- делаем файлик для секрета:
```
sas-test-k8s0.net:~/kuber# cat registry.secret
{
    "auths": {
        "registry.yandex.net": {
	    "auth": "TOKEN"
        }
    }
}
```
- `kubectl create secret generic registry --from-file=./registry.secret`
- делаем ServiceAccount:
```
cat sa.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: sa
imagePullSecrets:
  - name: registry
kubectl apply -f sa.yaml
```
- пример использования:
```
sas-test-k8s0.net:~/kuber# cat test.yaml 
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-test
spec:
  serviceAccountName: sa
  containers:
  - name: ubuntu-test
    image: registry.yandex.net/ubuntu
```

## Как это выглядит в работе

- деплоем тестовую приложеньку:
```
sas-test-k8s0.net:~# cat deployment-hello.yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-node
spec:
  selector:
    matchLabels:
      app: hello-node
  template:
    metadata:
      labels:
        app: hello-node
    spec:
      containers:
        - image: sqeven/echoserver:1.4
          name: echoserver
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: hello-node
  labels:
    app: hello-node
spec:
  type: NodePort
  ports:
    - port: 80
      targetPort: 80
      protocol: TCP
      nodePort: 30666
  selector:
    app: hello-node
```
- смотрим что создалось:
```
sas-test-k8s0.net:~# kubectl get all -o wide
NAME                              READY   STATUS    RESTARTS        AGE     IP                                 NODE                         NOMINATED NODE   READINESS GATES
pod/hello-node-5987c87f8d-zrrfb   1/1     Running   4 (4d19h ago)   5d21h   2a02:6b8:c02:563:0:675:17d0:cb03   sas-test-n1.net.yandex.net   <none>           <none>

NAME                 TYPE        CLUSTER-IP            EXTERNAL-IP   PORT(S)        AGE     SELECTOR
service/hello-node   NodePort    2001:db8:42:1::3ba1   <none>        80:30666/TCP   5d23h   app=hello-node
service/kubernetes   ClusterIP   2001:db8:42:1::1      <none>        443/TCP        11d     <none>

NAME                         READY   UP-TO-DATE   AVAILABLE   AGE     CONTAINERS   IMAGES                  SELECTOR
deployment.apps/hello-node   1/1     1            1           5d23h   echoserver   sqeven/echoserver:1.4   app=hello-node

NAME                                    DESIRED   CURRENT   READY   AGE     CONTAINERS   IMAGES                  SELECTOR
replicaset.apps/hello-node-5987c87f8d   1         1         1       5d23h   echoserver   sqeven/echoserver:1.4   app=hello-node,pod-template-hash=5987c87f8d
```
- проверяем:
```
sas-test-k8s0.net:~# curl [2001:db8:42:1::3ba1]
CLIENT VALUES:
client_address=2a02:6b8:c02:5cc:0:675:9092:86e8
command=GET
real path=/
query=nil
request_version=1.1
request_uri=http://[2001:db8:42:1::3ba1]:80/

SERVER VALUES:
server_version=nginx: 1.10.0 - lua: 10001

HEADERS RECEIVED:
accept=*/*
host=[2001:db8:42:1::3ba1]
user-agent=curl/7.58.0
BODY:
-no body in request-
```
- почему это работает:
```
sas-test-k8s0.net:~# ipvsadm -L
IP Virtual Server version 1.2.1 (size=1048576)
Prot LocalAddress:Port Scheduler Flags
  -> RemoteAddress:Port           Forward Weight ActiveConn InActConn
TCP  [2001:db8:42:1::1]:https rr
  -> [sas-test-k8s0.net.yandex.net]:6443 Masq    1      0          0         
  -> [sas-test-k8s1.net.yandex.net]:6443 Masq    1      2          0         
  -> [sas-test-k8s2.net.yandex.net]:6443 Masq    1      1          0         
TCP  [2001:db8:42:1::a]:domain rr
  -> [2a02:6b8:c02:563:0:675:e63b:3704]:domain Masq    1      0          0         
  -> [2a02:6b8:c02:5cc:0:675:8c36:9141]:domain Masq    1      0          0         
TCP  [2001:db8:42:1::a]:9153 rr
  -> [2a02:6b8:c02:563:0:675:e63b:3704]:9153 Masq    1      0          0         
  -> [2a02:6b8:c02:5cc:0:675:8c36:9141]:9153 Masq    1      0          0         
TCP  [2001:db8:42:1::3ba1]:http rr
  -> [2a02:6b8:c02:563:0:675:17d0:cb03]:http Masq    1      0          1         
TCP  [fb-sas-test-k8s0.net.yandex.net]:30666 rr
  -> [2a02:6b8:c02:563:0:675:17d0:cb03]:http Masq    1      0          0         
TCP  [sas-test-k8s0lb.net.yandex.net]:30666 rr
  -> [2a02:6b8:c02:563:0:675:17d0:cb03]:http Masq    1      0          0         
TCP  [sas-test-k8s0.net.yandex.net]:30666 rr
  -> [2a02:6b8:c02:563:0:675:17d0:cb03]:http Masq    1      0          0         
UDP  [2001:db8:42:1::a]:domain rr
  -> [2a02:6b8:c02:563:0:675:e63b:3704]:domain Masq    1      0          0         
  -> [2a02:6b8:c02:5cc:0:675:8c36:9141]:domain Masq    1      0          0         
```
на каждой тачке создаются такие сервисы.
Так что можно натравить L3 балансер прям на ноды и все будет работать даже если под один.

## nginx ingress
ingress nginx это и есть nginx просто интегрированный в кубер, т.е. к нему конфиги можно например деплоить ямликами.
`wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.1/deploy/static/provider/baremetal/deploy.yaml`
меняем Deployment на DaemonSet дабы наш nginx запускался на каждом сервере, а так же удаляем "ipFamilyPolicy: SingleStack" и "ipFamilies:" для работы с ipv6
добавляем к NodePort "externalTrafficPolicy: Local", пусть трафик попадает всегда в локальный nginx.
деплоим как обычно.
есть еще вариант просто удалить полностью NodePort сервис и у DaemonSet добавить настройку "hostNetwork: true", тогда nginx просто будет слушать сеть воркер ноды.
натягиваем L3 балансер на worker nodes и все начинает работать так как NodePort через iptables DNATит пакетики со всех external ip в наш nginx локальный.

Нюансы nginx ingress:
- похоже люди в кубере никогда не настраивали маломальски сложные конфиги в nginx, хотя вероятно это сделано ради унификации с другими ingress. Сделать кастом очень сложно.
- например rewrite-target обязательно сработает у вас на все path и никак иначе.
- проблема NodePort(не самого nginx ingress): нельзя заставить DNATить только один external ip в ваш nginx, будет обязательно натить все подряд, хотя технически ничего не мешает.
- для reverse proxy в левый эндпоинт нужно завести сервис в кубере с типом externalName и проксировать в него, при этом у вас возникнет отдельная проблема с реврайтами.

## Дебаг(стоит дополнить)

Яростно юзаем:
- `kubectl describe` на все подряд
- `kubectl logs` на все подряд
- `kubectl exec -ti` когда совсем беда

## TODO

- запилить модуль для hbf агента, выдергивать адреса подов.
- сделать multi cni для поднятия tun64 и подобного в подах.(спасибо Сереге за идею)

## Автор статьи

Борис Литвиненко - borislitv@yandex-team.ru
